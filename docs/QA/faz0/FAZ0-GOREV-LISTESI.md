# FAMILYGUARD — FAZ 0 TEKNİK FİZİBİLİTE GÖREV LİSTESİ

**Dayanak:** V1.1 — Revizyon 4 / Onaylı Ürün Baz Çizgisi, Bölüm 16 (T-1 … T-19) ve Nihai Şartname Denetimi E bölümü
**Durum:** Plan. Hiçbir görev başlatılmamıştır. Üretim kodlaması ve canlı altyapı kurulumu yapılmayacaktır.
**Not:** Denetim metni 17 belirsizlikten söz eder. Revizyon 4 netleştirmeleri iki yeni belirsizlik ekledi: T-18 (kapalı uygulamada APNs yerelleştirmesi) ve T-19 (SOS yüksek hassasiyet süresi ve geçici olay konumu sınırları). Bu liste 19 görevin tamamını kapsar.

## Genel kurallar
1. Bütün testler sentetik konumlar, hayalî aile hesapları ve kişisel veri içermeyen kayıtlarla yapılır.
2. Gerçek cihaz testlerinde test yapanın kendi konumu işlenir. Bu veri işleme yöntemi Karar 05 B-13 gereği ayrıca hukuki değerlendirmeye tabidir; değerlendirme tamamlanmadan konum kayıtları üretim altyapısına aktarılmaz. Test kayıtları test projesinde tutulur ve görev bitince silinir.
3. Faz 0 prototip arayüzleri nihai ürün ekranı değildir ve tasarım onayı gerektirmez (Karar 11 B-15).
4. Test için Supabase projesi açılması, harcama yapılması veya ücretli servis alınması proje sahibinin onayına bağlıdır. Underworld ve Brain Lab projelerine dokunulmaz.
5. Ölçülen her değer cihaz modeli, iOS sürümü, izin durumu, ağ durumu, pil sağlığı ve test tarihiyle `docs/QA/faz0/` altında kanıtlanır.
6. Bir görevin sonucu şartnamedeki bir parametreyi değiştiriyorsa bu yeni bir ürün kararı gerektirir; Claude değeri kendi başına değiştirmez.
7. Başarısızlık durumundaki alternatifler öneridir; uygulanmaları ürün direktörü kararına bağlıdır.

## Ortak kaynaklar
- **Cihaz A:** Proje sahibinin iPhone 17 Pro Max'i (mevcut).
- **Cihaz B:** Daha eski nesil ikinci iPhone (mevcut değil; temin edilmesi gerekir). iOS 17 desteği olan bir model önerilir.
- **Hesaplar:** Apple Developer (mevcut), App Store Connect Sandbox test kullanıcıları (ücretsiz), Supabase test projesi (onay gerekli).
- **Araçlar:** Xcode, Instruments (Energy Log, Location), Ayarlar > Pil ekranı.

---

### F0-01 · Adaptif konum motoru (T-1)
- **Amaç:** Mesafe tabanlı motorun gerçek davranışını ölçmek.
- **Doğrulanacak varsayım:** ~100 m hassasiyet ve 150–200 m kayıt mesafesiyle yürüyüş ve araçta yeterli güncelleme alınır; hareketsizden harekete geçiş durum makinesiyle güvenilir yakalanır.
- **Test yöntemi:** Prototip uygulama ile yürüyüş, araç ve uzun durgunluk senaryoları; ekran kilitli, düşük güç modu, uygulama zorla kapatılmış ve cihaz yeniden başlatılmış koşullar; konum izni değişiklikleri.
- **Cihaz/hesap:** Cihaz A + B, test projesi.
- **Kabul kriteri:** Her senaryoda güncelleme aralığı, doğruluk dağılımı ve kaçırılan hareket sayısı raporlanır; durum makinesi sık profil değişikliği yapmaz.
- **Kanıt:** Senaryo bazlı CSV kayıtları + harita izi ekran görüntüleri + rapor.
- **Alternatif:** Parametre ayarı (mesafe filtresi, hassasiyet), significant-change ağırlığının artırılması, bölge tabanlı uyandırma.
- **Hukuki bağımlılık:** Gerçek cihaz konum işleme yöntemi (Genel kural 2).
- **Bütçe:** Cihaz B.

### F0-02 · Harita izleyici lease ve Broadcast tetikleyicisi (T-2)
- **Amaç:** `map_viewers` + veritabanı tetikleyicisi + `realtime.send()` zincirinin doğruluğunu ve yükünü ölçmek.
- **Varsayım:** 120 sn lease ile izleyici yokken sıfır Broadcast; uygun yenileme aralığı bağlantı ve maliyet açısından kabul edilebilir.
- **Test yöntemi:** Sentetik konum yazımlarıyla izleyicili ve izleyicisiz senaryolar; normal kapanış, arka plana geçiş, ağ kesilmesi, yetki iptali; farklı yenileme aralıklarının karşılaştırılması.
- **Cihaz/hesap:** Cihaz A + B, test projesi.
- **Kabul kriteri:** İzleyici yokken Broadcast = 0; yetki iptalinde akış lease beklenmeden kesilir; yenileme aralığı için önerilen değer gerekçeli raporlanır.
- **Kanıt:** Supabase kullanım metrikleri, tetikleyici logları (kişisel veri yok), test raporu.
- **Alternatif:** Edge Function üzerinden gönderim, lease süresinin kısaltılması, istemci tarafı yeniden sorgu ağırlığı.
- **Hukuki bağımlılık:** Yok (sentetik veri).
- **Bütçe:** Test projesi.

### F0-03 · Realtime mesaj hacmi ve %90 hedefi (T-3)
- **Amaç:** Güncel mimarinin mesaj hacmini, karşılaştırılabilir eski modelle ölçmek.
- **Varsayım:** Aynı kullanıcı davranışı ve konum hacmiyle mesaj hacminde ~%90 azalma.
- **Test yöntemi:** Sentetik aile simülasyonu; aynı senaryo eski model (Postgres Changes) ve yeni model ile çalıştırılır; Karar 12-F madde 88'deki metrikler toplanır.
- **Cihaz/hesap:** Test projesi, simülasyon betiği.
- **Kabul kriteri:** Ölçüm raporu tamamlanır (yayın engeli değil); gereksiz Broadcast sıfır.
- **Kanıt:** Metrik tablosu + yöntem açıklaması.
- **Alternatif:** Oran tutmazsa güncelleme mesafesi ve izleyici politikası ürün direktörüne sunulur.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Test projesi kullanımı.

### F0-04 · SOS kuyruğu ve acil kişilerin veri koruma sınıfı (T-4)
- **Amaç:** Complete Until First User Authentication sınıfının yeniden başlatma sonrası davranışını doğrulamak.
- **Varsayım:** İlk kilit açılışından sonra kuyruk ve acil kişiler arka planda erişilebilir; yeniden başlatmadan sonra, ilk kilit açılmadan önce erişilemez.
- **Test yöntemi:** Cihazı yeniden başlatıp kilit açmadan ve açtıktan sonra erişim denemesi; arka plan görevlerinde okuma.
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Davranış belgelenir; kilit açılmadan önceki durum için kullanıcıya doğru bilgi gösterilir.
- **Kanıt:** Test logları + rapor.
- **Alternatif:** Kilit öncesi için asgari, şifreli ve kişisel veri içermeyen bir yedek (yalnızca acil numara) değerlendirilir.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-05 · Cihaz bağlama ve App Attest (T-5)
- **Amaç:** Oturumun başka cihaza taşınmasını zorlaştıracak doğrulama yöntemini seçmek.
- **Varsayım:** App Attest anahtarı ile sunucu tarafı doğrulama iOS 17'de uygulanabilir.
- **Test yöntemi:** Prototipte attestation ve assertion akışı; Keychain kopyalama ve oturum taşıma denemeleri.
- **Cihaz/hesap:** Cihaz A + B, Apple Developer.
- **Kabul kriteri:** Taşınan oturumla hassas işlem reddedilir; başarısız attestation durumunda güvenli geri dönüş davranışı tanımlanır.
- **Kanıt:** Test raporu.
- **Alternatif:** Sunucu tarafı cihaz kaydı + kısa ömürlü token + yeniden eşleştirme.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-06 · Critical Alerts başvurusu (T-6)
- **Amaç:** Apple'a Critical Alerts yetkisi başvurusunu hazırlamak.
- **Varsayım:** Yetki verilmeyebilir; yayın buna bağlı değildir.
- **Test yöntemi:** Başvuru metninin hazırlanması (kullanım gerekçesi, kullanıcı kontrolü); Time Sensitive davranışının Odak ve sessiz modda ölçülmesi.
- **Cihaz/hesap:** Apple Developer, Cihaz A + B.
- **Kabul kriteri:** Başvuru proje sahibinin onayıyla gönderilir; Time Sensitive davranışı raporlanır.
- **Kanıt:** Başvuru kopyası, Apple yanıtı, test raporu.
- **Alternatif:** Time Sensitive + SMS/arama yedeği (zaten zorunlu).
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-07 · Güvenli bölge izleme bütçesi (T-7)
- **Amaç:** CLMonitor ile 18 kullanıcı + 1 kalkış (+1 rezerv) bölgesinin 20 koşul sınırına sığdığını doğrulamak.
- **Varsayım:** Cihaz başına aktif koşul hiçbir senaryoda 20'yi aşmaz; kayıt hataları yakalanabilir.
- **Test yöntemi:** Maksimum bölge yükü, bölge ekleme/silme, Premium'dan ücretsize düşüş (18 → 2), kalkış bölgesinin yeniden kurulumu.
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Sınır aşılmaz; hata kullanıcıya gösterilir; aktif olmayan bölge aktif görünmez.
- **Kanıt:** Test raporu.
- **Alternatif:** Bölge önceliklendirme ve dönüşümlü izleme.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-08 · Güvenli bölge doğruluğu (T-8)
- **Amaç:** Giriş/çıkış saptama oranını ve yanlış alarmı ölçmek.
- **Varsayım:** 30 kontrollü geçişin ≥ %90'ı 5 dakika içinde saptanır; 8 saatlik sınır yakını durağan testte ≤ 1 yanlış olay.
- **Test yöntemi:** Farklı yarıçaplarla (150–300 m) kontrollü geçişler; doğruluk filtresi ve kalış süresi varyasyonları.
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Hedefler sağlanır veya eşikler gerekçeyle yeniden önerilir.
- **Kanıt:** Geçiş tablosu + rapor.
- **Alternatif:** Yarıçap ve kalış süresi ayarı; "olası giriş" durumunun genişletilmesi.
- **Hukuki bağımlılık:** Gerçek cihaz konum işleme yöntemi.
- **Bütçe:** Yok.

### F0-09 · Bağımsız sunucu izleme (T-9)
- **Amaç:** 60 sn aralıklı bağımsız izleme servisini seçmek.
- **Varsayım:** Ücretsiz bir servis 60 sn aralığı ve e-posta + ikinci kanal bildirimini destekler.
- **Test yöntemi:** Aday servislerin özelliklerinin karşılaştırılması; test projesinde sağlık uç noktası (veritabanı, SOS kayıt yolu, bildirim kuyruğu kontrolü, gerçek SOS göndermeden).
- **Cihaz/hesap:** İzleme servisi hesabı (onay gerekli), test projesi.
- **Kabul kriteri:** Kesinti ve düzelme algılanır; kişisel veri loglanmaz; gerçek ailelere bildirim gitmez.
- **Kanıt:** Kesinti simülasyonu raporu.
- **Alternatif:** Düşük maliyetli ücretli plan (ürün direktörü onayıyla).
- **Hukuki bağımlılık:** Servisin veri işleme kapsamı (kişisel veri yok).
- **Bütçe:** Ücretsiz plan yetmezse teklif.

### F0-10 · Supabase organizasyon kota kullanımı (T-10)
- **Amaç:** VDOX Lab Pro organizasyonundaki mevcut kota tüketimini görmek.
- **Varsayım:** Underworld ve Brain Lab'den sonra FamilyGuard için kota payı kalıyor.
- **Test yöntemi:** Proje sahibinin Supabase Usage ekranından alacağı veriler.
- **Cihaz/hesap:** Supabase VDOX Lab Pro organizasyonu (proje sahibi erişimi).
- **Kabul kriteri:** Mesaj, bağlantı, egress ve compute kullanımı tabloya işlenir.
- **Kanıt:** Kullanım ekran görüntüleri.
- **Alternatif:** Maliyet modelinin "kota dolu" senaryosuyla hesaplanması.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-11 · Maliyet ve yük modeli (T-11)
- **Amaç:** Güncel mimari için 100 / 1.000 / 10.000 aile maliyetini ve yükünü hesaplamak.
- **Varsayım:** F0-01, F0-02, F0-03 ve F0-10 verileriyle güvenilir model kurulabilir.
- **Test yöntemi:** Ölçülen aile başına değerlerle model; sentetik yük testi (API p95, hata oranı).
- **Cihaz/hesap:** Test projesi.
- **Kabul kriteri:** Ücretsiz ve Premium aile başına tahmini maliyet ve yük sonuçları raporlanır.
- **Kanıt:** Maliyet tablosu + yük testi raporu.
- **Alternatif:** Ekonomi sürdürülemez çıkarsa ürün direktörüne sunulur; genel yayına geçilmez.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Test projesi kullanımı.

### F0-12 · MapKit servis sınırları (T-12)
- **Amaç:** V1'de kullanılan MapKit özelliklerinin sınırlarını ve V1.1 için rota/ETA erişimini belgelemek.
- **Varsayım:** V1 harita gösterimi ek maliyet ve kota sorunu yaratmaz.
- **Test yöntemi:** Apple belgelerinin incelenmesi + prototipte harita yükleme davranışı.
- **Cihaz/hesap:** Cihaz A.
- **Kabul kriteri:** Sınırlar raporlanır.
- **Kanıt:** Kısa rapor + kaynak bağlantıları.
- **Alternatif:** Gerekirse önbellekleme.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-13 · Billing Grace Period ve geçiş hakkı (T-13)
- **Amaç:** Grace Period ile 7 günlük ürün geçişinin ayrımını sandbox'ta doğrulamak.
- **Varsayım:** App Store Server Notifications V2 olaylarıyla Grace Period başlangıcı, bitişi ve kesin sona erme ayırt edilebilir.
- **Test yöntemi:** Sandbox başarısız ödeme senaryoları; normal iptal, iade, ayrılma; ortak yıllık hakkın atomik tüketimi.
- **Cihaz/hesap:** App Store Connect sandbox kullanıcıları, test projesi.
- **Kabul kriteri:** Karar 12-D ve 13-A tablosundaki her durum doğru sonuç verir.
- **Kanıt:** Bildirim logları (kişisel veri yok) + test tablosu.
- **Alternatif:** Periyodik mutabakat ağırlığının artırılması.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-14 · SOS tetikleme yöntemi (T-14)
- **Amaç:** Basılı tutma ve kısa iptal penceresi yöntemlerini kullanılabilirlik açısından karşılaştırmak.
- **Varsayım:** Bir yöntem hem yanlışlıkla tetiklemeyi azaltır hem de yardımı geciktirmez.
- **Test yöntemi:** Prototip düğmeyle tek el, VoiceOver ve büyük yazı denemeleri.
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Seçilen yöntem gerekçesiyle Faz D tasarımına girdi olarak sunulur.
- **Kanıt:** Deneme kayıtları + rapor.
- **Alternatif:** İki yöntemin birlikte kullanılması.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-15 · Tazelik eşikleri ve hareketsizlik bilgisi (T-15)
- **Amaç:** Dinlenme, Normal ve SOS profilleri için tazelik eşiklerini belirlemek.
- **Varsayım:** iOS hareketsizlik bilgisini (Visits, significant-change, hareket verisi) GPS'e zorlamadan yeterli sıklıkta sağlar.
- **Test yöntemi:** Uzun durgunluk senaryoları; beş zaman bilgisinin ayrı kaydı (Karar 12-A).
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Profil başına önerilen eşikler; yanlış "güncel" gösterimi sıfır.
- **Kanıt:** Zaman serisi tablosu + rapor.
- **Alternatif:** Hareketsizlik bilgisi yoksa yalnızca ölçüm yaşı gösterilir.
- **Hukuki bağımlılık:** Gerçek cihaz konum işleme yöntemi.
- **Bütçe:** Yok.

### F0-16 · 15 dakikalık SOS kuyruk süresi (T-16)
- **Amaç:** Kuyruk süresinin uygunluğunu değerlendirmek.
- **Varsayım:** 15 dakika kısa kesintileri karşılar, eski olayların otomatik gönderilmesini önler.
- **Test yöntemi:** Farklı sürelerde bağlantı kesintisi; süre içinde ve sonrasında gönderim; iptal ile gönderimin eşzamanlı olması; idempotent doğrulama.
- **Cihaz/hesap:** Cihaz A + B, test projesi (gerçek kişilere bildirim gitmez).
- **Kabul kriteri:** M04-10b … M04-10f senaryoları geçer; süre için gerekçeli öneri.
- **Kanıt:** Test tablosu.
- **Alternatif:** Süre ayarı (ürün direktörü kararıyla).
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-17 · Düşük pil algılama (T-17)
- **Amaç:** Pil değişikliğinin ek GPS ve arka plan işi olmadan ne kadar güvenilir algılandığını ölçmek.
- **Varsayım:** Mevcut arka plan uyanmaları sırasında %20 eşiği yeterli sıklıkta yakalanır.
- **Test yöntemi:** Paylaşımı açık ve kapalı profillerle pil boşaltma senaryoları.
- **Cihaz/hesap:** Cihaz A + B.
- **Kabul kriteri:** Algılama gecikmesi raporlanır; tekrar bildirim oluşmaz.
- **Kanıt:** Rapor.
- **Alternatif:** Kullanıcıya "pil bilgisi uygulama açıldığında güncellenir" açıklaması.
- **Hukuki bağımlılık:** Yok.
- **Bütçe:** Yok.

### F0-18 · Kapalı uygulamada APNs yerelleştirmesi (T-18)
- **Amaç:** Uygulama kapalıyken bildirimlerin doğru dilde gösterilmesini sağlamak.
- **Varsayım:** APNs `loc-key` / `loc-args` ile uygulama paketindeki String Catalog metinleri kişisel veri göndermeden kullanılabilir.
- **Test yöntemi:** İki yöntemin (loc-key ve alıcı diline göre sunucu metni) karşılaştırılması; cihaz dili değişikliği; RTL dil.
- **Cihaz/hesap:** Cihaz A + B, APNs geliştirme sertifikası.
- **Kabul kriteri:** Kapalı uygulamada doğru dil; push içeriğinde kişisel veri yok.
- **Kanıt:** Ekran görüntüleri + payload örnekleri.
- **Alternatif:** Notification Service Extension ile cihazda yerelleştirme.
- **Hukuki bağımlılık:** Push içeriği denetimi (Bölüm 17).
- **Bütçe:** Yok.

### F0-19 · SOS yüksek hassasiyet süresi ve geçici konum sınırları (T-19)
- **Amaç:** SOS profilinin azami çalışma süresini ve yardım olayı konumlarının erişim ve saklama sınırlarını belirlemek.
- **Varsayım:** Belirli bir süre sonra normal profile dönüş, güvenliği bozmadan pili korur.
- **Test yöntemi:** Uzun süreli aktif SOS senaryosu; pil ölçümü; olay bitişinde erişimin kesilmesi.
- **Cihaz/hesap:** Cihaz A + B, test projesi.
- **Kabul kriteri:** Önerilen azami süre ve saklama sınırları; süresiz GPS ve süresiz erişim yok.
- **Kanıt:** Pil ölçümü + erişim testi raporu.
- **Alternatif:** Süre dolunca kullanıcıya "konum paylaşımına devam et" seçeneği.
- **Hukuki bağımlılık:** Saklama süreleri (Bölüm 17, madde 7).
- **Bütçe:** Yok.

---

## Faz 0 dışı ama paralel yürüyecek hukuki ve idari işler (proje sahibi)
1. Supabase'e KVKK standart sözleşme talebinin gönderilmesi.
2. KVKK uzmanı avukattan teklif alınması.
3. Hukuki veli doğrulama yönteminin uzmanla belirlenmesi.
4. Marka seçimi ve resmî marka incelemesi için teklif.
5. Cihaz B'nin temin edilmesi.

## Bütçe özeti (tutar teklif alınmadan atanmaz)
Cihaz B • Supabase test projesi kullanımı • bağımsız izleme (ücretsiz yetmezse) • hukuki danışmanlık • marka incelemesi.
