# FAMILYGUARD — FAZ 0 / GÖREV 001 — ÜCRETSİZ HAZIRLIK RAPORU

**Tarih:** 25 Kasım 2026 • **Dayanak:** Revizyon 4, Faz 0 görev listesi
**Kapsam dışı (yapılmadı):** kurulum, hesap açma, Supabase projesi, harcama, kod, e-posta gönderimi.
**Faz 0 ilerlemesi:** 0/19 PASS. Araştırma tamamlanan görevler teknik test yapılmadığı için PASS değildir.
**Not:** Tasarım sorumluluğu proje sahibi ve ürün direktöründedir. Claude ekran tasarlamaz; yalnızca onaylı PNG referanslarını kodlar.

---

## 1. Geliştirme ortamı — DURUM: BLOCKED (veri yok)

Claude'a bu oturumda bağlı tek cihaz Windows bilgisayardır (win32/x64). Xcode, iOS SDK ve simülatörler yalnızca macOS'ta çalıştığı için Mac ortamı buradan okunamadı. Hiçbir şey kurulmadı veya değiştirilmedi.

Proje sahibinin Mac Terminal'de çalıştıracağı salt okunur kontrol komutu (hiçbir şey kurmaz veya değiştirmez):

```
sw_vers; xcodebuild -version; swift --version; xcodebuild -showsdks | grep -i ios; xcrun simctl list runtimes; xcrun simctl list devices available | grep -i iphone | head -20
```

Bu komutun çıktısı geldiğinde şu maddeler raporlanacak: macOS sürümü, Xcode sürümü, Swift sürümü, iOS SDK'ları, iOS 17 simülatör çalışma zamanı var mı, mevcut iPhone simülatörleri.

- **Apple Developer hesabı:** Proje sahibinin bireysel hesabı mevcut (Team ID kayıtlı). Hangi yeteneklerin (App Attest, Time Sensitive, Critical Alerts) açılabileceği, kalıcı Bundle ID oluşturmadan doğrulanamaz. **BELİRSİZ.**

---

## 2. Supabase ücretsiz ön araştırma

### 2.1 Doğrulanmış fiyat yapısı (supabase.com/pricing, 25.11.2026)
| Kalem | Pro dahil | Aşım |
|---|---|---|
| Taban ücret | 25 USD/ay | — |
| Compute kredisi | 10 USD/ay (1 Micro) | — |
| Ek proje | — | 10 USD/ay'dan başlar |
| Realtime mesaj | 5 milyon/ay | 2,50 USD / milyon |
| Tepe bağlantı | 500 | 10 USD / 1.000 |
| Egress | 250 GB | 0,09 USD/GB |
| Disk | 8 GB / proje | 0,125 USD/GB |
| Günlük yedek | 7 gün | — |
| Auth MAU | 100.000 | 0,00325 USD/MAU |

### 2.2 Ayrı test projesinin tahmini ek maliyeti
- Pro organizasyonda yeni bir Micro proje: **yaklaşık +10 USD/ay**. Compute kredisi zaten mevcut projelerce kullanılıyor; bu yüzden ikinci kez düşülmez. Saatlik ücretlendirme nedeniyle proje yalnızca test süresince açık tutulursa maliyet düşer. **Tahmin; kesin değil.**
- Realtime, bağlantı ve egress kotaları organizasyonda ortaktır. Test trafiği Underworld ve Brain Lab ile aynı kotadan düşer.
- Mevcut projelerin kota kullanımı: **BLOCKED.** Claude'un Supabase erişimi yalnızca Free organizasyonu görüyor; VDOX Lab Pro organizasyonuna erişimi yok. Veriyi proje sahibi Usage ekranından alabilir.

### 2.3 Ücretsiz alternatif: yerel Supabase (önerilen ilk adım)
- `supabase start` yerel olarak Postgres, Auth, REST, Edge Functions, Storage ve **Realtime** çalıştırır. Kaynak: supabase.com/docs/guides/local-development/cli/getting-started
- Gereksinim: Docker uyumlu bir konteyner yöneticisi (macOS'ta OrbStack önerilir, Windows'ta Docker Desktop).
- Yerel ortamın riski yoktur: gerçek kişisel veri uzak sunucuya gitmez, harcama yoktur, Underworld ve Brain Lab etkilenmez.

### 2.4 Yerelde yapılabilecek / yapılamayacak testler
| Test | Yerel | Not |
|---|---|---|
| RLS politikaları, çapraz aile erişimi, rol yükseltme | ✅ | Tamamen yerelde test edilebilir |
| `map_viewers` lease, tetikleyici, Private Broadcast yetkisi | ✅ | Mantık doğrulaması |
| Yetki iptali ve Realtime kanal davranışı | ✅ | Bkz. 2.5 |
| Gerçek mesaj sayımı, faturalama, kota ölçümü (F0-03, F0-11) | ❌ | Barındırılan proje gerekir |
| Gerçek iPhone'dan uzak bağlantı ve ağ gecikmesi | ⚠️ | Telefon aynı ağdan yerel makineye bağlanabilir; internet koşulları temsil edilmez |
| APNs uçtan uca | ⚠️ | Edge Function yerelde çalışır; APNs geliştirme ortamı ayrıca gerekir |

### 2.5 ⚠️ TEKNİK ENGEL — Realtime yetki önbelleği
Supabase belgesine göre Private kanal yetkisi kanala katılırken hesaplanıp önbelleğe alınır; her mesajda veritabanı sorgulanmaz. Yetki kaldırılan istemci, JWT süresi dolana veya yeni JWT gönderilene kadar mesaj almaya devam eder. Kaynak: supabase.com/docs/guides/realtime/authorization

**Etkisi:** M03-01b ("Yetki iptalinde canlı akış lease beklenmeden hemen kesilir", P0) ve M01-13 yalnızca RLS ile karşılanamaz. Aile haritasında başka bir yetkili izleyici aktifken aynı kanala Broadcast gönderilir; iptal edilen istemci de o kanalda olduğu için mesajları görmeye devam eder.

**Çözüm önerisi (şartnamede zaten var: M01 madde 38, "kanal güvenlik sürümü"):**
1. Kanal adına bir güvenlik sürümü eklenir (ör. `family:<id>:v<n>`).
2. Yetki iptalinde sunucu sürümü artırır ve tetikleyici yeni mesajları yalnızca yeni kanala gönderir. Eski kanaldaki istemci yeni veri almaz.
3. Yetkili istemciler yeni kanala yeniden abone olur (sunucudan sürüm sorgusuyla).
4. JWT süresi kısa tutulur (ek savunma).

Bu, kapsam değişikliği değil, mevcut kuralın uygulama yöntemidir. Yerel ortamda F0-02 kapsamında doğrulanmalıdır.

---

## 3. Apple teknik araştırması

**Durum:** Bu bölüm Claude'un mevcut teknik bilgisine dayanır. Resmî belge sayfaları bu oturumda tek tek açılmadı; her satır resmî bağlantıyla yeniden doğrulanacaktır. **Tamamı BELİRSİZ (doğrulama bekliyor).**

| Konu | iOS 17 uyumu | Bilinen sınır | Gerçek cihazda doğrulanacak |
|---|---|---|---|
| Core Location (CLLocationManager / CLLocationUpdate) | ✅ (CLLocationUpdate iOS 17+) | Arka planda askıya alma; doğruluk ortama bağlı | Güncelleme aralığı, doğruluk, kilit ekranı davranışı (F0-01) |
| CLMonitor | ✅ iOS 17+ | Uygulama başına 20 koşul | 20 sınırı, kayıt hataları, yeniden başlatma sonrası (F0-07) |
| Significant Location Change | ✅ | Düşük hassasiyet (~500 m+), seyrek | Zorla kapatma sonrası uygulamayı uyandırıyor mu (F0-01) |
| Visits | ✅ | Gecikmeli teslim | Hareketsizlik bilgisi kaynağı olarak kullanılabilir mi (F0-15) |
| Arka plan konum izni | ✅ | "Her zaman" izni iki aşamalı; kullanıcı her an düşürebilir | İzin değişikliklerinin algılanması (F0-01) |
| Zorla kapatma | — | Kullanıcı uygulamayı kapattığında standart arka plan güncellemeleri durur; bölge ve önemli değişiklik olayları uygulamayı yeniden başlatabilir | Davranışın test edilmesi (F0-01, F0-07) |
| App Attest | ✅ (iOS 14+) | Simülatörde çalışmaz; anahtar cihaza özgüdür | Attestation/assertion akışı (F0-05) |
| Time Sensitive bildirim | ✅ (iOS 15+) | Odak modunu kullanıcı izin verirse aşar; sessiz modu aşmaz | Odak ve sessiz modda davranış (F0-06) |
| Critical Alerts | ✅ | Apple'dan özel yetki gerekir; onay garantisi yok | Başvuru taslağı (gönderilmeyecek) |
| APNs yerelleştirme | ✅ | `loc-key`/`loc-args` metinleri uygulama paketinde olmalı | Kapalı uygulamada dil, RTL (F0-18) |
| MessageUI | ✅ | SMS yalnızca kullanıcı onayıyla gönderilir; simülatörde SMS yok | Gerçek SIM'li cihazda SOS SMS akışı |
| StoreKit 2 | ✅ (iOS 15+) | Sandbox ve StoreKit Testing yerel yapılandırması mevcut | Grace Period ve iade senaryoları (F0-13) |
| Veri koruma sınıfları | ✅ | Complete Until First User Authentication, yeniden başlatma sonrası ilk kilit açılmadan erişimi engeller | SOS kuyruğu ve acil kişiler (F0-04) |

Resmî kaynaklar (doğrulama için):
- https://developer.apple.com/documentation/corelocation
- https://developer.apple.com/documentation/corelocation/clmonitor
- https://developer.apple.com/documentation/devicecheck/establishing-your-app-s-integrity
- https://developer.apple.com/documentation/usernotifications
- https://developer.apple.com/documentation/messageui
- https://developer.apple.com/documentation/storekit
- https://developer.apple.com/documentation/uikit/protecting-the-user-s-privacy/encrypting-your-app-s-files

---

## 4. İkinci iPhone gereksinimleri

### 4.1 Doğrulanmış bilgiler
- iOS 26, iPhone 11 ve sonrasını (A13 ve üstü) destekler; iPhone XS, XS Max ve XR'ı desteklemez.
- iOS 27 uyumluluğu: iPhone 11 serisinin destekten çıkacağı yönünde söylentiler vardı. WWDC 2026 sonrası bir habere göre Apple bu modelleri listede tuttu. **BELİRSİZ:** Apple'ın resmî listesiyle doğrulanmalıdır.

### 4.2 ⚠️ TEKNİK ENGEL — iOS 17'nin gerçek cihazda test edilmesi
- Apple eski iOS sürümlerine geri dönüşe izin vermez. iOS 17'yi gerçek cihazda test etmek için hiç güncellenmemiş, hâlâ iOS 17 kullanan bir iPhone gerekir. Böyle bir cihazı ödünç bulmak zordur.
- Öneri: iOS 17 uyumu **Xcode iOS 17 simülatöründe** test edilsin. Gerçek cihaz testleri ise ikinci cihazın üzerindeki en eski iOS sürümüyle yapılsın. Şartname "iOS 17 ve lansmandaki güncel iOS" dediği için bu yaklaşımın onayı ürün direktörüne aittir.

### 4.3 Önerilen ikinci cihaz (ödünç/mevcut)
| Öncelik | Model | Gerekçe |
|---|---|---|
| 1 | iPhone 12 / 12 mini / 13 | Daha eski nesil, güncel iOS'u alır, pil ve GPS karşılaştırması anlamlı |
| 2 | iPhone 11 / SE (2. nesil) | En eski destekli sınıf; iOS 27 desteği BELİRSİZ |
| 3 | iPhone XS / XR | Yalnızca iOS 18'e kadar; iOS 17/18 eski sürüm testi için değerli, ancak güncel iOS testi yapılamaz |

- **Minimum donanım:** GPS + SIM (MessageUI SMS testi için gerçek SIM şart) + iOS 17 veya üstü.
- **Pil sağlığı:** Pil sağlığı %80'in altındaki cihazlar pil testlerinde sapma yaratır. Her raporda pil sağlığı yüzdesi kaydedilir; mümkünse iki cihazın pil sağlığı birbirine yakın olmalıdır.

### 4.4 İki cihazlı test senaryoları
1. Ebeveyn (A) ↔ çocuk (B) QR ve manuel eşleştirme, çift taraflı onay.
2. B'de SOS → A'da bildirim, görüldü ve onaylandı durumları (gerçek acil servislere çağrı yapılmaz).
3. B çevrimdışı SOS → 15 dk içinde ve sonrasında bağlantı.
4. A harita açık/kapalı → B'den Broadcast sayımı.
5. B cihaz iptali → B'nin erişim ve yükleme denemeleri.
6. B güvenli bölge giriş/çıkış ve doğruluk.
7. Pil: aynı koşullarda 8 saatlik karşılaştırma.

---

## 5. Bağımsız izleme servisi

| Servis | Ücretsiz plan | Ücretsiz aralık | 60 sn için |
|---|---|---|---|
| UptimeRobot | 50 monitör | 5 dk (sabit) | Solo planı (60 sn, 10 monitör) |
| Better Stack | 10 monitör, 1 durum sayfası | 3 dk | Ücretli plan (30 sn'ye kadar) |
| HetrixTools | 15 uptime monitörü | 1 dk | Ücretsiz planda 1 dk (üçüncü taraf kaynağa göre; **BELİRSİZ**) |

- UptimeRobot'ın ücretsiz planda ticari kullanım koşulu kaynaklar arasında çelişkili. Bir kaynak 2024'te "yalnızca kişisel" olduğunu, bir diğeri Mayıs 2026 koşullarıyla ticari kullanıma izin verildiğini söylüyor. **BELİRSİZ:** Güncel kullanım koşulları okunmalıdır.
- Şartnamedeki 60 sn hedefini ücretsiz planlardan yalnızca HetrixTools karşılıyor gibi görünüyor; doğrulanmalı. Karşılamazsa UptimeRobot Solo planı en düşük maliyetli seçenektir; aylık ücret pricing sayfasından doğrulanmalı.
- Bütün servisler Supabase'den bağımsız çalışır. Sağlık kontrolü uç noktası kişisel veri döndürmemelidir (yalnızca "ok / hata kodu").
- Hesap açılmadı.

---

## 6. Hukuki hazırlık

### 6.1 Supabase'e gönderilecek sorular
Revizyon 4, Bölüm 5 / M08 madde 8'deki İngilizce metin hazırdır. Gönderilmeden önce imza satırı veri sorumlusunun resmî adıyla ("Halil İbrahim Karademir, individual developer, operating under the brand VDOX Lab") güncellenmelidir. **Gönderilmedi.**

### 6.2 Hukuk uzmanı kontrol listesi
**KVKK**
- [ ] Veri sorumlusu statüsü (bireysel geliştirici) ve VERBİS kayıt yükümlülüğü
- [ ] Çocuk konum verisinin hukuki sınıflandırması (m. 6 özel nitelikli mi)
- [ ] Açık rıza mı, başka hukuki sebep mi
- [ ] m. 9 yurt dışı aktarım: standart sözleşme, 5 iş günü bildirim, taraflar
- [ ] Aydınlatma metni ve çocuk için yaşa uygun bilgilendirme

**GDPR**
- [ ] AB temsilcisi (m. 27) gerekliliği
- [ ] Supabase DPA'sının yeterliliği; alt işleyenler
- [ ] Çocuk rızası yaşı (ülkeye göre 13–16)
- [ ] Veri koruma etki değerlendirmesi (DPIA) gerekliliği

**Çocukların konum verileri ve veli doğrulaması**
- [ ] Hangi yaş aralıkları; hangi yaş sınırları
- [ ] Veli doğrulama yöntemi (e-posta yetmez; ücretsiz ve hukuka uygun seçenekler)
- [ ] COPPA "verifiable parental consent" yöntemleri (ABD yayını için)
- [ ] Ayrı yaşayan ebeveynler ve velayet anlaşmazlığı

**Uluslararası aktarım**
- [ ] Frankfurt bölgesi ile Türkiye kullanıcıları
- [ ] APNs (Apple, ABD) üzerinden aktarılan teknik verilerin durumu
- [ ] Google Maps SMS bağlantısının üçüncü taraf paylaşımı

**Saklama ve silme**
- [ ] 24 saat / 30 gün konum geçmişi ve 7 günlük hesap silme süreleri
- [ ] Yedeklerden doğal sona erme (7 gün) yeterli mi
- [ ] Aileden ayrılan kişinin eski aile ilişkisindeki veriler
- [ ] Zorunlu işlem kayıtlarının (satın alma) saklama süresi

**Yetişkin hesabına dönüşüm**
- [ ] Yaş geçişinin doğrulanma yöntemi
- [ ] Eski ebeveyn erişimlerinin ve geçmiş verilerin durumu

**Kötüye kullanım ve izinsiz takip**
- [ ] Gizli takip yasağının yeterliliği
- [ ] Aile içi şiddet ve partner takibi senaryoları için yükümlülükler
- [ ] Kötüye kullanım bildirimine yanıt yükümlülüğü

E-posta gönderilmedi; danışmanlık alınmadı; gerçek kişisel veri işlenmedi.

---

## 7. Faz 0 bağımlılık tablosu

Sütunlar: **Ar** ücretsiz araştırmayla hazırlanabilir • **Yr** yerel ortamda test edilebilir • **2C** ikinci gerçek iPhone gerektirir • **SB** Supabase test projesi gerektirir • **Hk** hukuki onay gerektirir • **Bt** bütçe onayı gerektirir

| Görev | Konu | Ar | Yr | 2C | SB | Hk | Bt | Durum |
|---|---|---|---|---|---|---|---|---|
| F0-01 | Adaptif konum motoru | ✅ | ✅* | ✅ | — | ✅* | — | NOT STARTED |
| F0-02 | Lease + Broadcast tetikleyicisi | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-03 | Realtime %90 ölçümü | ✅ | ⚠️ | — | ✅ | — | ✅ | NOT STARTED |
| F0-04 | Veri koruma sınıfı | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-05 | App Attest | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-06 | Critical Alerts / Time Sensitive | ✅ | ✅ | ✅ | — | — | — | NOT STARTED |
| F0-07 | 20 koşul bütçesi | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-08 | Bölge doğruluğu | ✅ | ✅* | ✅ | — | ✅* | — | NOT STARTED |
| F0-09 | Bağımsız izleme | ✅ | ⚠️ | — | ✅ | — | ⚠️ | IN PROGRESS (araştırma) |
| F0-10 | Organizasyon kota kullanımı | ✅ | — | — | — | — | — | BLOCKED (Pro organizasyon erişimi yok) |
| F0-11 | Maliyet ve yük modeli | ✅ | ⚠️ | — | ✅ | — | ✅ | NOT STARTED |
| F0-12 | MapKit sınırları | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-13 | Grace Period ve geçiş hakkı | ✅ | ✅ | — | ⚠️ | — | — | NOT STARTED |
| F0-14 | SOS tetikleme yöntemi | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-15 | Tazelik eşikleri | ✅ | ✅* | ✅ | — | ✅* | — | NOT STARTED |
| F0-16 | 15 dk SOS kuyruğu | ✅ | ✅ | ✅ | — | — | — | NOT STARTED |
| F0-17 | Düşük pil algılama | ✅ | ✅ | ✅ | — | — | — | NOT STARTED |
| F0-18 | APNs yerelleştirme | ✅ | ✅ | — | — | — | — | NOT STARTED |
| F0-19 | SOS yüksek hassasiyet süresi | ✅ | ✅* | ✅ | — | ✅* | — | NOT STARTED |

\* **Yalnızca cihaz içinde kayıt:** Gerçek konum ölçümleri telefonda yerel dosyaya yazılır ve rapor olarak dışa aktarılır; uzak sunucuya hiç gönderilmez. Bu yöntemin hukuki ön onayı (Revizyon 4 kabulü, C bölümü madde 3) yine de gerekir, ancak uzak sunucu aktarımı olmadığı için onayın daha hızlı alınabileceği değerlendirilmektedir.
⚠️ Kısmen.

**İkinci cihaz olmadan hemen başlayabilecekler:** F0-02, F0-04, F0-05, F0-07, F0-12, F0-13, F0-14, F0-18. Hepsi Mac + iPhone 17 Pro Max + yerel Supabase ile yapılabilir.

---

## 8. Özet

### Gerekli kaynaklar
Mac (Xcode, yerel Supabase için OrbStack/Docker) • iPhone 17 Pro Max (mevcut) • ödünç ikinci iPhone • gerçek SIM (SMS testi) • Apple Developer hesabı (mevcut).

### Tahmini maliyetler (teklif değildir)
| Kalem | Tahmin |
|---|---|
| Yerel Supabase, Xcode, sandbox | 0 USD |
| Pro organizasyonda test projesi (F0-03/F0-11 için, gerekirse) | ~10 USD/ay, açık kaldığı saat kadar |
| 60 sn izleme (ücretsiz plan yetmezse) | Düşük aylık ücret; doğrulanacak |
| İkinci iPhone | Ödünç → 0 USD |
| Hukuk ve marka | Teklif gerekli |

### Teknik engeller
1. **Realtime yetki önbelleği** (2.5): M03-01b ancak kanal sürümü döndürmeyle karşılanabilir.
2. **iOS 17 gerçek cihaz testi** (4.2): Pratik olarak simülatörle sınırlı.
3. **Mac ortamı okunamadı** (1): Çıktı proje sahibinden bekleniyor.
4. **Pro organizasyon kota verisi okunamadı** (2.2).

### Proje sahibinden gereken kararlar (sırayla, tek tek)
1. Mac kontrol komutunun çıktısının paylaşılması.
2. Yerel Supabase (OrbStack/Docker) kurulumuna onay.
3. Ödünç ikinci iPhone'un modeli ve iOS sürümü.
4. Pro organizasyon Usage ekranı verileri.

### Ürün direktöründen gereken kararlar
1. Realtime yetki iptalinde kanal sürümü döndürme yönteminin kabulü (uygulama yöntemi; kapsam değişikliği değil).
2. iOS 17 uyumunun simülatörde, gerçek cihaz testlerinin ise mevcut en eski iOS sürümünde yapılması.
3. "Yalnızca cihaz içinde kayıt" yönteminin hukuki ön değerlendirmeye sunulması.

## Kaynaklar
- Supabase Pricing: https://supabase.com/pricing
- Supabase Local Development: https://supabase.com/docs/guides/local-development
- Supabase CLI Getting Started: https://supabase.com/docs/guides/local-development/cli/getting-started
- Supabase Realtime Authorization: https://supabase.com/docs/guides/realtime/authorization
- UptimeRobot Pricing: https://uptimerobot.com/pricing.md
- Better Stack Check Frequency: https://betterstack.com/docs/uptime/check-frequency/
- iOS 26 uyumluluğu: https://www.macrumors.com/2025/08/05/will-my-iphone-support-ios-26
- iOS 27 söylenti ve haberleri: https://www.macrumors.com/2026/04/20/ios-27-compatible-iphone-models-rumor/ • https://en.ammonnews.net/print.php?id=92300
