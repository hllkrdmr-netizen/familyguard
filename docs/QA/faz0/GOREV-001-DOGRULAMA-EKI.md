# FAMILYGUARD — GÖREV 001 DOĞRULAMA EKİ

**Tarih:** 25 Kasım 2026
**Dayanak:** Görev 001 Denetimi, D ve F bölümleri
**Yöntem:** Apple Developer Documentation sayfalarının resmî Markdown sürümleri (`.md`) okundu. HTML sayfaları JavaScript gerektirdiği için doğrudan okunamadı.
**Faz 0 ilerlemesi:** 0/19 PASS. Bu ek bir doğrulama kaydıdır; hiçbir görev PASS değildir.

Durum etiketleri: **DOĞRULANDI** (resmî belgede açıkça yazıyor) • **BELİRSİZ** (resmî belgede yok veya çelişkili; gerçek cihaz testi gerekli) • **DÜZELTME** (Görev 001 raporundaki bilgi değişti)

---

## 1. Apple teknik tablosu — satır satır doğrulama

### 1.1 Significant Location Change — DOĞRULANDI (kısmen)
- iOS 4.0+.
- Servis açıkken uygulama sonlandırılırsa, yeni olay geldiğinde sistem uygulamayı arka planda otomatik yeniden başlatır. Açılışta konum yöneticisi yeniden kurulmalı ve servis yeniden başlatılmalıdır.
- Bildirim, cihaz önceki bildirimden **500 m veya daha fazla** uzaklaştığında gelir; **beş dakikada birden sık** beklenmemelidir. Ağ verisi varsa bildirimler daha zamanında gelir.
- **BELİRSİZ:** Belge, kullanıcının uygulamayı **zorla kapatması** (uygulama değiştiriciden kaydırma) durumunu ayrıca ele almıyor. "Sistem tarafından sonlandırma" ile "kullanıcının zorla kapatması" ayrı tutulmalıdır (Denetim D-2). Zorla kapatma sonrası yeniden başlatma varsayılmayacak; F0-01'de gerçek cihazda test edilecek.
- Kaynak: https://developer.apple.com/documentation/corelocation/cllocationmanager/startmonitoringsignificantlocationchanges()

### 1.2 Bölge izleme / CLMonitor — DOĞRULANDI
- CLMonitor: **iOS 17.0+**.
- Core Location, bir uygulamanın **herhangi bir türde 20'den fazla koşulu aynı anda izlemesini engeller.**
- Koşul sağlandığında uygulama çalışmıyorsa sistem uygulamayı **başlatmayı dener**; uygulama yeniden açıldığında monitör **aynı tanımlayıcıyla** yeniden oluşturulmalıdır.
- ⚠️ **Yeni bulgu:** İzleme, cihaz yeniden başlatıldıktan sonra **ancak kullanıcı cihazın kilidini açtıktan sonra** gerçekleşebilir. Yeniden başlatma ile ilk kilit açılışı arasında güvenli bölge olayı alınamaz. Bu durum F0-04 ve F0-07'de gerçek cihazda ölçülecek; kullanıcıya gösterilecek bölge durumu buna göre doğru olmalıdır (aktif olmayan bölge aktif gösterilmez, M05-04).
- **BELİRSİZ:** Zorla kapatma sonrası bölge olaylarıyla yeniden başlatma belgede ayrıca açıklanmıyor; F0-07'de test edilecek.
- Kaynaklar: https://developer.apple.com/documentation/corelocation/clmonitor-2r51v • https://developer.apple.com/documentation/corelocation/monitoring-the-user-s-proximity-to-geographic-regions

### 1.3 Visits — DOĞRULANDI
- iOS 8.0+.
- Servis açıkken uygulama sonlandırılırsa, yeni ziyaret olayları hazır olduğunda sistem uygulamayı yeniden başlatır.
- Kesin konum izni istenmeden kullanılabilir; bu durumda ziyaret olayları azaltılmış doğrulukla gelir.
- Kaynak: https://developer.apple.com/documentation/corelocation/cllocationmanager/startmonitoringvisits()

### 1.4 Arka plan konumu — DOĞRULANDI (kısmen)
- iOS, uygulamaları arka plana geçtikten kısa süre sonra askıya alır. Askıdaki uygulama konum güncellemesi almaz; güncellemeler kuyruğa alınır ve uygulama yeniden çalıştığında teslim edilir.
- Arka plan güncellemeleri için "Location updates" arka plan modu gerekir ve `CLBackgroundActivitySession` başlatılır.
- Uygulama sonlandırılırsa konum API'leri açılışta yeniden başlatılmalıdır. Yetki durumu belirlenmemişse bu servisler açılışta başlatılmamalıdır.
- ⚠️ **BELİRSİZ — iOS 17 uyumu:** Belge `CLServiceSession` kullanımını öneriyor. Bu sınıfın iOS 17'de kullanılabilir olup olmadığı bu sayfada belirtilmiyor. iOS 17 minimum hedefi nedeniyle availability kontrolü ve iOS 17 alternatifi gerekebilir. Faz 1'den önce doğrulanacak.
- Kaynak: https://developer.apple.com/documentation/corelocation/handling-location-updates-in-the-background

### 1.5 App Attest — DOĞRULANDI
- Bütün cihazlar desteklemez; `isSupported` kontrolü zorunlu. Desteklenmiyorsa servis atlanır ve sunucu bu cihazdan assertion bekleyemez.
- ⚠️ **Yeni bulgu:** App Attest kullanmak için Apple Developer sitesinde **kayıtlı bir App ID** gerekir. Kalıcı Bundle ID oluşturma yasağıyla çakışmaması için F0-05'te yalnızca **geçici geliştirme kimliği** kullanılacaktır (Şartname 2.4 buna izin verir). Bu kayıt proje sahibinin onayına bağlıdır.
- Anahtarlar uygulama güncellemelerinde geçerli kalır; **yeniden yükleme, cihaz taşıma ve yedekten geri yüklemede geçersiz olur.** Bu, telefon değiştirme akışıyla (M01 madde 30–34) uyumludur.
- Aynı cihazdaki farklı kullanıcılar arasında anahtar paylaşılmamalıdır.
- Kaynak: https://developer.apple.com/documentation/devicecheck/establishing-your-app-s-integrity

### 1.6 Time Sensitive ve Critical Alerts — DOĞRULANDI
- `UNNotificationInterruptionLevel`: **iOS 15.0+**.
- **Time Sensitive:** Bildirimi hemen gösterir, ekranı aydınlatır, ses çalabilir ve sistem bildirim kontrollerini aşar.
- **Critical:** Hemen gösterir, ekranı aydınlatır ve **sessiz düğmesini aşarak** ses çalar.
- Critical Alerts yetkisi, uygulama kilitliyken, sessizdeyken veya Rahatsız Etme odağı açıkken bile ses çalınmasını sağlar. Yetki **Apple'ın başvuru formuyla** istenir. Başvuru gönderilmedi.
- Kaynaklar: https://developer.apple.com/documentation/usernotifications/unnotificationinterruptionlevel • https://developer.apple.com/documentation/bundleresources/entitlements/com.apple.developer.usernotifications.critical-alerts

### 1.7 APNs yerelleştirme ve içerik — DOĞRULANDI
- İki yöntem var: (a) yerelleştirilmiş metni doğrudan payload'a koymak (sunucunun kullanıcının dilini bilmesi gerekir), (b) metinleri uygulama paketinde tutup `title-loc-key`, `loc-key`, `loc-args` ile seçtirmek.
- Payload üst sınırı 4 KB.
- Apple, payload'a müşteri bilgisi veya hassas veri konulmamasını açıkça belirtir. Bu, şartnamenin "push içeriğinde kişisel veri yok" kuralıyla uyumludur.
- **BELİRSİZ:** Belge `Localizable.strings` dosyasından söz ediyor. Şartnamenin zorunlu kıldığı String Catalog (`.xcstrings`) ile `loc-key` uyumu F0-18'de gerçek cihazda doğrulanacak.
- Kaynak: https://developer.apple.com/documentation/usernotifications/generating-a-remote-notification

### 1.8 MessageUI — DOĞRULANDI
- `MFMessageComposeViewController`: iOS 4.0+.
- Göstermeden önce `canSendText()` çağrılmalı; false ise arayüz kullanılmamalı.
- Arayüz mesajın teslimini **garanti etmez**. Kişi iptal edebilir; gönderirse sorumluluk Mesajlar uygulamasındadır. Bu, M04 madde 15 ile uyumludur.
- Kaynak: https://developer.apple.com/documentation/messageui/mfmessagecomposeviewcontroller

### 1.9 Veri koruma sınıfı — DOĞRULANDI
- `completeUntilFirstUserAuthentication`: Dosya şifreli saklanır, cihaz açıldıktan sonra ilk kilit açılışına kadar erişilemez. İlk kilit açılışından sonra, cihaz yeniden kilitlense bile erişilebilir.
- F0-04'te gerçek cihazda ölçülecek.
- Kaynak: https://developer.apple.com/documentation/foundation/fileprotectiontype/completeuntilfirstuserauthentication

### 1.10 StoreKit 2 — BELİRSİZ (bu turda okunmadı)
- Grace Period ve App Store Server Notifications V2 ayrıntıları F0-13 kapsamında ayrıca doğrulanacak.

---

## 2. DÜZELTME — iOS 27 cihaz uyumluluğu
Görev 001 raporundaki "iPhone 11 serisi düşebilir" bilgisi söylentiydi. Apple'ın resmî sayfasına göre iOS 27, **iPhone 11, 11 Pro, 11 Pro Max ve iPhone SE (2. nesil) ve sonrası** ile uyumludur.
- Kaynaklar: https://www.apple.com/os/ios/ • https://support.apple.com/en-us/128058

**İkinci cihaz önerisi değişmedi.** iPhone 11 / SE (2. nesil) ve sonrası güncel iOS testini karşılar; iPhone XS/XR yalnızca eski sürüm testleri içindir.

---

## 3. Bağımsız izleme servisleri — doğrulama

| Servis | Ücretsiz plan | Ücretsiz aralık | Ticari kullanım | Durum |
|---|---|---|---|---|
| UptimeRobot | 50 monitör | 5 dk | **İzinli** — kullanım koşulları (son güncelleme 26 Mayıs 2026) ticari kullanıma açıkça izin veriyor | DOĞRULANDI |
| Better Stack | 10 monitör | 3 dk (ücretli planda 30 sn) | — | DOĞRULANDI (resmî belge) |
| HetrixTools | 15 uptime monitörü | **1 dk** | Kısıt bildirilmemiş | DOĞRULANDI (HetrixTools'un kendi sayfası); fiyat sayfası okunamadı |

**Sonuç:** Şartnamedeki 60 sn hedefine en yakın ücretsiz seçenek HetrixTools (1 dk). Üçüncü taraf kaynaklara göre bu planda e-posta dışı SMS kredisi yok ve hesabın düzenli olarak giriş yapılarak aktif tutulması gerekiyor (**BELİRSİZ**). Hesap açılmadı.

Kaynaklar:
- https://uptimerobot.com/pricing.md • https://uptimerobot.com/terms/
- https://betterstack.com/docs/uptime/check-frequency/
- https://hetrixtools.com/uptimerobot-alternative/ • https://hetrixtools.com/feature/website-monitor/

---

## 4. Ürün direktörüne bildirilecek yeni teknik noktalar
1. **Yeniden başlatma sonrası bölge izleme:** İlk kilit açılışına kadar güvenli bölge olayı alınamaz. Bu bir ürün kararı değildir; mevcut kurallar (M05-04, M05 madde 9) zaten karşılıyor. Kullanıcı metninde doğru durum gösterilmelidir.
2. **App Attest için geçici geliştirme App ID'si:** F0-05 için gerekir; proje sahibi onayına bağlıdır.
3. **`CLServiceSession` iOS 17 uyumu:** BELİRSİZ; Faz 1 öncesi doğrulanacak.
