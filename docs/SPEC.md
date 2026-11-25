# FAMILYGUARD — V1.1 NİHAİ ÜRÜN ŞARTNAMESİ

**Şartname sürümü:** V1.1 — Revizyon 4 / ONAYLI ÜRÜN BAZ ÇİZGİSİ
**Hedef uygulama sürümü:** V1.0 (iOS)
**Tarih:** 25 Kasım 2026
**Hazırlayan:** Claude (birleştirme) • **Denetim:** ChatGPT (ürün direktörü) • **Nihai onay:** proje sahibi
**Kaynak:** Orijinal şartname v1.0 (24 Kasım 2026) + Karar 01–14 + marka ek kararları 10-A, 10-B, 10-D, 10-E + Nihai Şartname Denetimi (25 Kasım 2026)
**Kod adı:** FamilyGuard (ticari yayın adı değildir, bkz. Bölüm 2)
**Ürün direktörü onayı:** VERİLDİ • **Nihai şartname denetimi:** TAMAMLANDI • **Ürün kapsamı:** KİLİTLENDİ
**Bekleyenler:** Marka seçimi (proje sahibi) • Faz 0 teknik fizibilite • Hukuki uygunluk • Faz D tasarım • App Store yayın onayı verilmedi
**Nihai bütçe, marka ve proje başlangıç onayı:** Proje sahibine aittir.
**Kodlama durumu:** Üretim kodlamasına başlanmayacaktır.

---

## 0. BELGENİN KULLANIMI

1. Bu belge ürün kuralları için **tek geçerli kaynaktır**. Geliştirme başladığında `docs/SPEC.md` olarak saklanır.
2. Karar 01–14 ve marka ek kararları (10-A, 10-B, 10-D, 10-E) yalnızca `docs/DECISIONS.md` içinde tarihsel kayıt olarak tutulur ve bağımsız talimat kaynağı olarak kullanılmaz.
3. Yürürlükten kalkmış kurallar bu belgeye alınmamıştır. Hangi eski kuralların neden çıkarıldığı Bölüm 18'de listelenmiştir.
4. Etiketler:
   - **[KESİN]**: Onaylanmış kural.
   - **[PARAMETRE]**: Başlangıç değeri; Faz 0 veya pilot ölçümüyle kesinleşecek.
   - **[BELİRSİZ]**: Doğrulanmamış teknik veya ticari bilgi.
   - **[HUKUK]**: Uzman hukuk görüşüne bağlı kural.
   - **[KARAR GEREKLİ]**: Ürün direktörünün kararını bekleyen çelişki veya boşluk. Revizyon 3 itibarıyla açık konu yoktur (Bölüm 18.C).
5. Etiketsiz maddeler [KESİN] kabul edilir.
6. **Terim ayrımı:** "Faz 0 … Faz 10, Faz D" geliştirme aşamalarıdır. "P0 / P1 / P2" yalnızca test önem seviyeleridir. Eski kararlarda geçen "P0 ölçümü / P0 kabul kriteri" ifadeleri bu belgede "Faz 0 ölçümü" ve ilgili modül testleri olarak yeniden adlandırılmıştır.

---

## 1. ÜRÜN TANIMI VE TEMEL İLKELER

### 1.1 Ürün
Ebeveyn, çocuk ve yetişkin aile üyesi rollerini tek uygulamada birleştiren; açık izinle konum paylaşımı, güvenli bölgeler, SOS ve temel aile güvenliği sunan, reklamsız bir aile güvenliği uygulamasıdır.

### 1.2 Değişmez ürün ilkeleri
1. Eski veri hiçbir zaman güncel konum gibi gösterilmez. Konumun ne zaman ölçüldüğü ve ne kadar doğru olduğu her zaman görünür.
2. Gönderilemeyen yardım talebi gönderilmiş, görülmeyen bildirim görülmüş, eski konum güncel olarak gösterilmez.
3. Temel güvenlik özellikleri ticari nedenlerle sınırlandırılmaz. Ürün yardım isteme hakkını değil, gelişmiş aile yönetimini satar.
4. Ürün, ailelerin güvenlik endişesini abonelik satmak için kullanmaz. Korkutucu satış metni kullanılmaz.
5. Gizli takip, görünmez takip veya habersiz eşleştirme modu geliştirilmez.
6. Hiçbir ebeveyn, yönetici veya abonelik sahibi kendisine tanımlanmamış kişisel veriye erişim hakkı elde etmez. Abonelik, aile üyelerinin verileri üzerinde mülkiyet hakkı vermez.
7. Konum verisi reklam, pazarlama veya satış amacıyla kullanılmaz. Reklam SDK'sı ve reklam profillemesi bulunmaz.
8. Ürünün ticari hedefleri çocukların kişisel verilerinin korunmasından ve proje sahibinin hukuki güvenliğinden üstün tutulmaz.
9. Uygulama resmî acil yardım hizmetlerinin yerine geçmez; otomatik polis veya ambulans çağırmaz.
10. V1 her şeyi yapan bir uygulama değildir. Temel işlevleri güvenilir, güvenli, anlaşılır ve sürdürülebilir biçimde yapan bir uygulamadır.
11. Uçtan uca şifreleme uygulanmamıştır ve pazarlamada iddia edilmez.
12. Önce karar, sonra tasarım, ardından uygulama ve kalite kontrol.

---

## 2. MARKA VE KİMLİK

### 2.1 Mevcut durum (Karar 10, 10-D, 10-E)
1. "FamilyGuard" yalnızca iç proje kod adıdır; bu adla ticari yayın yapılmaz.
2. **Koşullu birinci aday:** Wingfold. Doğrudan aile güvenliği uygulaması çakışması bulunamamıştır. Ancak ABD'de Sınıf 36'da (finansal danışmanlık) "WINGFOLD" başvurusu (seri no. 99124965) ve İspanya'da "Wingfold España" adıyla pazarlama/web hizmeti bulunduğundan tamamen temiz sayılmaz.
3. **Koşullu yedek aday:** Eavely. UK'de Sınıf 30'da (gıda) başvuru vardır; "Everly" ile sesli karışma riski taşır.
4. Elenen adlar yeniden önerilmez (liste `docs/DECISIONS.md` içinde tutulur).
5. Nihai marka seçimi proje sahibine aittir.
6. Resmî marka incelemesi (TÜRKPATENT, EUIPO, USPTO, WIPO; Sınıf 9, 42, 45 başlangıç) tamamlanmadan hukuki uygunluk garantisi verilmez. [HUKUK]
7. Dünyanın hiçbir sektöründe kullanılmamış bir isim bulma zorunluluğu yoktur. Öncelikli risk aynı veya benzer sektördeki çakışmalardır.
8. Marka incelemesi nihai şartnamenin onayını bekletmez.

### 2.2 Marka ilkeleri
- Korku değil güven, gözetleme değil aile bağı, karmaşa değil huzur.
- Resmî acil yardım kurumu veya kamu güvenlik hizmeti izlenimi verilmez.
- Uygulamanın işlevi App Store alt başlığı ve açıklamalarla anlatılır; marka adında "Family, Kids, GPS, Tracker, Guard" zorunlu değildir.
- 21 dilde olumsuz anlam taşımamalıdır (seçilen ad için dil kontrolü yapılacaktır). [BELİRSİZ]

### 2.3 Geliştirici markası ve web altyapısı
1. VDOX Lab geliştirici markasıdır; şirket değildir. Uygulama adı ile geliştirici markası ayrıdır.
2. Hukuki belgelerde ve sağlayıcı yazışmalarında veri sorumlusunun resmî adı ve bireysel geliştirici statüsü kullanılır. [HUKUK]
3. **Uygulamaya özel alan adı (.com, .app vb.) satın alınmaz.** Ürün sayfası, gizlilik politikası, kullanım koşulları, destek sayfası ve Universal Links VDOX Lab web altyapısı üzerinde (alt sayfa veya alt alan adı) barındırılır.
4. Alan adı durumu marka değerlendirmesinde kriter değildir.

### 2.3.1 Destek altyapısı (Karar 12-E, Karar 13-B)
1. Destek adresi: `info@vdoxlab.com` (VDOX Lab uygulamalarının mevcut genel iletişim adresi). `support@vdoxlab.com` oluşturulmaz.
2. Adresin aktif çalıştığı yayından önce gönderme ve alma testleriyle doğrulanır. Uygulama içi destek ekranında, App Store kayıtlarında ve VDOX Lab ürün sayfalarında yalnızca doğrulanmış adres kullanılır.
3. Talepler ürün bazında sınıflandırılır.
4. Gizlilik ve kişisel veri talepleri ayrı iş akışıyla yönetilir.
5. Destek taleplerinde çocukların konum bilgisi, şifre veya oturum tokenı istenmez.
6. E-posta üzerinden acil yardım sağlandığı izlenimi verilmez; destek hizmetinin 7/24 canlı acil müdahale merkezi olmadığı açıkça yazılır.
7. Gizlilik politikası, kullanım koşulları, destek ve hesap silme sayfaları VDOX Lab web altyapısında oluşturulur. Kesin adres ve bağlantılar yayın hazırlığından önce doğrulanır.

### 2.4 Marka kesinleşmeden oluşturulmayacak kalıcı kayıtlar
Production Bundle ID, App Store Connect uygulama kaydı, Android paket adı, Google Play kaydı, Production Supabase projesi, marka sosyal medya hesapları, production abonelik ürün kimlikleri ve nihai logo/ikon/mağaza metinleri.
- Sentetik veriyle yapılacak fizibilite için geçici geliştirme kimlikleri kullanılabilir; bunlar marka seçimini kısıtlamaz.
- Mimari, görünen adın sonradan değişmesi teknik kimliklerin değişmesini gerektirmeyecek biçimde kurulur.

---

## 3. PLATFORM VE TEKNOLOJİ

| Konu | Kural |
|---|---|
| V1 istemci | Native iOS, Swift + SwiftUI, minimum iOS 17 |
| Yeni API'ler | iOS 17 alternatifi ve availability kontrolü olmadan kullanılmaz |
| Harita | Apple MapKit + Core Location; ücretli üçüncü taraf harita zorunlu değildir |
| Sunucu | Supabase (Auth, Postgres + RLS, Realtime Private Broadcast, Edge Functions); platformdan bağımsız |
| Barındırma | Mevcut VDOX Lab Pro organizasyonunda ayrı proje; pilotta ayrı Pro organizasyon açılmaz. Frankfurt bölgesi değerlendirilmektedir [HUKUK] |
| Bildirim | APNs (V1), FCM (V1.5) |
| Abonelik | StoreKit 2 + sunucu doğrulaması; ücretli abonelik yönetim servisi (RevenueCat vb.) kullanılmaz |
| Android | V1.5: Kotlin + Jetpack Compose, ortak sunucu ve ortak aile hesapları |
| Dil | 21 dil mimarisi ilk günden; pilot TR/EN |

- Underworld ve Brain Lab projelerinin altyapı ayarları izinsiz değiştirilmez.
- Supabase Pro organizasyonunun kota ve fatura bilgileri henüz hesap erişimiyle doğrulanmamıştır. [BELİRSİZ]

---

## 4. ROLLER VE YETKİLER

| Rol | Yetkiler | Sınırlar |
|---|---|---|
| Ebeveyn / aile yöneticisi | Aile kurma, yetişkin daveti, çocuk profili oluşturma ve eşleştirme, cihaz yönetimi, güvenli bölgeler, bildirim tercihleri, abonelik satın alma | Rol seçimi tek başına velayet kanıtı değildir. Başka yetişkinin konum iznini açamaz. |
| Çocuk | SOS, beni almaya gel, güvendeyim, hazır yanıtlar, kendi güvenlik ekranı | Kendi rolünü yükseltemez; aile oluşturamaz; başka üyeyi yönetemez; satın alma yapamaz; başkalarının konumunu yalnızca tanımlı paylaşım kapsamında görür. |
| Yetişkin aile üyesi | Davet kabulü, gönüllü konum paylaşımı, SOS, yardım ve temel güvenlik | Diğer yetişkin üzerinde ebeveyn kontrolü yoktur. |

Üyelik kuralları:
1. V1'de bir kişi aynı anda tek aktif aileye üye olur.
2. Üye sayısına ödeme sahibi dahildir; cihazlar ayrı üye sayılmaz.
3. Yönetici devri yeniden doğrulama gerektirir.
4. Roller ve yetkiler sunucuda tutulur; istemcinin gönderdiği rol veya düzenlenebilir metadata yetki kaynağı değildir.
5. Uygulamadaki aile, Apple Family Sharing grubu değildir.
6. Aile yöneticisi yetkisi otomatik olarak hukuki veli yetkisi oluşturmaz. Çocuk verilerine erişim ve çocuk cihazı yönetimi için ayrıca doğrulanmış veli ilişkisi ve gerekli yetkilendirme aranır. [HUKUK]

---

## 5. V1 KAPSAMI — SEKİZ MODÜL

V1 bu sekiz modülle sınırlıdır. Kapsam kilidi için bkz. Bölüm 15.

### MODÜL 01 — HESAP, AİLE VE CİHAZ GÜVENLİĞİ

**Hesap ve davet**
1. Yetişkin hesap açar, aile oluşturur ve paylaşım açıklamasını okur. E-posta doğrulaması hesap sahipliğini kanıtlar, veli doğrulaması değildir.
2. Yetişkin daveti tek kullanımlıktır, 15 dakika geçerlidir; tüketim ve deneme sınırı sunucuda uygulanır.
3. Davet oluşturma ve kullanma oran sınırına tabidir.

**Çocuk profili**
4. Çocuktan e-posta veya şifre istenmez. Tam doğum tarihi varsayılan olarak toplanmaz.
5. Profili yalnızca doğrulanmış ve yetkili ebeveyn veya yasal veli oluşturur. [HUKUK: veli doğrulama yöntemi]
6. Profilde yalnızca şunlar bulunur: benzersiz profil kimliği, görünen ad veya takma ad, yaş aralığı, isteğe bağlı hazır avatar, veli ilişkisi, paylaşım ve cihaz durumu.
7. Gerçek ad soyad, fotoğraf, okul adı, kimlik numarası ve açık adres istenmez.
8. Yaş aralıkları ve hukuki yaş sınırları uzman görüşüyle kesinleşir. [HUKUK]
9. Çocuk ve ebeveyn hesapları teknik olarak ayrı kimliklerdir; çocuk cihazında ebeveynin giriş bilgisi kullanılmaz.

**QR ve manuel eşleştirme**
10. QR kod tek kullanımlıktır, 15 dakika geçerlidir; içeriği kriptografik olarak güvenli, tahmin edilemeyen bir anahtardır.
11. QR içinde çocuk adı, aile kimliği, konum, telefon veya oturum bilgisi bulunmaz.
12. Süre sunucu saatiyle doğrulanır; eşleştirme atomiktir; ikinci kullanım reddedilir; yeni kod öncekini iptal eder; ebeveyn istediği an iptal edebilir.
13. Manuel kod: en az 8 karakter, karıştırılabilecek karakterler yok, biçim örneği `K7MX-4QPR`, kriptografik rastgele, 15 dakika, tek kullanımlık, başlangıçta 5 başarısız denemede iptal [PARAMETRE]; kod, hesap, cihaz ve bağlantı düzeyinde oran sınırı.
14. Manuel eşleştirme QR ile aynı güvenlik ve onay kurallarına tabidir.

**Çift taraflı onay**
15. Kodun taranması konum paylaşımını başlatmaz.
16. Çocuk cihazı hangi aileye ve hangi veliye bağlanacağını yaşa uygun biçimde gösterir ve açıkça onaylar.
17. Ebeveyn cihazı yeni cihaz talebini gösterir; ebeveyn doğruladıktan sonra eşleştirme tamamlanır. İki cihazda kısa doğrulama bilgisi gösterilebilir.
18. iOS izinleri eşleştirmeden sonra ayrı aşamalarda istenir. Eşleştirme onayı işletim sistemi iznini veya yasal veli doğrulamasını yerine geçmez.
19. Hukuki izinler ve yaşa uygun bilgilendirme tamamlanmadan düzenli konum paylaşımı başlamaz. [HUKUK]

**Anonim oturum mimarisi**
20. Çocuk için Supabase Anonymous Auth kullanılabilir. Anonim oturum doğrulanmış eşleştirmeden sonra çocuk profiline bağlanır.
21. Eşleştirilmemiş anonim oturum hiçbir aile verisine erişemez, konum gönderemez, aile kanalına bağlanamaz.
22. Anonim kullanıcıların `authenticated` rolüyle işlem yapabildiği dikkate alınır; bu rol tek başına erişim için yeterli sayılmaz. Bütün hassas RLS politikaları aktif profil, aile üyeliği ve cihaz yetkisini doğrular.
23. Anonim oturum açma kötüye kullanıma karşı sınırlandırılır; gerekirse CAPTCHA veya cihaz doğrulaması kullanılır.
24. Eşleştirilmemiş ve 24 saatten eski anonim hesaplar güvenli temizleme işiyle silinir; eşleştirilmiş çocuk hesapları etkilenmez.

**Cihaz güvenliği**
25. V1'de her çocuk profiline aynı anda bir aktif telefon bağlanır.
26. Oturum bilgileri Keychain'de saklanır; erişim sınıfı arka plan görevleriyle uyumlu seçilir. UserDefaults veya şifresiz dosya kullanılmaz.
27. Gereksiz kalıcı donanım tanımlayıcıları toplanmaz. Cihaz kimliği tek başına kimlik doğrulama değildir.
28. Keychain kullanmak oturumun kriptografik olarak cihaza bağlandığı anlamına gelmez. App Attest veya uygun cihaz doğrulaması Faz 0'da değerlendirilir. [BELİRSİZ]
29. Cihaz kaydında işletim sistemi, uygulama sürümü, eşleştirme zamanı, oturum ilişkisi, yetki durumu ve push tokenı bulunabilir.

**Telefon değişikliği ve kayıp cihaz**
30. Telefon değişince yeni çocuk profili gerekmez; veli yeni eşleştirme kodu oluşturur.
31. Yeni eşleştirme tamamlanınca eski cihazın erişimi atomik olarak iptal edilir. Başarısız yeni eşleştirme mevcut cihazı devre dışı bırakmaz.
32. Ebeveyn panelinde: bağlı cihazı görüntüle, yeni cihaz eşleştir, kayıp/çalıntı cihazın erişimini kapat, eşleştirme talebini iptal et.
33. Cihaz iptali ebeveynin yeniden kimlik doğrulamasını gerektirir. İptalde aktif oturumlar, yenileme tokenları, push tokenı ve Realtime erişimi kaldırılır; sonradan gelen konum kayıtları reddedilir.
34. Yeni cihaz eşleştirmesi üye kapasitesini veya yeni üye hakkını tüketmez.
35. Çevrimdışı cihazda daha önce gösterilmiş verilerin uzaktan anında silineceği vaat edilmez; cihazdaki hassas aile verisi asgaride tutulur.

**JWT ve anlık erişim iptali**
36. Erişim tokenlarının oturum iptalinden sonra süresi dolana kadar kullanılabileceği dikkate alınır; yalnızca oturumu kapatmak yeterli sayılmaz.
37. Konum yükleme, SOS, aile verisi, geçmiş ve güvenlik ayarlarında aktif cihaz yetkisi sunucuda doğrulanır (gerekirse `session_id` ve cihaz yetki kaydı birlikte).
38. Realtime yetkisi yalnızca ilk bağlantıda kontrol edilmez. Gerekirse aile kanalının güvenlik sürümü değiştirilerek eski kanala yeni veri gönderilmesi engellenir.

**Çocuk güvenlik ekranı**
39. Çocuk modunda şu bilgiler gösterilir: bağlı olduğu aile, konumunu kimlerin görebildiği, düzenli paylaşım durumu, güvenli bölge izleme durumu, konum izni durumu, bağlı cihaz, acil kişiler, güvenlik ve gizlilik yardımı.
40. Çocuğun bilgisi dışında yeni konum izleyicisi eklenmez; yeni izleyici eklendiğinde yaşa uygun bildirim yapılır.
41. Çocuk kendini güvende hissetmediğinde yardım isteyebilir; ebeveyn kontrolü kötüye kullanım bildirmeyi engellemez.
42. Çocuk modunda korkutucu, suçlayıcı veya cezalandırıcı uyarı kullanılmaz.

**Yetişkin hesabına dönüşüm**
43. Çocuk profili ileride bağımsız yetişkin hesabına dönüştürülebilir. Geçiş yalnızca istemcinin değiştirdiği yaşa dayanmaz.
44. Geçişte eski ebeveyn yetkileri otomatik devam etmez ve sunucuda kaldırılır. Konum paylaşımı ve aile üyeliği kişinin kendi tercihine bağlıdır. Geçiş ebeveynin abonelik kararına bağlı değildir.
45. Doğrulama yöntemi ve geçmiş verilerin durumu uzman görüşüyle kesinleşir. [HUKUK]

**Ekonomi kuralı:** Profil oluşturma, eşleştirme, cihaz iptali, telefon değiştirme ve kayıp cihaz kurtarma ücretsizdir; ücretli SMS doğrulama servisi zorunlu değildir.

### MODÜL 02 — ADAPTİF KONUM MOTORU

**Profiller (V1)**
1. V1'de üç profil vardır: Dinlenme, Normal Hareket, SOS. Yolculuk profili V1.1'e taşınmıştır.
2. Normal Hareket: yaklaşık 100 m istenen hassasiyet, 150–200 m kayıt mesafesi. [PARAMETRE]
3. Zaman tabanlı "her 2–5 dakikada bir" garantisi yoktur. Güncellemeler hareket ve mesafeye bağlıdır.
4. Hareketsizken düşük enerjili servislere geçilir. Kalkış bölgesi, significant-change ve uygun olduğunda Visits servisleri değerlendirilir.
5. Otomatik duraklatmadan sonra standart servislerin kendiliğinden yeniden başlayacağı varsayılmaz. Hareket algılanınca Normal profili yeniden başlatan bir durum makinesi kurulur. GPS sapmalarının sık profil değişikliğine yol açması engellenir.
6. SOS profili daha yüksek hassasiyet kullanır, süreli olarak çalışır ve sonunda normal politikaya döner. Azami çalışma süresi Faz 0'da ölçülerek kesinleşir [PARAMETRE]. Süresiz yüksek hassasiyetli GPS çalıştırılmaz.
7. Harita açılması karşı cihazın güncelleme sıklığını artırmaz.

**Ölçüm sözleşmesi**
8. Ölçüm zamanı, sunucu kabul zamanı, yatay doğruluk, cihaz kimliği, izin durumu ve pil ölçüm zamanı ayrı saklanır.
9. Konum yaşı sunucuya ulaşma saatine göre değil, cihazın ölçüm zamanına göre hesaplanır.
10. Geç gelen ölçüm geçmişe yazılır; daha yeni bir son konumu geriye götürmez. Gelecek tarihli veya saat sapmalı kayıt "zaman doğrulanamıyor" olarak işaretlenir.
11. Çevrimdışı konum kuyruğu en fazla 24 saat tutulur; süresi geçen kayıt yüklenmez. Kuyruk tekilleştirilir.
12. Konum güncellenmemesi kişinin hareketsiz, güvende veya tehlikede olduğunun kanıtı sayılmaz.

**Ayrı tutulan zaman bilgileri (Karar 12-A)**
- Son başarılı GPS ölçümü.
- Son doğrulanmış hareket bilgisi.
- Son doğrulanmış hareketsizlik bilgisi.
- Son başarılı sunucu iletişimi.
- Son konum izni durumu.

**Tazelik kuralları**
1. Sabit 10 dakikalık eskime kuralı bütün profillere uygulanmaz. Dinlenme, Normal Hareket ve SOS profillerinin tazelik eşikleri Faz 0 gerçek cihaz ölçümleriyle belirlenir. [PARAMETRE]
2. Yeni GPS ölçümü yoksa ölçüm zamanı güncellenmez. Sunucu iletişiminin sürmesi konumun güncel olduğunu tek başına kanıtlamaz. Hareket algılanmaması kişinin kesinlikle aynı yerde olduğunun kanıtı sayılmaz.
3. Yeni ölçüm yokken eski konum güncel konum olarak gösterilmez. Yanlış "güncel konum" gösterimi P0 yayın engelidir.
4. Hareketsiz cihazlar yalnızca eski konum uyarısını önlemek için sürekli GPS ölçümüne zorlanmaz. Haritayı açan ebeveyn diğer cihazda zorunlu GPS ölçümü tetiklemez.
5. Örnek kullanıcı metinleri:
   - "Son konum ölçümü 35 dakika önce."
   - "Son hareket bilgisi 3 dakika önce: hareket algılanmadı."

**Durum metinleri** (eşikler Faz 0'da kesinleşir)

| Durum | Kullanıcı metni |
|---|---|
| Güncel ölçüm | "45 sn önce • ±25 m" |
| Yaklaşık / düşük doğruluk | "7 dk önce • yaklaşık konum" |
| Eski ölçüm | "Son konum ölçümü X önce alındı. Cihazın güncel durumu bilinmiyor." |
| Eski ölçüm + yeni hareketsizlik bilgisi | "Son konum ölçümü X önce. Son hareket bilgisi Y önce: hareket algılanmadı." |
| Bilinmiyor | "Konum alınamadı" |
| Paylaşım kapalı | "Paylaşım durduruldu" + son teyit saati |

**İzin ve bağlantı durumları**
13. "Paylaşımı durdurma" ile "işletim sistemi iznini kapatma" ayrı durumlardır.
14. Hassas konum kapatılınca: "Yaklaşık konum paylaşılıyor. Konum doğruluğu sınırlı olabilir."
15. Arka plan izni kaldırılınca: "Arka plan konum paylaşımı aktif değil."
16. İzin tamamen kapalıysa (doğrulanmışsa): "Konum izni kapalı."
17. Uygulamanın silindiği doğrulanamıyorsa "Uygulama silindi" denmez. Cihazın kapandığı, internetin kesildiği veya paylaşımın bilerek durdurulduğu doğrulanmadan iddia edilmez.
18. İzin değişikliği anında iletilemezse bağlantı gelince güncellenir.
19. V1'de uygulamanın silinmesini veya izin değiştirilmesini engelleme vaadi verilmez.

**Pil yönetimi** [PARAMETRE]
20. Normal karma kullanımda 8 saatte en fazla 5 yüzde puan ek tüketim (uygulamasız tabana göre medyan).
21. Ağırlıklı hareketsiz kullanımda 8 saatte en fazla 2 yüzde puan.
22. SOS modunun tüketimi ayrı raporlanır.
23. Hassasiyet ve sıklık değerleri ölçülmeden garanti edilmez. Pil optimizasyonu SOS ve güvenlik bildirimlerini devre dışı bırakmaz.
24. Hedefler tutmazsa parametreler optimize edilip testler tekrarlanır. Güvenlik ile pil arasında çözülemeyen çelişki ürün direktörüne sunulur.

### MODÜL 03 — AİLE HARİTASI

1. Harita Apple MapKit ile gösterilir.
2. Harita açılınca yetkili üyelerin son konumları toplu sorguyla alınır.
3. Canlı akış yalnızca yetkili ve aktif izleyiciler için Private Broadcast ile sağlanır.
4. Aktif izleyiciler süreli `map_viewers` kayıtlarıyla yönetilir: başlangıç geçerliliği 120 saniye [PARAMETRE], yenileme aralığı Faz 0'da belirlenir, süre sunucu saatiyle doğrulanır.
5. Yetkili aktif izleyici varsa veritabanı tetikleyicisi `realtime.send()` ile Private Broadcast üretir. İzleyici yoksa hiç konum Broadcast mesajı üretilmez; kontrol sunucuda yapılır.
6. Konum tabloları Postgres Changes ile yayınlanmaz. Presence kullanılmaz.
7. İzleyici oturumu uygulama arka plana geçince, harita kapanınca veya süre dolunca sonlanır. Süresi dolmuş kayıtlar otomatik temizlenir.
8. Yeniden bağlanınca son konum tekrar sorgulanır; kaybolan mesajlar yüzünden eski konum yenisinin üzerine yazılmaz.
9. Aileden çıkarılan veya yetkisi kaldırılan kullanıcının açık canlı oturumları da sonlandırılır.
10. Arayüzde "kesintisiz canlı konum" vaadi kullanılmaz.
11. Her işarette ölçüm zamanı, konum yaşı ve doğruluk bilgisi bulunur.
12. Aktif düzenli konum profili sınırı: ücretsiz 3, Premium 10.
13. Düzenli paylaşımı aktif olmayan üyeler aile listesinde kalır, ancak haritada eski konum işaretleri gösterilmez. Metin: "Düzenli konum paylaşımı aktif değil. Acil yardım ve temel güvenlik özellikleri kullanılabilir."
14. "Konum izni kapalı" ile "abonelik kapasitesi nedeniyle paylaşım durdu" farklı gösterilir.
15. Konum geçmişi: ücretsiz 24 saat, Premium 30 gün (aktif konum profilleri için).
16. Aktif SOS sırasında izin verilen son konum ölçüm zamanı ve doğrulukla gösterilir; SOS bitince geçici erişim politika gereği sona erer.

### MODÜL 04 — SOS VE ACİL YARDIM

**Çalışma mekanizması**
1. SOS bütün kullanıcılar için ücretsizdir; acil ekranlarda satın alma teklifi veya reklam bulunmaz.
2. SOS başlatılınca sunucuya olay kaydı gönderilir. Yeni GPS ölçümü beklenmez; son bilinen konum, ölçüm zamanı ve doğrulukla kullanılır. Aynı anda yeni ölçüm başlatılır ve elde edilirse kayıt güncellenir.
3. Düzenli konum paylaşımı kapalı olan üye de SOS başlatabilir; mevcut izinler kapsamında yeni ölçüm hemen başlar.
4. Konum yoksa SOS konumsuz gönderilir. Konum izni kapalıyken de SOS çalışır.
5. Kullanıcı sunucu yanıtını beklemeden SMS veya arama seçeneklerini kullanabilir.
6. Sunucudan 10 saniye içinde onay gelmezse SMS yedeği belirgin gösterilir [PARAMETRE]. Cihaz çevrimdışıysa beklemeden yedek seçenekler sunulur.
7. Başarısız SOS hiçbir koşulda başarılı gösterilmez.
8. SOS tetikleme yöntemi (basılı tutma, kısa iptal penceresi vb.) gerçek cihazlarda karşılaştırılarak seçilir. Yardımı gereksiz geciktiren çok aşamalı onay kullanılmaz. [PARAMETRE]

**SOS ekranı seçenekleri**
9. "Aileme SOS gönder", "SMS ile yardım iste", "Acil durum kişisini ara", "Yerel acil yardım numarasını ara".
10. Ekranda uygulamanın resmî acil yardım hizmetlerinin yerine geçmediği açıkça yazılır.

**SMS yedeği**
11. Apple MessageUI kullanılır; SMS otomatik gönderilmez, kullanıcı onaylar. Ücretli SMS API'si kullanılmaz.
12. İçerik: yardım isteyen üyenin adı, yardım talebi, son bilinen konum bağlantısı, ölçüm tarihi ve saati, varsa doğruluk, eski konumsa açık uyarı. Konum yoksa uydurma koordinat yerine "konum alınamadı" yazılır.
13. Konum bağlantısı uygulama sunucusuna bağlı değildir; iOS, Android ve tarayıcılarla uyumlu Google Maps bağlantısı kullanılır. Bağlantının açılmasıyla konumun Google ile paylaşılabileceği gizlilik değerlendirmesine dahildir.
14. Cihaz ve operatör SMS desteği kontrol edilir; operatör ücreti olabileceği belirtilir.
15. SMS ekranının "gönderildi" sonucu alıcının mesajı aldığı veya okuduğu anlamına gelmez. İptal edilen SMS gönderilmiş gösterilmez.

**Acil kişiler ve aramalar**
16. En fazla 5 acil durum kişisi; ücretsiz.
17. Cihazda şifreli saklanır, çevrimdışı erişilebilir, sunucuyla senkronize olur; silinen kişiler ve çıkış/eşleştirme kaldırma sonrası yerel kayıtlar temizlenir.
18. Bekleyen SOS kuyruğu ve acil kişiler için "Complete Until First User Authentication" veri koruma sınıfı değerlendirilir; yeniden başlatma sonrası ilk kilit açılmadan erişilemeyebileceği dikkate alınır. Gerçek cihazda doğrulanır. [BELİRSİZ]
19. Aramalar işletim sisteminin onay mekanizmalarıyla başlar; arka planda otomatik arama yapılmaz.
20. Yerel acil numaralar doğrulanmış ülke tablosuyla yönetilir (Türkiye: 112). Ülke, uygulama diline veya cihaz bölge ayarına göre kesin kabul edilmez; son doğrulanmış ülke cihazda saklanır; belirsiz veya eskiyse kullanıcıya doğrulatılır ya da ülke seçtirilir. Yanlış ülke varsayımıyla numara gösterilmez.

**Kesinti, kuyruk ve tekilleştirme**
21. Sunucuya ulaşamayan SOS cihazdaki güvenli bekleyen işlemler kuyruğuna alınır. Bağlantı gelince yalnızca geçerlilik süresi dolmamış, aktif ve iptal edilmemiş SOS otomatik gönderilir (madde 26–30). Yanıtı alınamamış olayın sunucu durumu idempotent olarak doğrulanır. İptal ile gönderim eşzamanlı gerçekleşirse iptal edilmiş olay yeniden aktif hale getirilemez.
22. Her SOS benzersiz kimlik taşır; tekrar denemeler mükerrer olay üretmez. İlk oluşturulma zamanı korunur. Gecikmeli gelen SOS'un gerçek saati açıkça gösterilir.
23. Kullanıcının iptal ettiği veya sonlandırdığı SOS hiçbir koşulda yeniden gönderilmez.

**Çevrimdışı SOS kuyruğu (Karar 12-B)**
24. SOS başlatıldığı anda yerel olay kimliği oluşturulur; gerçek oluşturulma zamanı korunur.
25. İnternet yoksa SMS ve arama seçenekleri hemen gösterilir; SOS'un henüz sunucuya ulaşmadığı açıkça bildirilir.
26. Bekleyen SOS'un başlangıç geçerlilik süresi 15 dakikadır. [PARAMETRE: Faz 0'da güvenlik ve kullanılabilirlik açısından değerlendirilir]
27. Süre içinde bağlantı gelirse aktif ve iptal edilmemiş SOS otomatik gönderilir; gerçek oluşturulma zamanı ve gönderim gecikmesi kaydedilir ve gösterilir.
28. Süresi dolan ve sunucuya hiç ulaşmamış SOS otomatik gönderilmez. Uygulama açıldığında şu seçenekler sunulur: "Önceki yardım talebiniz gönderilemedi. Hâlâ yardıma ihtiyacınız var mı?" → Yeni SOS gönder / Talebi kapat / SMS gönder / Telefonla ara.
29. Yeni SOS ayrı olay kimliğiyle oluşturulur. Süresi dolan yerel SOS ile sunucuda kayıtlı aktif SOS birbirine karıştırılmaz; sunucudaki aktif SOS yalnızca yerel kuyruk süresi doldu diye kapatılmaz.
30. Sunucuya ulaşmış fakat yanıtı istemciye gelmemiş olaylar idempotent sorgulamayla doğrulanır.

**SOS durumları** (ayrı ayrı gösterilir, doğrulanamayan teslimat bilgisi gösterilmez)
Sunucuya gönderiliyor → Sunucu tarafından kaydedildi → Bildirim sağlayıcısına iletildi → Aile üyesi tarafından görüldü → Aile üyesi yardım talebini onayladı • Gönderilemedi • Sonlandırıldı.
- Push sağlayıcısının bildirimi kabul etmesi, kullanıcının aldığı veya gördüğü anlamına gelmez.

**Bildirim önceliği**
31. SOS bildirimleri iOS Time Sensitive önceliğiyle gönderilir. Time Sensitive sessiz modu aşmaz ve kullanıcı ayarlarına bağlıdır.
32. Critical Alerts yetkisi için başvuru yapılır; Apple'ın onaylayacağı varsayılmaz. Bu yetki yayın için zorunlu değildir. Yetki yoksa sessiz mod veya Odak modunun aşılacağı vaat edilmez.
33. SOS dışındaki rutin bildirimlerde gereksiz yüksek öncelik kullanılmaz.

**Bağımsız sunucu izleme**
34. Supabase dışında çalışan bağımsız izleme servisi kullanılır; hedef kontrol aralığı 60 saniyedir [PARAMETRE]. Önce ücretsiz çözümler denenir; yetersizse ek maliyet ürün direktörüne sunulur.
35. Yalnızca HTTP yanıtı değil, veritabanı erişimi, SOS kayıt mekanizması ve bildirim kuyruğu da kontrol edilir. İzleme testleri gerçek kullanıcılara SOS göndermez.
36. Kritik arızada proje sahibine bağımsız bildirim, ikinci kanal olarak e-posta gönderilir; arıza başlangıcı, süresi ve düzelmesi kaydedilir; düzelme bildirimi gönderilir.
37. İzleme kayıtlarında kişisel veri bulunmaz. İzleme, 7/24 müdahale veya kesintisiz hizmet garantisi olarak pazarlanmaz.

### MODÜL 05 — GÜVENLİ BÖLGELER

1. Bölge türleri: ev, okul, iş yeri ve özel bölgeler; giriş ve çıkış bildirimi.
2. Kapasite: ücretsiz 2, Premium 18 kullanıcı bölgesi (aile toplamı, üye başına değil).
3. Sistem rezervleri: 1 otomatik kalkış algılama bölgesi + 1 yolculuk varış rezervi. V1'de yolculuk rezervi kullanılmaz.
4. Cihaz başına aktif izleme koşulu hiçbir durumda 20'yi geçmez (iOS sınırı; CLMonitor değerlendirilir).
5. Başlangıç yarıçapı 150–300 m; küçük bölgelerde doğruluk uyarısı. [PARAMETRE]
6. Sınırdaki GPS sıçramaları için doğruluk filtresi ve mümkünse 60–120 saniye kalış veya ikinci ölçüm kullanılır. Arka planda ikinci ölçüm alınamazsa "olası giriş" veya "doğrulanamadı" gösterilir. Yetersiz doğrulukta kesin varış bildirilmez. [PARAMETRE]
7. Bölge kayıt hataları gizlenmez; aktif olmayan bölgeler aktif gibi gösterilmez.
8. Düzenli paylaşımı kapalı üyede bölge izleme de durur. Panel metni: "Bu üye için güvenli bölge bildirimleri aktif değil."
9. Bildirim gelmemesi kişinin bölgede olduğunun kanıtı sayılmaz.

### MODÜL 06 — TEMEL AİLE GÜVENLİĞİ

Bu modüldeki bütün özellikler ücretsizdir, abonelikten bağımsızdır ve düzenli konum profili kapasitesini tüketmez. Düzenli konum paylaşımı kapalı üyeler de kullanabilir (Karar 12-C).

1. **Güvendeyim:** Kullanıcı beyanı ve saat paylaşılır. Konum eklemek zorunlu değildir; kullanıcı isterse mevcut izinler kapsamında tek seferlik konum ekleyebilir. Bu seçenek varsayılan olarak kapalıdır. Konum eklenmemesi bildirimi engellemez. Bildirim sürekli takibi yeniden başlatmaz, güvenliğin sistemce doğrulandığı anlamına gelmez; beyan zamanı korunur.
2. **Beni almaya gel:** Temel yardım talebi sayılır ve bütün yetkili üyelere ücretsizdir. Akış: istek + (izin varsa) konum → bir yetişkin kabul eder (ilk kabul atomik) → yolda → buluşuldu / iptal. Konum alınamaması talebi engellemez. Konum yalnızca ilgili olay ve yetkili alıcılarla paylaşılır; talep bitince veya iptal edilince geçici erişim sona erer. V1'de rota hesaplama, sürekli yolculuk takibi veya otomatik varış tahmini yoktur.
3. **Yardım isteğini kabul etme:** Kabul ve onay kayıtları ayrı tutulur.
4. **Hazır yanıtlar** (yalnızca ilgili güvenlik/yardım olayına bağlı): "Yoldayım", "Geliyorum", "Tamam", "Güvendeyim", "Yardım talebini gördüm", "Seni almaya geliyorum". Serbest sohbet V1'de yoktur.
5. **Düşük pil bildirimi:** Başlangıç eşiği %20'dir [PARAMETRE]. Aynı düşük pil olayı için tekrar tekrar bildirim gönderilmez. Pil bilgisi zaman damgalıdır; son ölçüm zamanı gerektiğinde gösterilir. Paylaşımı kapalı üyelerde de işletim sisteminin izin verdiği ölçüde çalışır. Bunun için GPS motoru yeniden başlatılmaz ve yalnızca pil kontrolü amacıyla arka plan işi oluşturulmaz. iOS uygulamayı çalıştırmadığında anlık algılama garanti edilmez. Pil paylaşımı ayrı güvenlik ve gizlilik tercihine bağlıdır.
6. **Konum izni durumu** ve **son cihaz bağlantısı bilgisi** gösterilir.

### MODÜL 07 — ABONELİK VE EKONOMİ

**Paket ve satın alma yetkisi**
1. Tek Premium aile paketi vardır: aylık 5,99 USD, yıllık 39,99 USD; yerel mağaza fiyatları ülkeye göre belirlenir.
2. Uygulama tamamen reklamsızdır.
3. Satın alma yalnızca yetişkin aile yöneticisine açıktır; çocuk modunda satın alma ekranı yoktur.
4. App Store Connect'te bu abonelik için Apple Family Sharing kapalıdır ve ürün direktörünün yeni kararı olmadan açılmaz. Premium hakları yalnızca doğrulanmış aile üyeliklerine dağıtılır.

**Mükerrer satın almayı önleme**
5. Satın alma ekranı açılmadan önce ailenin Premium durumu sunucudan doğrulanır; aile zaten Premium ise satın alma düğmesi gösterilmez; yöneticilere aboneliği yöneten kişi ve mağaza gösterilir.
6. Sunucuya ulaşılamıyorsa yeni satın alma başlatılmaz; geri yükleme desteklenir.
7. Satın alma öncesinde sunucuda aileye özel, süreli satın alma rezervasyonu oluşturulur; başarısız veya iptal edilmiş işlemden sonra kaldırılır. Askıda kalan mağaza işlemi rezervasyon süresi bitti diye geçersiz sayılmaz; gecikmeli tamamlanan satın alma ayrıca işlenir.
8. Sunucu önlemlerinin mağaza düzeyindeki bütün mükerrer satın alımları engelleyeceği varsayılmaz.

**Çift satın alma olursa**
9. İki işlem de doğrulanıp kaydedilir; kullanıcıdan gizlenmez; aileye çift hak veya ek kapasite verilmez; mükerrer abonelik bildirilir ve ayrı destek olay türüyle kaydedilir.
10. Yönetim için `showManageSubscriptions`, iade için `beginRefundRequest` kullanılır. Web bağlantıları yalnızca bunlar kullanılamazsa yedektir:
    - https://apps.apple.com/account/subscriptions
    - https://reportaproblem.apple.com
11. İptalin otomatik iade olmadığı açıklanır; iadenin onaylanacağı garanti edilmez. Bir işlemin iadesi diğer geçerli aboneliğin haklarını kaldırmaz.

**Üye değişikliği ve kötüye kullanım**
12. Premium ailede en fazla 10 aktif üye bulunur.
13. 30 günlük hareketli dönemde en fazla 5 farklı yeni üye eklenebilir [PARAMETRE]; ilk kurulumda 10 kapasitenin dolmasını engellemez. Daha önce doğrulanmış üyenin yeniden katılması yeni hak tüketmez. Yeni hesaplarla döndürme engellenir.
14. Sınır cihaz veya telefon değişikliğine uygulanmaz.
15. Şüpheli döndürmede otomatik kalıcı hesap kapatma yapılmaz; boşanma, velayet değişikliği, yeni üye veya bakım sorumluluğu için güvenli destek istisnası bulunur. Bu istisna paylaşım izinlerini veya katılım onaylarını geçersiz kılmaz.
16. Üye sınırının dolması mevcut üyelerin güvenliğini etkilemez.

**Satın alanın aileden ayrılması**
17. Mağaza aboneliğinin sahibi satın alan yetişkindir. Satın alma kaydı ile aileye verilen Premium hakkı ayrı veri yapılarında tutulur. Bir abonelik aynı anda tek aileye hak sağlar.
18. Ayrılmadan önce etkileri gösterilir. Ayrılma hakkı ticari gerekçelerle engellenmez. Eski aile geçerli Premium hakkını kaybederse, ortak yıllık geçiş hakkı kullanılmamışsa 7 günlük ürün geçişi başlar; hak kullanılmışsa aile hemen ücretsiz pakete düşer (madde 29–31). Bu sürede eski ailenin yöneticisi yeni abonelik alabilir. Ailenin başka geçerli Premium aboneliği varsa geçiş başlatılmaz. Ayrılıp yeniden katılmak hakkı sıfırlamaz. 7 günlük geçiş, ayrılan kişiye eski ailenin verilerine erişim yetkisi vermez.
19. Satın alan aboneliğini yeni ailesine bağlayabilir; aile değiştirme için 30 günlük bekleme vardır [PARAMETRE]; gerçek aile değişiklikleri için destek istisnası bulunur. Aynı aboneliğin sürekli aileler arasında döndürülmesi engellenir.
20. Satın alan ayrıldığı anda eski ailenin konum ve özel bilgilerine erişimini kaybeder; abonelik yönetim erişimi korunur.

**Hesap silme**
21. Hesap silmek mağaza aboneliğini iptal etmez; bu açıkça yazılır ve mağaza yönetimi seçeneği sunulur. Aktif abonelik hesap silmeyi engellemez.
22. Silmeden sonra yalnızca hukuki, finansal ve mağaza doğrulaması için zorunlu asgari işlem kayıtları tutulur. Geçerli satın almalar geri yüklenebilir, ancak eski aileye veya silinmiş verilere erişim sağlamaz.

**İptal, iade ve ödeme sorunları**
23. Otomatik yenilemenin iptali hakkı hemen bitirmez; ücretli dönem sonuna kadar kullanılır.
24. İade, iptal ve hak geri alma doğrulanmış mağaza durumuna göre gecikmeden uygulanır.
25. Mağaza Billing Grace Period'u (değerlendirilip uygun yapılandırılır) ile uygulamanın 7 günlük geçiş süresi ayrı kavramlardır. Uygulama doğrulanmamış abonelik süresi üretmez.
26. Normal Premium bitişinden önce bildirim gönderilir.
27. Abonelik durumundaki hiçbir değişiklik SOS, SMS ve acil arama erişimini kaldırmaz.

**Premium sona erdiğinde (güvenli düşürme)**
28. Aile silinmez; hiçbir üye otomatik çıkarılmaz (geçiş hakkı olmasa bile); 10 kişiye kadar mevcut üyeler kalır. Ücretsiz 3 üye sınırının üzerindeki aileye kapasite uygun olana kadar yeni üye eklenemez.

**7 günlük ürün geçiş hakkı (Karar 12-D, Karar 13-A)**
29. Tek bir ortak geçiş hakkı vardır ve aile bazındadır: bir aile 365 günlük hareketli dönemde en fazla bir kez kullanabilir [PARAMETRE: pilot sonrası yeniden değerlendirilebilir]. Normal bitiş, ödeme başarısızlığı sonrası kesin bitiş ve abonelik sahibinin ayrılması aynı haktan düşer; her olay için ayrı hak oluşmaz. Yönetici, cihaz veya abonelik sahibi değişikliği, ayrılıp yeniden katılma ve yeni satın alma hakkı sıfırlamaz. Başlamış geçiş, ikinci bir geçişle uzatılamaz. Ailenin başka geçerli Premium aboneliği varsa geçiş başlamaz. Hakkın tüketilmesi ve abonelik durumunun güncellenmesi sunucuda atomik ve idempotent yapılır; mükerrer olaylar yeni hak oluşturmaz.
30. Tetikleyiciler:

| Durum | Davranış |
|---|---|
| Normal abonelik iptali | Ödenmiş dönem sonuna kadar Premium sürer; dönem bitince uygun ailede 7 günlük geçiş başlar |
| Ödeme başarısızlığı | Mağazanın doğrulanmış Billing Grace Period'u varsa mağaza hakkı korunur; mağaza hakkı bitmeden geçiş başlamaz; hak kesin olarak bitince uygun ailede geçiş uygulanabilir |
| İade veya mağaza hak geri alması | Doğrulanmış mağaza kararı uygulanır; otomatik geçiş oluşturulmaz |
| Sahte satın alma veya kötüye kullanım | Geçersiz hak kaldırılır; geçiş oluşturulmaz; temel ücretsiz güvenlik korunur |
| Abonelik sahibinin aileden ayrılması (aile Premium hakkını kaybederse) | Ortak hak kullanılmamışsa 7 günlük geçiş; kullanılmışsa doğrudan ücretsiz paket (madde 18) |
| Aynı anda birden fazla tetikleyici (ör. normal bitiş + ayrılma) | Tek geçiş; ikinci hak tüketilmez, süre uzamaz |

31. Geçiş hakkı olmayan aile doğrudan ücretsiz pakete düşer.
32. Billing Grace Period ile ürün geçişi teknik ve görsel olarak ayrıdır. Ürün geçişi mağaza aboneliğinin uzatıldığı anlamına gelmez.
33. Geçiş sırasında yeniden geçerli Premium alınırsa hak doğru şekilde etkinleşir.
34. Yönetici ücretsizde aktif kalacak 3 konum profilini ve 2 güvenli bölgeyi Premium kullanırken önceden veya geçiş süresi içinde seçebilir.
35. Bitiş ve hak hesaplamaları sunucu otoritesinde yapılır.
**Ücretsiz pakete düşüş**
36. Seçim yapılmazsa önceden gösterilen deterministik varsayılan sıralama uygulanır (çocuk profillerine öncelik verilmesi değerlendirilir; aynı öncelikte ailenin sıralaması geçerlidir); sonuç yöneticiye bildirilir.
37. Yönetici seçimi kullanıcıların paylaşım izinlerini geçersiz kılmaz; izni olmayan kişi için takip başlatılamaz; kişinin paylaşımı sonlandırma hakkı korunur.
38. Geçiş bitince (veya geçiş hakkı yoksa hemen) yalnızca seçilen 3 profilin düzenli paylaşımı sürer. Diğerlerinin üyeliği ve temel güvenlik hakları korunur; düzenli paylaşımları, geçmiş güncellemeleri ve bölge izlemeleri durur.
39. Bitişten önce başlamış SOS yarıda kesilmez.
40. Geçiş süresinin bitmesi yeni ücret oluşturmaz.
41. Ücretsiz pakette 30 günlük hareketli dönemde en fazla 2 gönüllü aktif profil değişikliği yapılabilir [PARAMETRE]. Geçiş içindeki değişiklikler, aileden ayrılma, izin kaldırma, telefon değiştirme ve güvenlik kaynaklı değişiklikler (destek istisnası) bu sınıra dahil değildir. Sınır SOS ve acil iletişimi etkilemez.
42. Konum geçmişi saklama politikasına göre temizlenir; gizli Premium arşivi tutulmaz. Premium yeniden alınınca silinmiş geçmiş geri gelmez, izinler yeniden doğrulanır, kullanıcının kapattığı paylaşım kendiliğinden başlamaz.
43. Abonelik bitişi çocuğun telefonunu kullanılmaz hale getirmez.
44. Bildirim zamanlaması: bitişten önce mümkünse hatırlatma; geçiş başlangıcında yeni kapasite açıklaması; geçişin bitmesinden 24 saat önce hatırlatma; paylaşımı duracak üyelere durum bildirimi (push içeriğinde isim veya konum yok).

**Satın alma ekranı bilgilendirmesi** (satın almadan önce gösterilir)
10 kişiye kadar düzenli konum paylaşımı • Premium bitince 7 günlük geçiş (aile başına 365 günde bir kez; iade ve hak geri almada uygulanmaz) • Geçiş sonunda 3 aktif profil • Ücretsiz 2 güvenli bölge • Mevcut üyelerin grupta kalması • Temel güvenliğin ücretsiz devam etmesi.
- Ekranda yalnızca mevcut (yayınlanmış) özellikler gösterilir; V1.1, V1.5 ve V2 özellikleri Premium avantajı olarak sunulmaz.

**Sunucu tarafı doğrulama**
45. StoreKit 2; sunucu tarafında satın alma doğrulaması; App Store Server Notifications V2 (imzalar doğrulanır); `appAccountToken` ile hesap ilişkisi.
46. İşlem kimlikleri benzersiz saklanır; aynı işlem birden fazla hesaba veya aileye bağlanamaz. İstemciden gelen Premium bilgisi tek başına güvenilir sayılmaz.
47. Mükerrer bildirimler sonucu tekrar üretmez; gecikmeli ve sıra dışı bildirimler desteklenir; bildirimlerin anında geleceği varsayılmaz; periyodik mutabakat yapılır; açılışta ve geri yüklemede durum yeniden doğrulanabilir.
48. Abonelik durumu sunucu otoritesindedir; hak değişiklikleri atomik veritabanı işlemleriyle korunur; Sandbox ve Production kayıtları ayrılır.
49. Abonelik doğrulama servisi kesintisinde mevcut haklar güvenli biçimde korunur.

### MODÜL 08 — GİZLİLİK VE HUKUKİ UYGUNLUK

**Hukuki süreç** [HUKUK]
1. KVKK ve uluslararası veri aktarımı uzmanı avukattan görüş alınır; maliyet proje sahibinin bütçe onayına sunulur.
2. Hukuki inceleme tamamlanmadan gerçek çocuk veya aile verisi üretim altyapısına aktarılmaz. Sentetik konum ve hayalî hesaplarla teknik prototipe izin verilir. Gerçek cihaz testlerindeki veri işleme yöntemi ayrıca değerlendirilir.
3. Nihai veri barındırma kararı hukuki görüş olmadan kesinleşmez. Hukuki uygunluk, gerçek kullanıcı pilotunun ve ticari yayının zorunlu kabul kriteridir.

**Supabase ve sınır ötesi aktarım** [HUKUK]
4. Supabase'e KVKK standart sözleşmesini (Kurul'un yayımladığı metin, zorunlu hükümler değiştirilmeden) imzalayıp imzalamayacağı yazılı sorulur. Taraflar ve sözleşme türü hukuk uzmanıyla doğrulanır.
5. Standart sözleşme kullanılırsa 5 iş günü içindeki Kurum bildirimi yapılır; kimin yaptığı ve belgeleri kaydedilir.
6. Supabase GDPR DPA'sının tek başına KVKK uyumu sağladığı varsayılmaz. Alt işleyenler, yedek konumları, destek erişimi ve sonraki aktarımlar incelenir. Yazılı cevap gelmeden imzalayacağı varsayılmaz.
7. İmzalanmazsa seçenekler: A) Türkiye yayınını ertelemek, B) Türkiye'de barındırılan ayrı/alternatif altyapı, C) avukatın önereceği başka hukuka uygun mekanizma. Türkiye pazarından şu aşamada vazgeçilmez. Türkiye dışı pilot KVKK yükümlülüklerini kaldırmaz. Türkiye'de sunucu olsa bile bildirim, analiz ve destek hizmetlerinin aktarım riski incelenir.
8. Supabase destek talebinin İngilizce metni `docs/PRIVACY.md` içinde tutulur. İmza satırı Karar 06 gereği veri sorumlusunun resmî adı ve bireysel geliştirici statüsüyle güncellenir.

**Uluslararası yayın**
9. 21 dil desteği bütün ülkelerde yayın anlamına gelmez; ülkeler hukuki uygunluğa göre ayrı ayrı açılır.
10. Türkiye için KVKK, AB için GDPR (DPA tek başına uyum değildir), ABD için COPPA ve uygulanabilir çocuk gizliliği düzenlemeleri incelenir. Gizlilik politikaları, ebeveyn bilgilendirmeleri ve sözleşmeler pazara göre uyarlanır; gerekirse yaş ve ülke bazlı kayıt sınırı uygulanır. Uygunluğu doğrulanmamış ülkede ticari yayın yapılmaz.

**Çocukların gizliliği**
11. Çocuk konum verisi yüksek hassasiyetli kişisel veri olarak ele alınır. KVKK m. 6 anlamında otomatik olarak özel nitelikli sayılmaz; sınıflandırmayı uzman yapar. [HUKUK]
12. Ebeveyn yetkilendirme ve velayet doğrulama süreçleri tasarlanır; çocuğa yaşına uygun gizlilik bilgilendirmesi sunulur.
13. Yetişkinlerin paylaşımı kendi açık ve bilgilendirilmiş tercihidir. Aile içinde olmak bütün üyelerin konumuna koşulsuz erişim vermez; SOS konumu yalnızca ilgili ve yetkili alıcılarla paylaşılır.
14. Yetkisiz ebeveyn erişimi, velayet anlaşmazlığı, aile içi şiddet ve takip amaçlı kötüye kullanım senaryoları tehdit modeline dahildir.
15. Destek ekibi rutin olarak konum göremez; istisnai erişim gerekçeli, süreli ve denetlenebilir olur.

**Veri saklama ve silme** [PARAMETRE]

| Veri | Politika |
|---|---|
| Konum geçmişi | Ücretsiz 24 saat, Premium 30 gün. Süre dolunca API erişimi hemen kesilir; fiziksel temizlik en geç 24 saat içinde. Son konum da süresiz tutulmaz. |
| Konum içeren olay kopyaları | Aynı saklama sınırına tabidir; yardım talebi konumları amaçla sınırlı saklanır. |
| Çevrimdışı konum kuyruğu | Azami 24 saat; süresi geçen kayıt yüklenmez. |
| Hesap silme | Uygulama içinden başlatılır; oturum ve paylaşım erişimi hemen iptal; aktif kişisel veriler 7 gün içinde silinir; zorunlu işlem kayıtları gerekçeli ve asgari tutulur. |
| Aileden ayrılma | Ayrılan kişinin eski aile verilerine erişimi hemen kaldırılır. Ayrılma bağımsız kullanıcı hesabının silinmesi anlamına gelmez. Eski aile ilişkisindeki verilerin saklama ve silme politikası hukuki değerlendirmeye tabidir. [HUKUK] |
| Geçici yardım olayı konumları (SOS, Beni almaya gel, Güvendeyim) | Erişim olay bitince veya iptal edilince sona erer; azami erişim ve saklama süresi Faz 0'da kesinleşir [PARAMETRE]. Süresiz olay konumu erişimi oluşturulmaz. |
| Yedekler | Pro günlük yedekleri 7 gün saklanır [BELİRSİZ]; silinen verinin yedeklerden doğal sona erdiği açıklanır; geri yüklemede silme kayıtları yeniden uygulanır; "anında tüm yedeklerden silindi" denmez. |
| Tanılama | Ham konum, çocuk adı, token ve mesaj içeriği loga girmez; kişisel olmayan tanılama 30 gün; güvenlik olayları gerekçeli ayrı süre. |
| Eşleştirilmemiş anonim hesaplar | 24 saat sonra silinir. |

**Veri güvenliği**
16. Bütün aktarımlar TLS ile yapılır; sağlayıcı şifrelemesi ve erişim yapılandırması yayından önce doğrulanır.
17. Bütün hassas tablolarda RLS zorunludur; aileler arası erişim engellenir; yönetici erişimi sınırlı ve denetlenir.
18. `service_role` veya ayrıcalıklı anahtar uygulamaya gömülmez.
19. Kişisel veri ihlali müdahale prosedürü, veri işleme envanteri, üçüncü taraf listesi ve gerekirse veri koruma etki değerlendirmesi hazırlanır.
20. App Store gizlilik beyanı gerçek veri toplama davranışıyla eşleşir. Çocuklara yönelik mağaza kategorisi seçimi ayrıca değerlendirilir. [HUKUK]
21. Gereksiz kişisel veri toplanmaz.

---

## 6. BİLDİRİM POLİTİKASI

1. APNs (ve V1.5'te FCM) bildirimlerinde şunlar bulunmaz: çocuğun veya üyenin adı, telefon, açık adres, GPS koordinatı, okul veya ev adı, konum geçmişi, sağlık bilgisi, aile içi mesaj içeriği, doğrudan kişiyi tanımlayan hesap bilgisi.
2. Yalnızca olay kategorisi, genel metin ve gerekirse kişiyi tanımlamayan olay referansı gönderilir; ayrıntılar uygulama açılınca kimlik doğrulama ve yetki kontrolüyle alınır.
3. Bildirim tokenları da kişisel veri değerlendirmesine dahildir. Anonimleştirme aktarım yükümlülüklerini ortadan kaldırmaz.
4. Kilit ekranında konum veya kimlik bilgisi gösterilmez.
5. Sessiz push sürekli GPS uyandırma yöntemi değildir ve teslimi garanti edilmez.
6. Standart metinler (Türkçe kaynak; 21 dilde insan kontrolü zorunlu):
   - SOS: "Acil yardım talebi var. Ayrıntıları görmek için uygulamayı açın."
   - Güvenli bölge: "Yeni bir güvenli bölge bildiriminiz var."
   - Yardım isteği: "Bir aile üyeniz yardım istiyor."
   - Düşük pil: "Bir aile cihazının pil seviyesi düşük."
   - (V1.1) Yolculuk: "Takip ettiğiniz yolculukla ilgili yeni bir bildirim var."
   - (V1.1) Günlük durum: "Bir aile durum kontrolü bekliyor."
7. Kritik olaylar kalıcı kaydedilir ve push kuyruğuyla işlenir; başarısızlıklarda tekrar deneme ve mükerrer önleme vardır. Kalıcı olay kaydı doğruluk kaynağıdır; push ve Realtime yardımcı kanallardır.

---

## 7. TEKNİK MİMARİ

### 7.1 Veri yolu
```
iPhone → Supabase Auth + yetkili API → Postgres/RLS → olay kuyruğu → APNs
Aile haritası ← yetkili son konum sorgusu + harita açıkken Private Broadcast
```

### 7.2 Veri grupları (asgari)

| Grup | İçerik ve kural |
|---|---|
| profiles / families / memberships | Kullanıcı, aile, rol, aktiflik, ilişki onayı; yetki sunucu kaydından hesaplanır |
| devices / sharing_consents | Cihaz, push tokenı, paylaşım tercihleri, izin sürümü ve zamanları; token erişimi kısıtlı |
| pairing_codes | QR/manuel anahtar, süre, deneme sayacı, tüketim durumu |
| latest_locations / location_history | Ayrı yapılar; ölçüm ve alım zamanı, doğruluk; aile ve kullanıcı indeksleri; geçmiş zamana göre bölümlenebilir |
| map_viewers | Süreli aktif izleyici kayıtları (sunucu saatiyle) |
| zones | Bölge yapılandırması, aktiflik, kayıt hatası durumu |
| events / acknowledgements | Benzersiz olay kimliği, gerçek olay zamanı, alıcılar, ayrı teyit durumları |
| pickups | Durum makinesi, atomik kabul, iptal nedeni |
| emergency_contacts | En fazla 5, şifreli, senkronize |
| purchases / entitlements / purchase_reservations | Satın alma kaydı ile aile hakkı ayrı; işlem kimliği benzersiz; Sandbox/Production ayrımı |
| audit_log | Üyelik, davet, cihaz, abonelik değişiklikleri; hassas koordinat içermez |

(Journeys ve daily_checks V1.1'dedir.)

### 7.3 Erişim kuralları
- Konum okuma: aktif aile üyeliği + ilgili paylaşım yetkisi + aktif cihaz yetkisi.
- Konum yazma: yalnızca kendi cihazı adına, geçerli aile ilişkisi ve yetkili cihazla.
- Aile değiştirme, rol yükseltme, davet tüketimi ve abonelik bağlama sunucuda doğrulanır.
- Realtime kanalları aynı yetki modelini izler; Private Broadcast RLS ile korunur.
- Aktif düzenli paylaşım kapsamı dışındaki üyeler için düzenli takip kapsamında arka plan GPS durdurulur, geçmiş toplanmaz, Broadcast üretilmez. Kullanıcının başlattığı izinli SOS, Güvendeyim ve Beni almaya gel olaylarında amaçla sınırlı, geçici konum paylaşımı korunur; bu olaylar sürekli takibi yeniden başlatmaz.
- Düzenli paylaşımın kapatılması, cihazın iptal edilmesi veya aileden ayrılma sonrasında cihazda bekleyen konum kayıtları sunucu tarafından reddedilir.

### 7.4 Zamanlanmış sunucu işleri
Geçmiş temizliği, süresi dolmuş `map_viewers` temizliği, eşleştirilmemiş anonim hesap temizliği, bildirim tekrar denemeleri, abonelik mutabakatı, geçiş süresi bitişleri. Uygulamanın açık kalmasına bağlı görev oluşturulmaz.

### 7.5 Ölçüm ve maliyet kontrolü
- Broadcast gönderici ve alıcı mesajları, izleyici kontrol trafiği, veritabanı yazımları, Edge Function çağrıları, egress ve tepe bağlantılar ayrı ölçülür.
- Organizasyon kota ve harcama alarmları kurulur (öneri: %50 / %75 / %90). Otomatik maliyet kısıtlamalarının kritik güvenlik işlevlerine etkisi ayrıca değerlendirilir. Kritik güvenlik özellikleri maliyet gerekçesiyle kapatılmaz.
- Hata izleme anonim olay kimlikleri ve gecikme ölçümleriyle yapılır.

---

## 8. EKONOMİ

### 8.1 Paketler (V1 — güncel)

| Kapsam | Ücretsiz | Premium |
|---|---|---|
| Yeni ailede üye | 3 | 10 |
| Aktif düzenli konum profili | 3 | 10 |
| Güvenli bölge (aile toplamı) | 2 | 18 |
| Konum geçmişi | 24 saat | 30 gün |
| SOS, SMS yedeği, acil kişiler (5), acil arama | Dahil | Dahil |
| Güvendeyim, beni almaya gel, düşük pil, hazır yanıtlar | Dahil | Dahil |
| Güvenli eşleştirme, cihaz değiştirme ve kurtarma | Dahil | Dahil |
| Reklam | Yok | Yok |
| Fiyat | 0 | 5,99 USD/ay veya 39,99 USD/yıl |

- Premium'dan ücretsize geçen ailede 10 üyeye kadar aile ilişkisi korunur; düzenli paylaşım 3 profille sınırlanır.
- V1.1 ve V2 özellikleri yayınlandığında mevcut Premium abonelerine ek ücret alınmadan sunulması hedeflenir. Yeni paket veya fiyat değişikliği ayrı ürün kararı gerektirir.
- Kullanıcı henüz geliştirilmemiş bir özellik için ödeme yapmaya yönlendirilmez.

### 8.2 Altyapı maliyeti

**Referans tablo — eski model (Postgres Changes, her ölçüm 2 dinleyiciye):** Bu tablo yalnızca karşılaştırma içindir; güncel mimarinin maliyeti değildir.

| Aktif aile | 100 | 1.000 | 10.000 |
|---|---|---|---|
| Eski model aylık alt toplam (ortak kota boş) | 10 USD | 85 USD | 581 USD |
| Eski model (ortak kota tamamen dolu) | 15 USD | 97,50 USD | 593,50 USD |

- Varsayımlar: aile başına 2 paylaşan cihaz, cihaz başına günde 120 ölçüm, 30 gün.
- Supabase Pro organizasyon kotaları (Realtime 5 milyon mesaj, 500 tepe bağlantı, 250 GB çıkış, 10 USD compute kredisi) organizasyon genelinde paylaşılır; tepe bağlantılar proje bazında hesaplanıp toplanır. [BELİRSİZ: yayın öncesi yeniden kontrol]
- **Realtime %90 hedefi (Karar 12-F):** Realtime mesaj hacminde %90 azalma hedefi korunur, ancak P0 veya P1 yayın engeli değildir. Ölçülmeden garanti edilmiş tasarruf olarak gösterilmez. Mesaj azalması toplam Supabase faturasının aynı oranda azalacağı anlamına gelmez. Oran, aynı kullanıcı davranışı ve konum hacmine sahip karşılaştırılabilir referans modelle hesaplanır. Varsayımsal örnek: 10.000 ailede 581 USD → 268,25 USD.
- İzleyici yokken gereksiz Broadcast üretmeme kuralı ise zorunludur. Yanlış yetkilendirme, gereksiz Broadcast veya kontrolsüz maliyet ayrı teknik sorun sayılır. SOS ve güvenlik bildirimleri maliyet optimizasyonundan olumsuz etkilenmez.
- Ekonomi modeli sürdürülemez çıkarsa ürün direktörünün değerlendirmesi olmadan genel yayına geçilmez.
- Faz 0 ve Faz 8 raporlarında ölçülecekler: aile başına günlük konum kaydı ve Broadcast mesajı, aktif harita izleme süresi, izleyicisiz süre, eşzamanlı bağlantı, veritabanı işlem hacmi, veri transferi, push hacmi, ücretsiz ve Premium aile başına tahmini maliyet.
- Güncel mimari maliyeti 100 / 1.000 / 10.000 aile için Faz 0 ölçümleriyle yeniden hesaplanır. Ölçüm yapılmadan kesin bütçe kabul edilmez.
- Modelde 7 günlük geçişlerin ve düşürülmüş ailelerdeki pasif üyelerin maliyeti pilotta ayrıca ölçülür.

### 8.3 Gelir referansı
- Varsayım: ücretli ailelerin %60'ı yıllık, %40'ı aylık → aile başına brüt aylık eşdeğer 4,3955 USD.

| Ücretli aile | Brüt | %15 komisyon sonrası | %30 komisyon sonrası |
|---|---|---|---|
| 100 | 439,55 USD | 373,62 USD | 307,69 USD |
| 1.000 | 4.395,50 USD | 3.736,18 USD | 3.076,85 USD |
| 5.000 | 21.977,50 USD | 18.680,88 USD | 15.384,25 USD |

- %15 oranı Small Business Program kaydına ve uygunluğa bağlıdır. [BELİRSİZ]
- Eski modelde 85 USD altyapıyı karşılamak için yaklaşık 23 ücretli aile, 5.000 USD aylık eşdeğer gelir için yaklaşık 1.339 ücretli aile gerekir (%15 senaryosu). Bu eşikler yeni maliyet ölçümüyle güncellenir.
- Vergi, iade, kur, edinim, destek ve personel düşülmemiştir.

### 8.4 Ayrı bütçe kalemleri (teklif alınmadan fiyat atanmaz)
Hukuki danışmanlık ve mevzuat uyumu, marka tescili (TR/AB/ABD), insan kontrollü çeviri ve dil QA'sı, bağımsız izleme (ücretsiz yetmezse), e-posta teslim servisi, ek staging projesi, PITR/özel yedek, test cihazları, müşteri desteği, pazarlama.

### 8.5 Ölçülecekler
Aile başına ölçüm/mesaj/çıkış, pil etkisi, ücretsizden ücretliye dönüşüm, ücretli aile kaybı, destek talebi ve edinim maliyeti. Compute büyütme kararı CPU, bellek ve sorgu gecikmesi ölçümüne dayanır.

---

## 9. TASARIM

### 9.1 Tasarım öncelikli geliştirme
1. Ürün mekanikleri kesinleşmeden ekran tasarımına, tasarım sistemi onaylanmadan ekran kodlamasına başlanmaz.
2. Her ekranın görseli ve etkileşimleri kodlamadan önce onaylanır. Onaylanmamış hiçbir ekran kodlanmaz.
3. Claude tasarımı bağımsız olarak değiştirmez; teknik olarak uygulanamayan ayrıntıları gerekçesiyle raporlar.
4. Kişisel veri içermeyen teknik fizibilite prototipleri bu kuralın istisnasıdır; arayüzleri nihai ürün ekranı olarak kullanılmaz.
5. Faz 1–6 arasında geçici ürün arayüzü kodlanmaz; onaylı referanslar kullanılır. Faz 7'de ekranlar baştan tasarlanmaz.

### 9.2 Soft Premium görsel yön (Karar 10-D)

| Rol | Renk |
|---|---|
| Ana arka plan | #F8F6F1 |
| Ana koyu ton | #183D38 |
| Yardımcı yeşil | #A8C5B5 |
| Sıcak nötr | #E7D9C8 |
| SOS / acil | #C63838 |
| Metin / koyu yüzey | #222B29 |

- Açık ve koyu görünüm desteklenir.
- Kullanılmaz: altın çerçeve, metalik veya ağır doku, lacivert-altın, mermer, ipek görünümü.
- Ultra premium hissi korunur; ancak okunabilirlik ve kullanım kolaylığının önüne geçmez.
- Bu palet bir yön kararıdır; kontrast oranları tasarım sistemi aşamasında WCAG'e göre doğrulanır. [PARAMETRE]
- Marka adı kesinleşmeden logo, ikon ve nihai ekran tasarımı üretilmez.

### 9.3 Tasarım sistemi (kodlamadan önce)
Ana ve yardımcı renkler, açık/koyu görünüm, tipografi ölçeği, kart bileşenleri, ana/ikincil/acil düğmeler, alt navigasyon, form alanları, onay pencereleri, bildirim kartları, harita bilgi panelleri, durum göstergeleri, yükleniyor/boş/hata/çevrimdışı ekranları, animasyon ilkeleri, dokunsal geri bildirim, boşluk ve hizalama, köşe yuvarlaklıkları, kontrast, Dynamic Type, VoiceOver, sağdan sola düzen, küçük ve büyük iPhone uyumu.
- Değerler merkezi tasarım tokenlarıyla yönetilir.
- Güvenlik durumları yalnızca renkle anlatılmaz; metin ve simge desteği vardır.
- Kritik düğmeler Apple'ın erişilebilir dokunma alanı ilkelerine uyar.

### 9.4 Görsel varlıklar (marka kesinleşince)
Ana ve alternatif logo, 1024×1024 ikon, açılış ekranı, renk paleti, tipografi, ikon ailesi, harita işaretleri, üye avatarları, güvenlik durumu simgeleri, SOS ve Premium görsel kimliği, bildirim ikonları, boş durum illüstrasyonları, App Store görselleri.
- Hepsi tek tasarım ailesinden olur; uyumsuz hazır ikon setleri kullanılmaz; kullanım hakları kontrol edilir.
- Kodla çizilen görseller açıkça belirtilir ve onaysız olarak özel tasarlanmış varlıkların yerine kullanılmaz.

### 9.5 V1 ekran envanteri (başlangıç)
- **G01 Karşılama ve hesap:** açılış, karşılama, tanıtım, rol seçimi, ebeveyn hesabı, yetişkin girişi, hesap kurtarma, gizlilik bilgilendirmesi, konum ve bildirim izin rehberleri.
- **G02 Aile kurulumu:** aile oluşturma/katılma, yetişkin daveti, çocuk profili, QR gösterme/tarama, manuel eşleştirme, çift taraflı onay, başarılı/başarısız/süresi dolmuş eşleştirme, yeni cihaz, kayıp cihaz iptali.
- **G03 Ebeveyn ana ekranı:** aile haritası, üye listesi ve detay paneli, son konum, doğruluk, geçmiş, düşük pil, eski konum, bağlantı kesintisi, paylaşım kapalı, bölge izleme kapalı.
- **G04 Çocuk modu:** ana ekran, SOS, beni almaya gel, güvendeyim, acil kişiler, güvenlik ve gizlilik, "Konumumu kimler görebilir?", paylaşım ve izin durumu, hazır yanıtlar.
- **G05 SOS:** başlatma, gönderiliyor, konum alınıyor, kaydedildi, sağlayıcıya iletildi, görüldü, onaylandı, gönderilemedi, çevrimdışı, SMS yedeği, acil arama, gelen SOS, aktif yardım talebi, sonlandırma.
- **G06 Güvenli bölgeler:** liste, ekleme, haritadan seçim, yarıçap, ad ve simge, takip edilecek üyeler, bildirim tercihleri, düzenleme, silme, kapasite, izleme hatası.
- **G07 Temel aile güvenliği:** güvendeyim, alma isteği (gelen, kabul, iptal), hazır yanıtlar, güvenlik bildirimleri, olay geçmişi, düşük pil.
- **G08 Premium:** karşılaştırma, plan seçimi, satın alma, başarılı/başarısız, aile zaten Premium, mükerrer bilgilendirme, geri yükleme, yönetim, 7 günlük geçiş, 3 profil seçimi, 2 bölge seçimi, sona erme bilgilendirmesi.
- **G09 Ayarlar ve gizlilik:** profil, aile yönetimi, üye yetkileri, cihaz yönetimi, paylaşım tercihleri, bildirim ayarları, acil kişiler, dil, görünüm, gizlilik merkezi, veri ve hesap yönetimi, hesap silme, aileden ayrılma, yardım ve destek, yasal belgeler.
- Her madde ayrı ekran olmak zorunda değildir; durumlar varyant olabilir. Nihai envanteri ürün direktörü onaylar.

### 9.6 SOS tasarım kuralları
Kolay bulunur; tek elle kullanılır; yanlışlıkla tetikleme azaltılır; VoiceOver ve büyük yazıyla tamamlanabilir; durumlar açıkça ayrılır; konum alınamasa da çalışır; SMS ve arama kolay erişilir; reklam veya satın alma teklifi yoktur; resmî acil hizmetle fark yazılıdır; yalnızca estetikle onaylanmaz, gerçek cihaz kullanılabilirlik testi zorunludur.

### 9.7 Tasarım onay süreci
Mekanik tanımı → kullanıcı akışı → görsel tasarım → ürün direktörü değerlendirmesi → revizyon → proje sahibi görsel onayı → teknik uygulanabilirlik → tasarım kilidi → kodlama → tasarım ile kod karşılaştırması (ekran görüntüleriyle) → gerçek cihaz testi → kabul veya düzeltme.
- Her ekranın benzersiz referans kimliği ve onay durumu kaydedilir; güncel ve eski dosyalar ayrılır; kodlama ajanı yalnızca güncel ve onaylı referansları kullanır.

---

## 10. LOKALİZASYON

1. Lokalizasyon mimarisi Faz 1'den itibaren zorunludur; Swift String Catalog kullanılır.
2. Kullanıcıya görünen hiçbir metin koda sabit yazılmaz. Erişilebilirlik etiketleri, hata mesajları, bildirimler ve izin açıklamaları da dahildir.
3. Uygulama içinde sunucu metin değil olay kodu ve parametre gönderir; uygulama yerelleştirilmiş metni gösterir.
3a. Uygulama kapalıyken görüntülenen APNs bildirimleri ayrı ele alınır: APNs yerelleştirme anahtarları (loc-key) veya alıcının diline göre sunucuda seçilen güvenli yerelleştirilmiş metinler teknik olarak değerlendirilir. Her iki yöntemde de push içeriğine kişisel veri eklenmez. [BELİRSİZ, bkz. T-18]
4. Tarih, saat, mesafe, fiyat ve sayılar yerel biçimdedir. Çoğullar String Catalog ile yönetilir; kelime parçalarından cümle kurulmaz.
5. Sağdan sola düzen ilk günden desteklenir; uzun Almanca metinler ve Arapça düzen tasarım testlerine dahildir.
6. **21 dil:** Türkçe, İngilizce, Almanca, Fransızca, İspanyolca, İtalyanca, Portekizce (Brezilya), Felemenkçe, İsveççe, Norveççe, Danca, Fince, Lehçe, Çekçe, Romence, Yunanca, Rusça, Ukraynaca, Arapça, Japonca, Korece.
7. Pilot TR/EN baştan doldurulur; diğer 19 dil Faz 7'de tamamlanır; genel yayın 21 dildir.
8. SOS, güvenlik, izin, gizlilik ve abonelik metinleri 21 dilde yetkin insan kontrolünden geçer. Eksik güvenlik metni veya yanlış kritik çeviri yayın engelidir (P0).
9. 21 dil, 21 ülkede hukuken yayına hazır olunduğu anlamına gelmez.

---

## 11. SÜRÜM YOL HARİTASI

### V1.1 — İlk özellik güncellemesi (V1 yayınından ve gerçek kullanım verisinden sonra yeniden önceliklendirilir; tek güncellemede çıkması zorunlu değildir)
Güvenli yolculuk • planlı varış zamanı • gecikme hatırlatması (öneri: beklenen süreden 10 dk sonra) • yolculuk varış bölgesi (sistem rezervi) • yolculuk konum profili • günlük durum kontrolü (yerel saat, öneri: yanıtsızlıkta 15 dk sonra hatırlatma; yanıtsızlık "acil durum" sayılmaz; saat dilimi/yaz saati testi) • yaşlı aile bireyleri için planlı durum hatırlatmaları • genişletilmiş hazır mesajlar • serbest aile sohbeti (içerik güvenliği, engelleme, bildirme ve kötüye kullanım önlemleriyle) • gelişmiş aile iletişimi.

### V1.5 — Android
Kotlin, Jetpack Compose, ortak Supabase ve aile hesapları, platformlar arası abonelik (bir mağazadan alınan aile aboneliği diğer platformdaki üyelere de geçerli; yönetim satın alınan mağazada; ikinci ödeme zorlanmaz), Google Play Billing + Real-time Developer Notifications (durum Google Play Developer API ile doğrulanır), FCM, Android arka plan konum yönetimi, Google Play arka plan konum beyanı + tanıtım videosu + izin incelemesi, kişisel geliştirici hesabı için 12 test kullanıcısı / 14 gün kesintisiz kapalı test zorunluluğu, Android gerçek cihaz testleri.

### V2 — Dijital ebeveyn kontrolü
Family Controls, Device Activity, Managed Settings, ekran süresi, ders ve uyku modu, uygulama sınırlamaları, görev ve ödül sistemi.
- Apple yetkilendirmesine, hukuki uygunluğa ve işletim sistemi sınırlarına bağlıdır; Apple aile yapısı ve veli yetkilendirmesi doğrulanır.
- Ödül akışı: görev → çocuk tamamladı → ebeveyn onayladı → ödül süresi → cihazda uygulandı/bekliyor → tüketildi/süresi doldu. Onay ve kredi tek işlemde; çift onay ikinci ödül üretmez; çevrimdışı cihazda "uygulandı" denmez.
- Premium sona erme davranışı ayrı güvenlik kararıyla tanımlanır.
- V1'de V2 özelliklerinin çalıştığı izlenimi verilmez.

---

## 12. GELİŞTİRME SIRASI

**Hazırlık:** Karar birleştirme (bu belge) → çelişki denetimi → ürün direktörü onayı → kapsam kilidi → marka seçimi ve resmî marka kontrolü.

**Faz 0 — Teknik ve hukuki fizibilite:** Supabase standart sözleşme yazışması, hukuk uzmanı incelemesi, sentetik veriyle prototip, konum motoru fizibilitesi, pil ölçüm yöntemi, SOS ve çevrimdışı iletişim fizibilitesi, Critical Alerts başvuru hazırlığı, App Attest değerlendirmesi, iki gerçek iPhone test altyapısı, `map_viewers` yenileme aralığı ve maliyet ölçümleri.

**Faz D — Tasarım** (bağımlılıklar uygunsa Faz 0 ile paralel): marka görsel kimliği, logo ve ikon, tasarım sistemi, kullanıcı akışları, bütün V1 ekranları ve kritik durumlar, görsel varlıklar, erişilebilirlik tasarımı, SOS kullanılabilirlik değerlendirmesi, ürün direktörü ve proje sahibi onayı.

**Faz 1** Hesap, aile ve cihaz güvenliği • **Faz 2** Adaptif konum motoru ve aile haritası • **Faz 3** Güvenli bölgeler ve bildirimler • **Faz 4** SOS ve yedek iletişim • **Faz 5** Temel aile güvenliği • **Faz 6** StoreKit 2 ve abonelik • **Faz 7** Arayüz cilası, erişilebilirlik ve lokalizasyonun tamamlanması • **Faz 8** Güvenlik, gerçek cihaz ve yük testleri • **Faz 9** Hukuki yayın kontrolü ve TestFlight • **Faz 10** App Store yayın hazırlığı.

- Her faz kendi kabul kriterlerini tamamlamadan sonraki faza geçilmez.
- Teknik veya güvenlik nedenli tasarım değişiklikleri karar kaydıyla yapılır.

---

## 13. KABUL TESTLERİ

### 13.1 Önem seviyeleri
- **P0, kritik yayın engeli:** başarısız test sayısı sıfır olmalıdır. Kapsam: yetkisiz veri erişimi, çapraz aile erişimi, yetkisiz eşleştirme, rol yükseltme, iptal edilmiş cihazın erişimi, SOS'un sessizce başarısız olması, yanlış SOS başarı veya teslim bilgisi, SMS ve arama yedeğinin çalışmaması, eski konumun güncel gösterilmesi, kritik bölge hataları, abonelik yüzünden temel güvenliğin kapanması, veri silme ve saklama ihlali, hukuki uygunluğun tamamlanmaması, kritik güvenlik açığı, kritik metinlerin yanlış çevrilmesi.
- **P1, önemli yayın engeli:** temel akışların tamamlanamaması, hesap ve cihaz değiştirme hataları, abonelik hakkının yanlış hesaplanması, mükerrer satın alma hataları, tekrarlanan çökme, konum motorunun kabul edilemez performansı, pil hedeflerinin tutmaması, bölgelerin işlevsel olarak çalışmaması, konum ve izin durumlarının yanlış gösterilmesi, erişilebilirlik yüzünden güvenlik işlevlerinin kullanılamaması, yayın dillerinde kritik eksikler. Bir P1 kriterinin değiştirilmesi teknik gerekçe, risk analizi ve ürün direktörü onayı gerektirir. Güvenlik, hukuk ve temel işlev P1'leri keyfî ertelenmez.
- **P2, yayın sonrası iyileştirme:** kritik olmayan görsel kusurlar, küçük animasyonlar, ikincil ekran hizaları, güvenliği etkilemeyen performans, metin ve görünüm iyileştirmeleri. Gerekçeyle ertelenebilir.
- Başarısız bir P0 veya P1 testinin P2'ye düşürülmesi yasaktır. V1.1, V1.5 ve V2 testleri V1 başarısızlığı sayılmaz.
- Hedef kaçırıldığında gerekçe yazmak tek başına geçiş sağlamaz.

### 13.2 Test ortamı
En az iki gerçek iPhone (mümkünse biri eski nesil); iOS 17 ve lansmandaki güncel iOS; farklı pil sağlığı ve ağ koşulları. Her sonuç cihaz, işletim sistemi, izin ve ağ bilgisiyle `docs/QA/` altında kanıtlanır.

### 13.3 Test kataloğu

**M01 — Hesap, aile, cihaz (eski T01)**
| ID | Test | Seviye |
|---|---|---|
| M01-01 | A ve B aileleri arasında bütün okuma, yazma ve Realtime saldırı denemeleri reddedilir | P0 |
| M01-02 | Rol yükseltme yapılamaz; çocuk satın alma başlatamaz | P0 |
| M01-03 | Üye çıkarılınca yeni veri erişimi hemen kapanır (açık oturum ve kanal dahil) | P0 |
| M01-04 | Çocuk profili e-posta ve şifre olmadan oluşur; ebeveyn hesabından ayrıdır | P1 |
| M01-05 | QR içinde kişisel veri yok | P0 |
| M01-06 | Geçerli kod kabul; süresi dolmuş, kullanılmış ve iptal edilmiş kod reddedilir | P0 |
| M01-07 | Eşzamanlı kod tüketiminde tek işlem başarılı | P0 |
| M01-08 | Kaba kuvvet denemeleri engellenir; manuel kod 5 hatada iptal | P0 |
| M01-09 | Çift taraflı onay olmadan eşleştirme tamamlanamaz ve konum paylaşımı başlatılamaz | P0 |
| M01-10 | Eşleştirilmemiş anonim hesap veri göremez, konum gönderemez | P0 |
| M01-11 | Yetkisiz kişi profil oluşturamaz veya devralamaz | P0 |
| M01-12 | Yeni cihaz eşleştirmesi başarılı; eski cihazın erişimi iptal | P1 / P0 (iptal) |
| M01-13 | Eski cihaz süresi dolmamış JWT ile bile hassas veriye erişemez, konum gönderemez, yeni Broadcast alamaz, yeniden bağlanamaz | P0 |
| M01-14 | Başarısız cihaz değişikliği mevcut cihazı devre dışı bırakmaz | P1 |
| M01-15 | Telefon değişikliği üye kapasitesi tüketmez | P1 |
| M01-16 | Anonim hesap temizliği aktif çocuk hesaplarını silmez | P0 |
| M01-17 | Çocuk güvenlik ekranı konumu görebilenleri doğru listeler | P0 |
| M01-18 | Yetişkin hesabına dönüşte eski ebeveyn yetkileri kalkar | P0 |

**M02 — Konum motoru (eski T02, T03, T06)**
| ID | Test | Seviye |
|---|---|---|
| M02-01 | Tazelik eşikleri (Faz 0'da belirlenen) sınır değerlerde doğru; geç gelen ölçüm "güncel" olmaz; yeni ölçüm yokken ölçüm zamanı güncellenmez | P0 |
| M02-01b | Hareketsizlik bilgisi ile GPS ölçüm zamanı ayrı gösterilir; sunucu iletişimi konumu "güncel" yapmaz | P0 |
| M02-01c | Harita açılması diğer cihazda zorunlu GPS ölçümü tetiklemez | P1 |
| M02-02 | Saat sapması ve sıra dışı gönderim son konumu bozmaz | P0 |
| M02-03 | Uçak modu, konum reddi, yaklaşık konum, bildirim kapalı, düşük güç, zorla kapatma ve yeniden başlatmada sahte başarı yok | P0 |
| M02-04 | Ağ dönünce kuyruk tekilleşir; 24 saati geçen kayıt yüklenmez | P1 |
| M02-05 | Hareketsizden harekete geçiş; yürüyüş, araç ve uzun durgunluk senaryoları raporlanır | P1 |
| M02-06 | Hassas, arka plan ve tam izin kapatma durumları doğru gösterilir | P1 |
| M02-07 | Doğrulanmamış "uygulama silindi" bildirimi üretilmez | P1 |
| M02-08 | Pil: normal kullanımda 8 saatte ≤ 5 puan, hareketsizde ≤ 2 puan (medyan, tekrarlanabilir koşul) | P1 |
| M02-09 | SOS profilinden normal profile dönüş doğrulanır | P1 |
| M02-10 | Düzenli paylaşımı aktif olmayan profilden düzenli takip kapsamında konum toplanmaz; kullanıcının başlattığı izinli SOS, Güvendeyim ve Beni almaya gel konumları amaçla sınırlı gönderilir ve sürekli takibi başlatmaz | P0 |
| M02-11 | Paylaşım kapatıldıktan, cihaz iptal edildikten veya aileden ayrıldıktan sonra cihazda bekleyen konum kayıtları yüklenemez | P0 |
| M02-12 | SOS yüksek hassasiyet profili azami süre sonunda normal profile döner | P1 |

**M03 — Harita (Karar 02)**
| ID | Test | Seviye |
|---|---|---|
| M03-01 | Aktif ve süresi dolmamış yetkili izleyici kaydı yokken konum Broadcast mesajı: 0. Normal harita kapanışında izleyici kaydı hemen sonlanır; beklenmedik bağlantı kesilmesinde kayıt lease süresi dolunca sona erer | P1 |
| M03-01b | Yetki iptalinde canlı akış lease süresi beklenmeden hemen kesilir | P0 |
| M03-02 | Yetkisiz aile konumuna erişim: 0 | P0 |
| M03-03 | Realtime kesintisi ve yeniden bağlanma doğru çalışır | P1 |
| M03-04 | Eski konum yeni konumu ezmez | P0 |
| M03-05 | Yetkisi kaldırılmış kullanıcının canlı erişimi engellenir | P0 |
| M03-06 | Düzenli paylaşımı aktif olmayan profiller için düzenli takip Broadcast'i üretilmez; haritada eski işaret gösterilmez; izinli yardım olayı konumu yalnızca yetkili alıcılara olay süresince gösterilir | P0 |
| M03-07 | Realtime mesaj hacminde karşılaştırmalı azalma ölçülüp raporlanır (hedef ≥ %90) | Ölçüm raporu (yayın engeli değil) |
| M03-07b | İzleyici oturumu sona ermesi, lease süresi ve bağlantı kesintisi davranışı | P1 |
| M03-08 | Yük: model tepe yükünde API p95 ≤ 1 sn, hata < %1 | P1 [PARAMETRE] |

**M04 — SOS (eski T04 + Karar 04)**
| ID | Test | Seviye |
|---|---|---|
| M04-01 | 100 kontrollü çevrimiçi denemede kayıp ve mükerrer kalıcı olay: 0 | P0 |
| M04-02 | Sunucu kaydı p95 ≤ 2 sn (hedef); APNs kabulü ve kullanıcı teyidi ayrı ölçülür | P1 [PARAMETRE] |
| M04-03 | İnternet yok, şebeke var: SMS ve arama çalışır | P0 |
| M04-04 | İnternet ve şebeke yok: iletişim kurulamadığı açıkça gösterilir | P0 |
| M04-05 | Supabase erişilemez veya SOS API arızalı: yedekler çalışır, başarısızlık başarılı gösterilmez | P0 |
| M04-06 | Push başarısız: SOS kaydı korunur, tekrar deneme çalışır | P0 |
| M04-07 | Eski konum: ölçüm zamanı ve uyarı gösterilir | P0 |
| M04-08 | Konum izni kapalı veya düzenli paylaşım kapalı: SOS oluşturulabilir | P0 |
| M04-09 | İptal edilen SMS gönderilmiş gösterilmez | P0 |
| M04-10 | Bağlantı gelince bekleyen olay güvenle işlenir; sonlandırılmış SOS yeniden aktif olmaz | P0 |
| M04-10b | 15 dk içinde bağlantı: aktif SOS gerçek zaman ve gecikmeyle otomatik gönderilir | P0 |
| M04-10c | Süresi dolmuş SOS otomatik gönderilmez; açılışta "Hâlâ yardıma ihtiyacınız var mı?" seçenekleri gösterilir; yeni SOS ayrı kimlik alır | P0 |
| M04-10d | İptal edilmiş SOS hiçbir koşulda gönderilmez | P0 |
| M04-10e | Sunucuya ulaşmış ama yanıtı gelmemiş SOS idempotent sorguyla doğrulanır; mükerrer olay yok | P0 |
| M04-10f | Sunucudaki aktif SOS yerel kuyruk süresi doldu diye kapanmaz | P0 |
| M04-11 | Bağımsız izleme arızayı algılar; gerçek ailelere test SOS'u göndermez | P1 |
| M04-12 | Acil kişiler çevrimdışı erişilebilir (yeniden başlatma sonrası davranış raporlanır) | P0 |
| M04-13 | Yanlış ülke varsayımıyla acil numara gösterilmez | P0 |
| M04-14 | SOS tek elle, VoiceOver ve büyük yazıyla tamamlanır | P0 |
| M04-15 | SOS ekranında satın alma teklifi yok | P0 |

**M05 — Güvenli bölgeler (eski T05)**
| ID | Test | Seviye |
|---|---|---|
| M05-01 | 30 kontrollü geçişin en az %90'ı uygun izin ve ağda 5 dk içinde saptanır | P1 [PARAMETRE] |
| M05-02 | 8 saatlik sınır yakını durağan testte en fazla 1 yanlış olay | P1 [PARAMETRE] |
| M05-03 | Cihaz başına aktif koşul hiçbir senaryoda 20'yi geçmez | P0 |
| M05-04 | Kayıt hatası gizlenmez; aktif olmayan bölge aktif gösterilmez | P0 |
| M05-05 | Paylaşımı kapalı üyede "bölge bildirimleri aktif değil" gösterilir | P0 |

**M06 — Temel aile güvenliği**
| ID | Test | Seviye |
|---|---|---|
| M06-01 | Alma isteğinde ilk kabul atomik; eşzamanlı kabulde tek kazanan | P1 |
| M06-02 | Güvendeyim beyan zamanı korunur; eski konum tazelenmiş sayılmaz | P0 |
| M06-03 | Hazır yanıtlar yalnızca ilgili olay kapsamında gönderilir | P1 |
| M06-04 | Düşük pil bilgisi zaman damgalı gösterilir; %20 eşiğinde tek bildirim, tekrar yok | P1 |
| M06-05 | Paylaşımı kapalı üye güvendeyim (konumsuz ve tek seferlik konumla), beni almaya gel ve düşük pil kullanabilir; düzenli profil kapasitesi tüketilmez | P0 |
| M06-06 | Güvendeyim konum seçeneği varsayılan kapalı; sürekli takibi yeniden başlatmaz | P0 |
| M06-07 | Beni almaya gel bitince geçici konum erişimi sona erer | P0 |
| M06-08 | Düşük pil için GPS motoru yeniden başlatılmaz | P1 |

**M07 — Abonelik (eski T07 + Karar 06/07)**
| ID | Test | Seviye |
|---|---|---|
| M07-01 | İki ebeveynin eşzamanlı satın alması; rezervasyon zaman aşımı; askıda ve gecikmeli satın alma | P1 |
| M07-02 | Mükerrer satın alma tespiti ve iade yönlendirmesi | P1 |
| M07-03 | Family Sharing kapalı | P1 |
| M07-04 | Geri yükleme; normal iptal; ücretli dönem sonuna kadar hak | P1 |
| M07-05 | İade ve hak geri alma; başarısız ödeme; Billing Grace Period | P1 |
| M07-06 | Satın alanın ayrılması; 7 günlük geçişin bitmesi; aboneliğin başka aileye bağlanması; kötüye kullanım amaçlı döndürme | P1 |
| M07-07 | Satın alanın hesabını silmesi | P1 |
| M07-08 | 10 üyeli ailenin ücretsize geçmesi; 3 profil seçimi; varsayılan sıralama; yalnızca 3 profilin aktif kalması; diğerlerinin aileden çıkarılmaması | P1 |
| M07-09 | Premium biterken aktif SOS'un kesilmemesi | P0 |
| M07-10 | Düşürmede diğer üyelerin SOS ve temel iletişim haklarının korunması | P0 |
| M07-11 | Geçişin 365 gün içinde ikinci kez oluşturulamaması; yönetici/cihaz/sahip değişikliği ve yeniden satın almanın hakkı sıfırlamaması | P1 |
| M07-11b | Grace Period süresince geçiş başlamaması; ödeme başarısızlığıyla kesin bitişte geçiş | P1 |
| M07-11c | İade ve hak geri almada geçiş oluşturulmaması | P1 |
| M07-11d | Geçiş hakkı olmayan ailenin doğrudan ücretsize düşmesi; üyelerin çıkarılmaması | P0 (üyeler/SOS) / P1 |
| M07-11e | 3 profil ve 2 bölgenin Premium sırasında önceden seçilebilmesi | P1 |
| M07-11f | Abonelik sahibinin geçiş hakkı bulunan aileden ayrılması → 7 günlük geçiş | P1 |
| M07-11g | Abonelik sahibinin geçiş hakkını kullanmış aileden ayrılması → doğrudan ücretsiz paket | P1 |
| M07-11h | Ayrılma ve yeniden katılma döngüsü hakkı sıfırlamaz | P1 |
| M07-11i | Aynı ailede abonelik sahiplerinin değişmesi | P1 |
| M07-11j | Ailenin başka geçerli Premium aboneliği varken geçiş başlamaz | P1 |
| M07-11k | Normal bitiş ve ayrılmanın aynı anda olması → tek geçiş | P1 |
| M07-11l | Mükerrer olaylar yeni hak oluşturmaz; mevcut geçiş yeniden başlatılamaz veya uzatılamaz | P1 |
| M07-11m | Ayrılan kişi eski aile verilerine erişemez (geçiş süresince dahil) | P0 |
| M07-11n | Ücretsiz pakete düşüşte üyelikler, SOS, temel güvenlik ve aktif yardım olayları korunur | P0 |
| M07-12 | Bölge kapasitesinin 18'den 2'ye düşmesi | P1 |
| M07-13 | Üye ekleme ve profil değiştirme sınırları; telefon değişiminin sayılmaması | P1 |
| M07-14 | Gecikmeli, mükerrer ve sahte mağaza verisi | P0 (sahte) / P1 |
| M07-15 | Sunucu kesintisinde yeni satın alma engeli; doğrulama servisi kesintisinde mevcut hakların korunması | P1 |
| M07-16 | Sandbox ve Production ayrımı | P1 |
| M07-17 | İstemci manipülasyonuyla ücretsiz kapasite aşılamaz | P0 |
| M07-18 | Satın alma ekranında geçiş kuralları ve yalnızca mevcut özellikler gösterilir | P1 |
| M07-19 | Premium yeniden alınınca haklar doğru açılır; silinmiş geçmiş geri gelmez | P1 |

**M08 — Gizlilik ve hukuk**
| ID | Test | Seviye |
|---|---|---|
| M08-01 | Geçmiş TTL: süre dolunca erişim hemen kapanır, fiziksel silme ≤ 24 saat | P0 |
| M08-02 | Hesap silme ve yedekten geri yükleme sonrası silme kuralları yeniden uygulanır | P0 |
| M08-03 | Push içeriklerinde kişisel veri yok | P0 |
| M08-04 | Loglarda konum, ad, token ve mesaj içeriği yok | P0 |
| M08-05 | Bölüm 17'deki hukuki kabul maddeleri tamamlanmış | P0 |
| M08-06 | info@vdoxlab.com gönderme ve alma testleri başarılı; yasal sayfa bağlantıları çalışıyor | P1 |

**Tasarım ve lokalizasyon (eski T08'in V1 kısmı + Karar 11)**
| ID | Test | Seviye |
|---|---|---|
| UI-01 | 21 dilde eksik anahtar yok; koda sabit metin yok | P1 |
| UI-02 | Kritik metinler 21 dilde insan kontrolünden geçmiş | P0 |
| UI-03 | RTL düzeni, uzun çevirilerde taşma yok | P1 |
| UI-04 | Dynamic Type ve VoiceOver ile kritik güvenlik akışları tamamlanır | P0 |
| UI-05 | Küçük ve büyük iPhone, açık ve koyu görünüm | P1 |
| UI-06 | Kodlanan ekranlar onaylı referanslarla uyumlu; onaysız tasarım yok | P1 |
| UI-07 | Kritik olmayan görsel kusurlar | P2 |

(Eski T08'in V2 kısmı ve eski T09 zamanlı akışlar V1.1/V2 test planına taşınmıştır.)

### 13.4 Yayın onayı (V1)
Bütün P0 testleri geçmiş • bütün P1 engelleri kapanmış • en az iki gerçek iPhone ile test • pil ve konum ölçümleri tamam • hukuki uygunluk onayı • Supabase barındırma ve aktarım kararı kesin • yayın dillerinde güvenlik metinleri insan kontrolünden geçmiş • abonelik gerçek sandbox senaryolarıyla doğrulanmış • sunucu kesintisi ve çevrimdışı SOS test edilmiş • veri güvenliği denetimi tamam • gizlilik ve mağaza metinleri uygulamayla eşleşiyor • test kanıtları kayıtlı • ürün direktörü ve proje sahibi yayın onayı.

---

## 14. PROJE DOSYALARI

`docs/SPEC.md` (bu belge, tek ana kaynak) • `docs/ARCHITECTURE.md` • `docs/DECISIONS.md` • `docs/ROADMAP.md` • `docs/TEST-PLAN.md` • `docs/SECURITY.md` • `docs/PRIVACY.md` • `docs/ECONOMY.md` • `docs/STATUS.md` • `docs/DESIGN-SYSTEM.md` • `docs/SCREEN-INVENTORY.md` • `docs/USER-FLOWS.md` • `docs/LOCALIZATION.md` • `docs/QA/` (design/ dahil) • `design-reference/brand|screens|icons|components|states/` • `assets/branding|icons|illustrations/`

Diğer belgeler SPEC.md ile çelişemez.

---

## 15. KAPSAM KİLİDİ VE YETKİLER

1. Bu şartname onaylanınca V1 kapsamı kilitlenir. Yeni fikirler doğrudan geliştirme listesine değil, yol haritasına yazılır.
2. Kilit yalnızca şu nedenlerle açılır: kritik güvenlik açığı, hukuki zorunluluk, App Store zorunluluğu, işletim sistemi kaynaklı teknik engel, temel işlevi engelleyen durum. Her değişiklik gerekçeli karar kaydı gerektirir.
3. Değişiklik kaydı: karar ID → mevcut kural → bulgu ve kanıt → seçenekler ve etkileri → ürün direktörü kararı → proje sahibi onayı (gerekiyorsa) → sürüm ve kabul testi.

| Rol | Yetki |
|---|---|
| Proje sahibi | Nihai bütçe, yatırım, harcama, hedef pazar, marka ve yayın onayı |
| ChatGPT (ürün direktörü) | Mekanik ve ekonomi kararları, kapsam, kabul hedefleri, kalite kontrol; doğrulanmamış teknik veya hukuki iddiayı kesinleştiremez |
| Claude | Teknik danışmanlık, mimari, kodlama, test, hata analizi, raporlama. Onaylı şartnameyi, fiyatı, saklama sürelerini, rol yetkilerini, güvenlik vaatlerini veya tasarımı bağımsız olarak değiştirmez. Çözülemeyen engeli "çalışıyor" diye kapatmaz. |

---

## 16. TEKNİK BELİRSİZLİKLER (Faz 0'da çözülecek)

| No | Konu | Durum |
|---|---|---|
| T-1 | Mesafe tabanlı motorun gerçek güncelleme sıklığı, doğruluğu ve pil etkisi | Ölçülmedi |
| T-2 | `map_viewers` 120 sn geçerlilik ve yenileme aralığı; tetikleyici + `realtime.send()` yük ve maliyeti | Ölçülmedi |
| T-3 | Realtime mesajlarında %90 azalma hedefi | Hedef, sonuç değil |
| T-4 | Complete Until First User Authentication sınıfında SOS kuyruğu ve acil kişilerin yeniden başlatma sonrası davranışı | Gerçek cihazda doğrulanacak |
| T-5 | App Attest / cihaz bağlama yöntemi | Değerlendirilecek |
| T-6 | Critical Alerts yetkisi | Başvuru; onay belirsiz |
| T-7 | CLMonitor ile 20 koşul bütçesi ve kalkış bölgesi davranışı | Prototipte doğrulanacak |
| T-8 | Güvenli bölge doğruluğu (%90 / 5 dk, yanlış alarm ≤ 1) | Ölçülmedi |
| T-9 | Bağımsız izleme servisinin 60 sn aralığı ücretsiz desteklemesi | Doğrulanmadı |
| T-10 | Supabase Pro kotalarının organizasyondaki mevcut tüketimi (Underworld ve Brain Lab dahil) | Hesap verisi görülmedi |
| T-11 | Güncel mimari için 100 / 1.000 / 10.000 aile maliyet ve yük modeli | Yeniden hesaplanacak |
| T-12 | MapKit rota/ETA servis limitleri (V1'de ETA yok; V1.1 için) | Kontrol edilecek |
| T-13 | Apple Billing Grace Period yapılandırması | Değerlendirilecek |
| T-14 | Tetikleme yöntemi (basılı tutma veya iptal penceresi) kullanılabilirliği | Gerçek cihazda karşılaştırılacak |
| T-15 | Profil bazlı tazelik eşikleri; iOS'un hareketsizlik bilgisini ne sıklıkla ve hangi güvenilirlikle verdiği | Ölçülmedi |
| T-16 | 15 dk SOS kuyruk süresinin uygunluğu | Faz 0'da değerlendirilecek |
| T-17 | Düşük pil değişikliğinin arka planda algılanabilirliği (GPS ve ek arka plan işi olmadan) | Doğrulanmadı |
| T-18 | Uygulama kapalıyken APNs bildirimlerinin 21 dilde yerelleştirilmesi (loc-key veya sunucu tarafı yerelleştirilmiş metin) | Değerlendirilecek |
| T-19 | SOS yüksek hassasiyet profilinin azami süresi; geçici yardım olayı konumlarının erişim ve saklama sınırları | Ölçülmedi |

## 17. HUKUKİ BAĞIMLILIKLAR (gerçek kullanıcı pilotundan önce zorunlu)

1. Uzman hukuk görüşü (KVKK, uluslararası aktarım, çocuk verisi sınıflandırması).
2. Supabase'in KVKK standart sözleşmesine yazılı cevabı.
3. Veri barındırma kararı ve hukuka uygun aktarım mekanizması (gerekirse sözleşme imzası ve 5 iş günü içinde Kurum bildirimi).
4. Çocuk gizliliği değerlendirmesi; yaş aralıkları ve yaş sınırları; veli doğrulama yöntemi; yetişkin hesabına geçiş usulü.
5. Kötüye kullanım önleme tasarımı (aile içi şiddet, velayet anlaşmazlığı, yetkisiz veli).
6. Gizlilik politikası, ebeveyn bilgilendirmesi, kullanım sözleşmesi (pazar bazlı).
7. Veri silme ve saklama politikaları.
8. Push içeriklerinin kişisel veri denetimi; Google Maps bağlantısının gizlilik değerlendirmesi.
9. Yetkisiz erişim ve çapraz aile güvenlik testleri.
10. Kişisel veri ihlali müdahale planı.
11. Hedef ülke bazlı yayın uygunluğu (KVKK, GDPR, COPPA vb.).
12. Marka resmî incelemesi ve tescil stratejisi (TR/AB/ABD).
13. Veri sorumlusunun resmî adı ve bireysel geliştirici statüsünün sözleşmelerde doğru kullanımı.
14. Hukuki danışmanlık, marka ve uyum giderleri için teklif ve bütçe onayı.

---

## 18. BİRLEŞTİRME NOTLARI

### 18.A Çözülen çelişkiler ve çıkarılan eski kurallar
1. **Premium bölge sayısı:** Orijinal "20 bölge" → 18 kullanıcı + 1 kalkış + 1 yolculuk rezervi (Karar 03/06/07). V1'de yolculuk rezervi kullanılmaz.
2. **Konum sıklığı:** Orijinal "normal harekette 2–5 dk, yolculukta 15–30 sn" → mesafe tabanlı adaptif motor (Karar 03); zaman garantisi kaldırıldı; yolculuk profili V1.1'e taşındı.
3. **Realtime:** Orijinal "uygulama açıkken Realtime / Postgres Changes" → yalnızca aktif izleyiciye Private Broadcast, Presence yok (Karar 02/03).
4. **Maliyet tablosu:** Orijinal 10/85/581 USD tablosu güncel maliyet değil, "eski model referansı" olarak bırakıldı.
5. **Yolculuk ve günlük durum:** Orijinalde V1 tamamlayıcı ve Premium özelliği → V1.1 (Karar 09). V1 Premium listesinden ve satış ekranından çıkarıldı. Eski T09 testi V1.1'e taşındı.
6. **Premium listesi:** Karar 07'deki "gelişmiş yolculuk, V2 ebeveyn kontrolü" maddeleri Karar 09 F gereği güncel Premium avantajı olarak gösterilmez.
7. **Premium bitişi:** Karar 06 J, Karar 07 ile değiştirildi (3 aktif profil + 2 bölge, üyeler kalır). Orijinal "bitişte geçmiş 24 saate iner" kuralı, Karar 07'nin saklama ve silme politikasına bağlandı.
8. **Çocuk rolü:** Orijinal "çocuk yolculuk başlatabilir" → V1.1.
9. **Serbest sohbet:** V1.1. V1'de yalnızca olay bazlı hazır yanıtlar (Karar 08/09).
10. **Abonelik yönetimi:** Web bağlantıları yalnızca yedek; birincil `showManageSubscriptions` ve `beginRefundRequest` (Karar 07).
11. **Alan adı:** Karar 10 F/G'deki ticari alan adı, .com/.app önceliği ve alan adı puanı kaldırıldı (Karar 10-D/10-E). VDOX Lab web altyapısı kullanılacak.
12. **Faz adları:** Orijinal P0–P4 teslim aşamaları → Faz 0–10 + Faz D (Karar 09/11). P0/P1/P2 artık yalnızca test önem seviyeleridir; eski "P0 ölçümü" ifadeleri "Faz 0 ölçümü" olarak düzeltildi.
13. **Marka ve 8 aday süreci:** Karar 10 E'deki "8 aday / 3 kısa liste" süreci tamamlandı; güncel durum Karar 10-E (Wingfold koşullu, Eavely yedek).
14. **Supabase destek metninin imzası:** Karar 05 J'deki "VDOX Lab" imzası, Karar 06 A gereği veri sorumlusunun resmî adıyla güncellenecek.
15. **Pil testi cihaz sayısı:** Orijinal T06 "3 cihaz", Karar 03/09 "en az iki iPhone". Bağlayıcı alt sınır olarak 2 alındı; 3 cihaz önerilir.

### 18.B Karar 12 ile çözülen konular
1. **Tazelik ve hareketsiz cihazlar:** Sabit 10 dk kuralı kaldırıldı; beş ayrı zaman bilgisi tutuluyor; profil bazlı eşikler Faz 0'da belirlenecek; yanlış "güncel" gösterimi P0 (Modül 02).
2. **Çevrimdışı SOS kuyruğu:** 15 dk başlangıç süresi; süre dolunca otomatik gönderim yok, kullanıcıya soruluyor (Modül 04).
3. **Paylaşımı kapalı üyeler:** Güvendeyim, beni almaya gel ve düşük pil (%20) ücretsiz ve tanımlı (Modül 06).
4. **7 günlük geçiş:** Aile başına 365 günde bir kez; tetikleyici tablosu tanımlandı (Modül 07).
5. **Destek altyapısı:** Ortak VDOX Lab web altyapısı ve destek kuralları (Bölüm 2.3.1).
6. **Realtime %90:** Yayın engeli değil, ölçüm raporu; izleyicisiz Broadcast üretmeme kuralı zorunlu (Bölüm 8.2).

### 18.C Karar 13 ile çözülen konular
1. **Abonelik sahibinin ayrılması:** Tek ortak yıllık geçiş hakkına bağlandı. Karar 06'daki bağımsız "satın alan ayrılınca 7 gün" kuralı bu kuralla değiştirildi (Modül 07, madde 18 ve 29–31).
2. **Destek adresi:** `info@vdoxlab.com`; `support@vdoxlab.com` oluşturulmayacak (Bölüm 2.3.1).

**Açık ürün konusu: YOK.** Kalan belirsizlikler yalnızca Faz 0 ölçümlerine (Bölüm 16) ve hukuki bağımlılıklara (Bölüm 17) aittir.

### 18.D Nihai denetim netleştirmeleri (Revizyon 4)
Yeni kapsam oluşturmayan, mevcut kararların uygulanmasını netleştiren düzenlemeler:
1. Belge künyesi ve Bölüm 0 madde 2: Karar 01–14 ve marka ek kararları.
2. M04 madde 21: Otomatik yeniden gönderim madde 26–30'a bağlandı; iptal ile gönderim eşzamanlı olursa olay yeniden aktif olamaz.
3. M02-10, M03-06, Bölüm 7.3: Konum yasağı düzenli takip kapsamındadır; izinli SOS, Güvendeyim ve Beni almaya gel konumları amaçla sınırlı korunur.
4. M03-01: İzleyici kaydı tanımı, normal kapanış, beklenmedik kesinti ve yetki iptali (lease beklenmez, M03-01b) ayrıldı.
5. Bölüm 10 madde 3a: Uygulama kapalıyken APNs yerelleştirmesi ayrı tanımlandı (T-18).
6. Bölüm 4 madde 6: Aile yöneticisi yetkisi hukuki veli yetkisi değildir.
7. M08 saklama tablosu: Hesap silme ve aileden ayrılma ayrı satırlarda; geçici yardım olayı konumları satırı eklendi.
8. M01-09: Çift taraflı onay olmadan eşleştirme tamamlanamaz.
9. M02-11: Paylaşım kapatma, cihaz iptali ve aileden ayrılma sonrası bekleyen konum kayıtları reddedilir.
10. M02 madde 6, M02-12, T-19: SOS yüksek hassasiyet süresi ve geçici olay konumu sınırları Faz 0'da kesinleşir; süresiz erişim yok.

---

## 19. KAYNAKLAR (yayın öncesi yeniden kontrol edilecek)

**Apple:** Arka plan konum güncellemeleri, bölge izleme (20 koşul), konum yetkilendirmesi, Family Controls yetkisi, AuthorizationCenter, Managed Settings, arka plan push, App Review Guidelines, App Privacy Details, Auto-renewable Subscriptions, Small Business Program.
- https://developer.apple.com/documentation/corelocation/handling-location-updates-in-the-background
- https://developer.apple.com/documentation/corelocation/monitoring-the-user-s-proximity-to-geographic-regions
- https://developer.apple.com/documentation/corelocation/requesting-authorization-to-use-location-services
- https://developer.apple.com/documentation/familycontrols/requesting-the-family-controls-entitlement
- https://developer.apple.com/documentation/usernotifications/pushing-background-updates-to-your-app
- https://developer.apple.com/app-store/review/guidelines/
- https://developer.apple.com/app-store/app-privacy-details/
- https://developer.apple.com/app-store/subscriptions/
- https://developer.apple.com/app-store/small-business-program/

**Supabase:** Fiyatlandırma, compute, Realtime fiyatlandırma, Realtime mesaj ve tepe bağlantı kullanımı, RLS.
- https://supabase.com/pricing
- https://supabase.com/docs/guides/realtime/pricing
- https://supabase.com/docs/guides/platform/manage-your-usage/realtime-messages
- https://supabase.com/docs/guides/platform/manage-your-usage/realtime-peak-connections
- https://supabase.com/docs/guides/database/postgres/row-level-security

**Marka ön kontrolü (Karar 10-E):**
- https://trademarks.justia.com/991/24/wingfold-99124965.html
- https://www.ipo.gov.uk/t-tmj/tm-journals/2025-031/UK00004236474.html

---
*Belge sonu • Şartname V1.1 • Hedef uygulama V1.0 • Üretim kodlaması başlamamıştır.*
