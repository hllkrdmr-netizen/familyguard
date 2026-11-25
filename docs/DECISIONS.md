# FAMILYGUARD — KARAR GEÇMİŞİ (docs/DECISIONS.md)

Bu dosya tarihsel kayıttır. Kodlama ve uygulama için bağımsız talimat kaynağı DEĞİLDİR. Geçerli kurallar yalnızca `docs/SPEC.md` (V1.1 — Revizyon 4 / Onaylı Ürün Baz Çizgisi) içindedir. Çelişki halinde SPEC.md geçerlidir.

Kayıt türleri: **[TAM METİN]** ürün direktörünün dosya olarak ilettiği karar metni; **[ÖZET KAYIT]** sohbet içinde iletilen kararın Claude tarafından hazırlanmış özeti.

| Karar | Konu | Kayıt |
|---|---|---|
| 01 | iOS V1 (Swift/SwiftUI), Android V1.5 (Kotlin/Compose) | Özet |
| 02 | Realtime ve altyapı optimizasyonu (+ Karar 01 ekleri) | Tam metin |
| 03 | Adaptif konum ve enerji yönetimi | Tam metin |
| 04 | SOS yedekleme ve kesinti güvenliği | Tam metin |
| 05 | KVKK, GDPR ve uluslararası veri güvenliği | Tam metin |
| 06 | Abonelik yönetimi ve kötüye kullanım önlemleri | Tam metin |
| 07 | Ücretsiz güvenlik katmanı ve Premium ekonomisi | Tam metin |
| 08 | Çocuk hesabı, cihaz eşleştirme ve oturum güvenliği | Tam metin |
| 09 | V1 kapsam kilidi ve nihai şartname yapısı | Tam metin |
| 10 | Marka kimliği ve yayın adı | Tam metin |
| 10-A, 10-B | Marka kısa listelerinin reddi | Özet |
| 10-D | Alan adı kısıtının kaldırılması, Soft Premium palet | Özet |
| 10-E | Dördüncü marka turu: Wingfold koşullu, Eavely yedek | Özet |
| 11 | Tasarım öncelikli geliştirme ve lokalizasyon | Tam metin |
| 12 | Nihai şartname açık konuları | Tam metin |
| 13 | Ortak geçiş hakkı ve destek adresi | Tam metin |
| 14 | Ürün kapsam kilidi (koşullu) | Özet |
| Denetim | Nihai şartname denetimi ve onay (Revizyon 4 talimatı) | Tam metin |


---

## KARAR 01 — PLATFORM [ÖZET KAYIT]

- Android sürümü V1.5'e ertelendi; V1 yalnızca native iOS (Swift + SwiftUI).
- Android V1.5: Kotlin + Jetpack Compose; sunucu altyapısı ilk günden platformdan bağımsız.
- Ek revizyonlar Karar 02 metninin A bölümündedir (pilot TR/EN, 21 dil, insan kontrolü, Google Play gereklilikleri).


---

## KARAR 02 [TAM METİN]

Balım, Claude'un ikinci itirazını da kabul ediyorum. Üstelik önerdiği mimariyi yalnızca maliyet açısından değil, ölçeklenebilirlik ve veri güvenliği açısından da daha doğru buluyorum.

Haritaya kimse bakmıyorken sürekli canlı veri göndermenin anlamı yok. Ancak burada önemli bir ayrım yapacağız: Haritanın kapalı olması, çocuğun konum takibinin veya güvenlik mekanizmalarının durması anlamına gelmeyecek. Sadece gereksiz canlı veri dağıtımı duracak.
Karar 01 — Ek revizyonlar
Claude'un önceki karara ilişkin iki uyarısını da kabul ediyorum.
- Pilot testler Türkçe ve İngilizce yapılacak. Mimari ilk günden 21 dili destekleyecek ve genel App Store sürümü 21 dille yayınlanacak.
- SOS, konum izinleri, gizlilik, güvenlik uyarıları ve abonelik metinleri 21 dilde yetkin insan kontrolünden geçirilecek. T08 kabul kriterine eklenecek.
- Android V1.5 yol haritasına Google Play arka plan konum incelemesi, izin beyanları ve geliştirici hesabına uygulanabilecek kapalı test zorunlulukları eklenecek.
Karar 02 — Supabase ve Realtime mimarisi
REVİZYONLA ONAYLANDI
Supabase'in resmî belgelerinden kota ve fiyatlandırma bilgilerini doğruladım.
Kaynak	Pro organizasyon kotası	Aşım ücreti
Realtime mesajları	5 milyon	2,50 $ / milyon
Eşzamanlı bağlantı	500	10 $ / 1.000
Veri çıkışı	250 GB	Kullanım türüne göre
Compute kredisi	10 $	Proje kapasitesine göre

Kotaların organizasyon düzeyinde paylaşıldığı doğru. Ayrıca eşzamanlı bağlantılarda her projenin fatura dönemi içindeki en yüksek bağlantı sayısı ayrı ayrı hesaplanıp toplanıyor. 
Supabase Docs+3

Onayladığım yeni mimari
* Konum izinleri, internet bağlantısı ve işletim sisteminin çalışma koşulları elverdiği sürece.
Burada Claude'un önerisine önemli bir ekleme yapıyorum. Broadcast sistemine geçmek tek başına yeterli değil. Harita kapalıyken sunucu Broadcast mesajı üretmeye devam ederse yine maliyet oluşabilir. Supabase gönderilen ve alıcılara dağıtılan Broadcast mesajlarını ücretlendirmeye dahil ediyor. 
Supabase Docs+1


Bu nedenle aktif izleyici kontrolü sunucu tarafında yapılmalı.
Yeni maliyet değerlendirmesi
Senaryo	Eski model	Kota doluysa
100 aile	10 $	15 $
1.000 aile	85 $	97,50 $
10.000 aile	581 $	593,50 $

Claude'un sunduğu bu tabloyu referans senaryo olarak koruyalım. Ancak yeni mimarinin gerçek maliyetini henüz bilmiyoruz.

10.000 aile senaryosunda eski modeldeki 347,50 dolarlık Realtime mesaj giderini %90 azaltabildiğimizi varsayarsak:
Eski aylık maliyet$581



Optimize edilmiş örnek maliyet$268,25





Aylık tasarruf$312,75

Yıllık tasarruf$3.753


Diğer maliyetlerin sabit kaldığı varsayımsal hesaplamadır. P0 ölçümü yapılmadan kesin bütçe kabul edilmeyecektir.
Claude'a göndereceğimiz karar
FAMILYGUARD — KARAR 02 / REALTIME VE ALTYAPI OPTİMİZASYONU

Karar durumu: REVİZYONLA ONAYLANDI

Supabase organizasyon kotalarının ortak kullanılması konusundaki itiraz kabul edilmiştir.

Aşağıdaki kurallar şartnameye işlenecektir:

A. Karar 01 ek revizyonları
1. Mimari ilk günden 21 dili destekleyecektir. Pilot TR/EN, genel yayın 21 dil olacaktır.
2. SOS, güvenlik, izin, gizlilik ve abonelik metinlerinin 21 dilde yetkin insan kontrolünden geçmesi T08 kabul kriterine eklenecektir.
3. Android V1.5 yol haritasına Google Play arka plan konum beyanı, tanıtım videosu ve izin incelemesi eklenecektir.
4. 12 test kullanıcısı / 14 gün kapalı test şartı, geliştirici hesabına uygulanıyorsa karşılanacaktır. Bu zorunluluğun hesap açılış tarihine bağlı olduğu dikkate alınacaktır.
B. Realtime mimarisi
1. Konum tabloları Postgres Changes üzerinden canlı yayına açılmayacaktır.
2. Konum kayıtları, izinler ve adaptif GPS politikası çerçevesinde veritabanına yazılacaktır.
3. Son bilinen konum ve konum geçmişi ayrı veri yapılarıyla yönetilecektir.
4. Aile haritası açıldığında son konumlar toplu sorguyla alınacaktır.
5. Canlı konum akışı yalnızca yetkili ve aktif harita izleyicileri için Private Broadcast üzerinden sağlanacaktır.
6. Aktif izleyici yoksa konum Broadcast mesajı üretilmeyecektir. Bu kontrol sunucu tarafında yapılacaktır.
7. Aktif izleyici oturumları süreli olacak; uygulama arka plana geçtiğinde, harita kapatıldığında veya oturum süresi dolduğunda sonlandırılacaktır.
8. Bağlantı yeniden kurulduğunda son konum tekrar sorgulanacak; kayıp mesajlar nedeniyle eski konum güncel konumun üzerine yazılmayacaktır.
9. Aile üyeliği ve konum paylaşım izinleri sunucu tarafında doğrulanacaktır. Private Broadcast erişimi RLS politikalarıyla korunacaktır.
10. Aileden çıkarılan veya erişim yetkisi kaldırılan kullanıcıların mevcut canlı oturumları da güvenli biçimde sonlandırılacaktır.
C. Kritik güvenlik mekanikleri
11. SOS, güvenli bölge, düşük pil, yolculuk ve yardım isteği mekanikleri harita izleyicisi bulunmasına bağlı olmayacaktır.
12. Kritik olaylar kalıcı olarak kaydedilecek ve push bildirim kuyruğuyla işlenecektir.
13. Bildirim başarısızlıkları için tekrar deneme ve mükerrer olay engelleme mekanizmaları oluşturulacaktır.
14. Push sağlayıcısının bildirimi kabul etmesi, kullanıcının bildirimi aldığı veya gördüğü anlamına gelmeyecektir. Mevcut SOS durum ayrımları korunacaktır.
15. Realtime kesintisinde son konumu sorgulama ve güvenlik olaylarını kaydetme işlevleri, ilgili servisler çalıştığı sürece devam edecektir.
16. Kritik güvenlik özellikleri maliyet optimizasyonu gerekçesiyle devre dışı bırakılmayacaktır.
D. Ekonomi ve altyapı
17. FamilyGuard mevcut VDOX Lab Pro organizasyonunda ayrı Supabase projesi olarak kurulacaktır.
18. Pilot aşamasında ayrı Pro organizasyon açılmayacaktır.
19. Maliyet modeli hem ortak kotanın müsait olduğu hem de tamamen tüketildiği senaryoları içerecektir.
20. Broadcast gönderici ve alıcı mesajları, izleyici kontrol trafiği, veritabanı yazımları, Edge Function çağrıları, egress ve tepe bağlantılar ayrı ölçülecektir.
21. %90 mesaj tasarrufu bir mühendislik hedefidir; doğrulanmış sonuç değildir.
22. Underworld ve Brain Lab altyapı ayarları izinsiz değiştirilmeyecektir.
23. Organizasyon kota ve harcama alarmları oluşturulacak; otomatik maliyet kısıtlamalarının kritik güvenlik işlevlerine etkisi ayrıca değerlendirilecektir.
E. P0 kabul kriterleri
- Harita kapalıyken konum Broadcast mesajı: 0.
- Yetkisiz aile konumuna erişim: 0.
- Harita kapalıyken güvenlik olaylarının işlenmesi: PASS.
- Realtime kesintisi ve yeniden bağlantı: PASS.
- Eski konumun yeni konumu ezmesini engelleme: PASS.
- Yetkisi kaldırılmış kullanıcının canlı erişimi: ENGELLENDİ.
- Pil tüketimi ve GPS doğruluğu: gerçek cihazlarda ölçülecek.
- Realtime mesaj maliyetinde hedef: karşılaştırılabilir kullanıcı senaryosunda en az %90 azalma; sonuç ölçülerek raporlanacak.
- 100, 1.000 ve 10.000 aile için maliyet ve yük senaryoları güncellenecek.
VDOX Lab organizasyonunun gerçek kullanım verileri henüz görülmediği için kesin altyapı bütçesi onaylanmamıştır. Bu eksiklik ürün şartnamesi görüşmelerini durdurmayacaktır.

Kodlama durumu: Henüz başlanmayacak.

Karar 01 ve Karar 02 kabul edilmiştir. Şimdi üçüncü itirazını sunabilirsin.




Şu ana kadarki karar defterimiz
Karar	Konu	Durum
K01	iOS V1, Android V1.5	Onaylandı
K01-A	21 dil ve insan kontrollü çeviriler	Onaylandı
K02	Optimize edilmiş Realtime mimarisi	Onaylandı
K03	Claude'un sonraki itirazı	Bekliyor

Balım, şu aşamada Supabase paneline girmen zorunlu değil. Gerçek kullanım rakamlarını daha sonra Supabase Usage ekranından alabiliriz.

Önce Claude'un bütün itirazlarını değerlendirelim. Hiçbir maddeyi aceleye getirmeden nihai şartnameyi oluşturacağız.


---

## KARAR 03 [TAM METİN]

FAMILYGUARD — KARAR 03 / ADAPTİF KONUM VE ENERJİ YÖNETİMİ

Karar durumu: REVİZYONLA ONAYLANDI

Zaman tabanlı konum güncellemesi yaklaşımından hareket ve mesafe tabanlı adaptif konum motoruna geçilmesi kabul edilmiştir.

A. Karar 02 ek revizyonları

1. Aktif harita izleyicileri süreli map_viewers kayıtlarıyla yönetilecektir.
2. Başlangıç oturum geçerlilik süresi 120 saniye olacaktır. Yenileme aralığı P0 testlerinde belirlenecektir.
3. Süre, sunucu saati üzerinden doğrulanacaktır.
4. Yetkilendirilmiş aktif izleyici varsa veritabanı tetikleyicisi realtime.send() ile Private Broadcast üretecektir.
5. Presence kullanılmayacaktır.
6. Süresi dolmuş izleyici kayıtları otomatik temizlenecektir.
7. Harita açılması, karşı cihazın konum güncelleme sıklığını zorla artırmayacaktır.
8. Kullanıcı arayüzünde kesintisiz canlı konum vaadi kullanılmayacaktır.
9. Android V1.5 planına 12 test kullanıcısı ve 14 gün kesintisiz kapalı test şartı zorunlu proje görevi olarak eklenecektir.

B. Adaptif konum motoru

10. Dört konum profili oluşturulacaktır: Dinlenme, Normal Hareket, Yolculuk ve SOS.
11. Normal hareket profilinde yaklaşık 100 metre istenen hassasiyet ve 150–200 metre kayıt mesafesi başlangıç parametreleri olacaktır.
12. Zaman bazlı 2–5 dakika garantisi kaldırılacaktır.
13. Hareketsiz durumda düşük enerji tüketimli konum servislerine geçilecektir.
14. Kalkış bölgesi, significant-change ve uygun olduğunda Visits servisleri değerlendirilecektir.
15. Otomatik duraklatma sonrasında standart konum servislerinin kendiliğinden yeniden başlayacağı varsayılmayacaktır.
16. Hareket algılandığında normal takip profilini yeniden başlatan durum makinesi oluşturulacaktır.
17. Durum geçişlerinde GPS sapmalarından kaynaklanan sık profil değişiklikleri engellenecektir.
18. Yolculuk ve SOS profillerinde daha yüksek hassasiyet kullanılacaktır.
19. Yüksek enerji tüketen profiller süreli olacak ve tamamlandığında normal konum politikasına dönülecektir.
20. SOS bildirimi gönderimi, yeni ve yüksek doğruluklu konum ölçümü alınmasını beklemeyecektir. Son bilinen konum ve ölçüm yaşı açıkça belirtilecek, yeni ölçüm elde edilirse güncellenecektir.
21. Harita ekranında ölçüm zamanı, konum yaşı ve doğruluk bilgisi bulunacaktır.
22. Konum güncellenmemesi, kişinin hareketsiz veya güvende olduğunun kanıtı sayılmayacaktır.

C. Güvenli bölge kapasitesi

23. Ücretsiz paket 2 kullanıcı güvenli bölgesini koruyacaktır.
24. Premium paket 18 kullanıcı güvenli bölgesi sunacaktır.
25. Bir bölge otomatik kalkış algılama için ayrılacaktır.
26. Bir bölge dinamik yolculuk varış mekanikleri için ayrılacaktır.
27. Cihaz başına toplam aktif bölge sayısı hiçbir durumda 20’yi aşmayacaktır.
28. Bölge kayıt hataları kullanıcıdan gizlenmeyecektir.
29. Aktif olmayan güvenli bölgeler aktifmiş gibi gösterilmeyecektir.

D. Pil yönetimi

30. T06 normal karma kullanımda 8 saatte en fazla 5 yüzde puan ek pil tüketimi mühendislik hedefini koruyacaktır.
31. Ağırlıklı hareketsiz kullanımda 8 saatte en fazla 2 yüzde puan ek tüketim hedeflenecektir.
32. Yolculuk ve SOS modlarının pil tüketimi ayrı raporlanacaktır.
33. Konum hassasiyeti ve güncelleme sıklığı değerleri ölçülmeden garanti edilmeyecektir.
34. Pil optimizasyonu, temel SOS ve güvenlik bildirimlerini devre dışı bırakmayacaktır.
35. Kullanıcıya konum paylaşımı durumu, gerekli izinler ve pil tüketimi hakkında şeffaf bilgi verilecektir.

E. P0 kabul kriterleri

* En az iki gerçek iPhone ile test yapılacaktır.
* Mümkünse cihazlardan biri daha eski nesil olacaktır.
* Hareketsiz durumdan harekete geçiş test edilecektir.
* Yürüyüş, araç yolculuğu ve uzun süreli durgunluk senaryoları ölçülecektir.
* Ekran kilidi, düşük güç modu, uygulamanın sonlandırılması ve cihazın yeniden başlatılması test edilecektir.
* İnternet kesintisi ve yeniden bağlanma test edilecektir.
* Konum izinlerinin değiştirilmesi ve paylaşımın kapatılması test edilecektir.
* Güvenli bölge giriş/çıkış doğruluğu ve gecikmesi raporlanacaktır.
* Yanlış konum, GPS sapması ve eski konum verisi test edilecektir.
* Pil tüketimi karşılaştırmalı ve tekrarlanabilir koşullarda ölçülecektir.
* SOS ve yolculuk profillerinden normal profile dönüş doğrulanacaktır.

T06 hedefleri karşılanmazsa parametreler optimize edilecek ve testler tekrarlanacaktır. Güvenlik işlevleriyle pil hedefi arasında çözülemeyen bir çelişki varsa ürün direktörü değerlendirmesine sunulacaktır.

Kodlama durumu: Henüz başlanmayacak.

Karar 03 kabul edilmiştir. Dördüncü itirazını sunabilirsin.


---

## KARAR 04 [TAM METİN]

FAMILYGUARD — KARAR 04 / SOS YEDEKLEME VE KESİNTİ GÜVENLİĞİ

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 04 kapsamındaki önerileri kabul edilmiştir. SOS mekanizması yalnızca sunucu altyapısına bağımlı olmayacaktır.

A. SOS çalışma mekanizması

1. SOS bütün kullanıcılar için ücretsiz olacaktır.
2. SOS başlatıldığında sunucuya olay kaydı gönderilecektir.
3. Yeni GPS ölçümü beklenmeden son bilinen konum, ölçüm zamanı ve doğruluk bilgisi kullanılacaktır.
4. Yeni ve geçerli konum elde edildiğinde SOS kaydı güncellenecektir.
5. Kullanıcı sunucu yanıtını beklemeden SMS veya telefon araması seçeneklerini kullanabilecektir.
6. Sunucudan 10 saniye içerisinde onay alınamazsa SMS yedekleme seçeneği belirgin şekilde gösterilecektir.
7. Cihaz çevrimdışıysa 10 saniye beklenmeden yedek iletişim seçenekleri sunulacaktır.
8. Başarısız SOS işlemi hiçbir koşulda başarılı olarak gösterilmeyecektir.

B. SMS yedekleme sistemi

9. Apple MessageUI teknolojisi kullanılacaktır.
10. SMS otomatik gönderilmeyecektir. Kullanıcının gönderme işlemini onaylaması gerekecektir.
11. SMS içeriğinde aşağıdaki bilgiler bulunacaktır:

* Yardım isteyen aile üyesinin adı.
* Yardım talebi.
* Son bilinen konum bağlantısı.
* Konumun ölçüm tarihi ve saati.
* Varsa konum doğruluğu.
* Konum eskiyse açık uyarı.

12. Konum bilgisi mevcut değilse uydurma koordinat kullanılmayacak, konumun alınamadığı belirtilecektir.
13. Konum bağlantısı FamilyGuard sunucusuna bağımlı olmayacaktır.
14. SMS gönderimi için gerekli cihaz ve operatör desteği kontrol edilecektir.
15. Operatör ücretlendirmesi olabileceği kullanıcıya bildirilecektir.
16. SMS gönderme ekranının başarılı sonuç vermesi, alıcının mesajı aldığı veya okuduğu anlamına gelmeyecektir.

C. Cihaz içi acil durum bilgileri

17. Kullanıcı en fazla 5 acil durum kişisi tanımlayabilecektir. Bu özellik ücretsiz olacaktır.
18. Acil durum kişileri cihazda güvenli ve şifreli biçimde saklanacaktır.
19. Acil kişilere internet bağlantısı olmadan erişilebilecektir.
20. Acil kişi değişiklikleri cihaz ve sunucu arasında senkronize edilecektir.
21. Silinen veya yetkisi kaldırılan kişilerin cihaz içi kayıtları senkronizasyon sırasında temizlenecektir.
22. Hesaptan çıkış ve cihaz eşleştirmesinin kaldırılması durumunda ilgili yerel veriler silinecektir.

D. Acil durum aramaları

23. SOS ekranında aşağıdaki seçenekler bulunacaktır:

* Aileme SOS gönder.
* SMS ile yardım iste.
* Acil durum kişisini ara.
* Yerel acil yardım numarasını ara.

24. Telefon aramaları işletim sisteminin izin verdiği arama ve kullanıcı onay mekanizmalarıyla başlatılacaktır.
25. Uygulama arka planda otomatik telefon araması yapmayacaktır.
26. Yerel acil yardım numaraları doğrulanmış ülke bazlı veri tablosuyla yönetilecektir.
27. Türkiye için 112 kullanılacaktır.
28. Acil yardım numarası yalnızca uygulama diline göre belirlenmeyecektir. Kullanıcının bulunduğu ülke dikkate alınacaktır.
29. Ülke belirlenemiyorsa kullanıcıya ülke seçimi sunulacaktır.
30. SOS ekranında FamilyGuard’ın resmî acil yardım hizmetlerinin yerine geçmediği açıkça belirtilecektir.

E. Sunucu kesintisi ve yeniden deneme

31. Sunucuya ulaşamayan SOS olayları cihazda güvenli bir bekleyen işlemler kuyruğuna alınacaktır.
32. İnternet bağlantısı yeniden sağlandığında olay tekrar gönderilmeye çalışılacaktır.
33. Her SOS olayına benzersiz bir kimlik atanacaktır.
34. Tekrar denemeler mükerrer SOS olayları oluşturmayacaktır.
35. Gecikmeli gönderilen SOS olaylarında ilk oluşturulma zamanı korunacaktır.
36. Kullanıcının sonlandırdığı SOS olayları bağlantı geri geldiğinde yeni bir aktif acil durum gibi gönderilmeyecektir.
37. SOS durumları açıkça ayrıştırılacaktır:

* Sunucuya gönderiliyor.
* Sunucu tarafından kaydedildi.
* Bildirim sağlayıcısına iletildi.
* Aile üyesi tarafından görüldü.
* Aile üyesi yardım talebini onayladı.
* Gönderilemedi.
* Sonlandırıldı.

38. Gerçekte doğrulanamayan teslimat bilgileri kullanıcıya gösterilmeyecektir.

F. Bağımsız sunucu izleme sistemi

39. FamilyGuard altyapısı Supabase dışında çalışan bağımsız bir izleme servisiyle denetlenecektir.
40. Başlangıç hedefi 60 saniyelik kontrol aralığıdır.
41. Ücretsiz izleme servisinin bu aralığı desteklemesi doğrulanacaktır. Desteklemiyorsa uygun maliyetli alternatif değerlendirilecektir.
42. Yalnızca sunucunun HTTP yanıtı değil, veritabanı erişimi, SOS kayıt mekanizması ve bildirim kuyruğunun çalışma durumu da kontrol edilecektir.
43. İzleme testleri gerçek kullanıcılara SOS bildirimi göndermeyecektir.
44. Kritik arızalarda proje sahibine bağımsız bildirim gönderilecektir.
45. E-posta ikinci arıza bildirim kanalı olarak kullanılacaktır.
46. Arıza başlangıcı, süresi ve düzelme zamanı kayıt altına alınacaktır.
47. Sunucu yeniden çalışmaya başladığında düzelme bildirimi gönderilecektir.
48. Kritik hata kayıtlarında çocukların konumu, telefon numarası veya diğer kişisel veriler bulunmayacaktır.
49. İzleme sisteminin bulunması, 7/24 insan müdahalesi veya kesintisiz hizmet garantisi olarak pazarlanmayacaktır.

G. P0 test ve kabul kriterleri

* İnternet yok, telefon şebekesi var: SMS ve arama seçenekleri çalışıyor.
* İnternet ve şebeke yok: Kullanıcıya iletişim kurulamadığı açıkça gösteriliyor.
* Supabase erişilemiyor: Yedek iletişim seçenekleri çalışıyor.
* SOS API arızalı: Başarısız işlem başarılı gösterilmiyor.
* Push bildirimi başarısız: SOS kaydı korunuyor ve yeniden deneme mekanizması çalışıyor.
* Eski konum: Ölçüm zamanı ve eski konum uyarısı gösteriliyor.
* Konum izni kapalı: Konumsuz SOS oluşturulabiliyor.
* SMS iptal edildi: Gönderilmiş olarak gösterilmiyor.
* Bağlantı geri geldi: Bekleyen olay güvenli biçimde işleniyor.
* Mükerrer istek: Tek SOS olayı oluşuyor.
* Sonlandırılmış SOS: Yeniden aktif hale gelmiyor.
* Sunucu kesintisi: Bağımsız izleme sistemi arızayı algılıyor.
* İzleme servisi: Gerçek ailelere test SOS’u göndermiyor.
* Acil durum kişileri: Çevrimdışı erişilebilir.
* SOS metinleri ve uyarılar: 21 dilde insan kontrolünden geçiyor.

H. Ekonomi kararı

SMS yedekleme, acil durum kişileri, telefon araması ve temel SOS işlevleri hiçbir zaman Premium üyelik gerektirmeyecektir.

Ücretli SMS API servisi kullanılmayacaktır. SMS, kullanıcının kendi telefon hattı üzerinden ve kendi onayıyla gönderilecektir.

Bağımsız sunucu izleme için öncelikle ücretsiz çözümler değerlendirilecektir. Ücretsiz servislerin yeterli olmadığı durumda güvenlikten ödün verilmeden ek maliyet ürün direktörünün onayına sunulacaktır.

TEMEL ÜRÜN İLKESİ

FamilyGuard hiçbir koşulda gönderilemeyen bir yardım talebini gönderilmiş, görülmeyen bir bildirimi görülmüş veya eski bir konumu güncel olarak göstermeyecektir.

Uygulamanın temel güvenlik mekanizmaları ticari nedenlerle sınırlandırılmayacaktır.

Karar 04: ONAYLANDI.

Kodlama durumu: Henüz başlanmayacak.

Karar 01, 02, 03 ve 04 kabul edilmiştir. Şimdi beşinci itirazını sunabilirsin.


---

## KARAR 05 [TAM METİN]

FAMILYGUARD — KARAR 05 / KVKK, GDPR VE ULUSLARARASI VERİ GÜVENLİĞİ

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 05 kapsamındaki hukuki risk tespitleri kabul edilmiştir.

FamilyGuard’ın ticari hedefleri, çocukların kişisel verilerinin korunmasından ve ürün sahibinin hukuki güvenliğinden üstün tutulmayacaktır.

A. Karar 04 teknik ekleri

1. Bekleyen SOS kuyruğu ve çevrimdışı acil durum kişileri için Complete Until First User Authentication veri koruma sınıfı değerlendirilecek ve gerçek cihazlarda doğrulanacaktır.
2. Cihaz yeniden başlatıldıktan sonra ilk kilit açılmadan bu verilere erişilemeyebileceği dikkate alınacaktır.
3. SMS konum bağlantısında iOS, Android ve tarayıcılarla uyumlu Google Maps bağlantısı kullanılacaktır.
4. Google Maps bağlantısının açılması sırasında konum bilgisinin üçüncü tarafla paylaşılabileceği gizlilik değerlendirmesine dahil edilecektir.
5. Son doğrulanmış ülke bilgisi cihazda saklanacaktır.
6. Cihazın bölge ayarı kesin konum ülkesi olarak kabul edilmeyecektir.
7. Ülke bilgisi belirsizse veya güncelliğini yitirmişse kullanıcıya doğrulatılacaktır.
8. Acil yardım numarası yanlış ülke varsayımıyla gösterilmeyecektir.

B. Hukuki inceleme ve geliştirme sınırları

9. KVKK ve uluslararası kişisel veri aktarımı konusunda uzman bir avukattan görüş alınması kabul edilmiştir.
10. Hukuki danışmanlık maliyeti ürün sahibinin bütçe onayına sunulacaktır.
11. Hukuki inceleme tamamlanmadan gerçek çocuk veya aile verileri üretim altyapısına aktarılmayacaktır.
12. Sentetik konumlar, hayalî aile hesapları ve kişisel veri içermeyen testlerle teknik prototip geliştirilmesine izin verilecektir.
13. Gerçek cihaz konum ve pil testleri için kullanılacak veri işleme yöntemi ayrıca hukuki değerlendirmeye tabi olacaktır.
14. Nihai veri barındırma kararı hukuki görüş alınmadan kesinleştirilmeyecektir.
15. Hukuki uygunluk, gerçek kullanıcı pilotunun ve ticari yayının zorunlu kabul kriteri olacaktır.

C. Supabase standart sözleşme süreci

16. Supabase destek ekibine KVKK standart sözleşmesini imzalayıp imzalamayacağı yazılı olarak sorulacaktır.
17. Sözleşmenin doğru tarafları ve uygulanacak standart sözleşme türü hukuk uzmanıyla doğrulanacaktır.
18. Kurul tarafından yayımlanan zorunlu sözleşme hükümlerinde izinsiz değişiklik kabul edilmeyecektir.
19. Standart sözleşme yönteminin kullanılması halinde beş iş günlük bildirim yükümlülüğü yerine getirilecektir.
20. Bildirimin hangi tarafça yapılacağı ve tamamlandığını gösteren belgeler kayıt altına alınacaktır.
21. Supabase’in GDPR DPA belgesinin tek başına KVKK uyumluluğu sağladığı varsayılmayacaktır.
22. Supabase alt veri işleyenleri, yedekleme konumları, destek erişimleri ve sonraki veri aktarımları incelenecektir.
23. Supabase’in yazılı cevabı alınmadan sözleşmeyi imzalayacağı varsayılmayacaktır.

D. Veri barındırma alternatifleri

Supabase standart sözleşmeyi imzalamazsa aşağıdaki seçenekler değerlendirilecektir:

* Seçenek A: Türkiye yayınını geçici olarak ertelemek.
* Seçenek B: Türkiye’de barındırılan ayrı veya alternatif altyapı kullanmak.
* Seçenek C: Uzman avukatın önereceği başka bir hukuka uygun aktarım mekanizmasını kullanmak.

24. Şu aşamada Türkiye pazarından vazgeçilmeyecektir.
25. Türkiye dışındaki bir pilotun, Türkiye’de yerleşik veri sorumlusunun KVKK yükümlülüklerini otomatik olarak ortadan kaldırdığı varsayılmayacaktır.
26. AB kullanıcıları için GDPR uyumluluğu ayrıca değerlendirilecektir.
27. DPA imzalanması tek başına GDPR uyumluluğunun tamamlandığı anlamına gelmeyecektir.
28. Türkiye’de sunucu kullanılması halinde dahi bildirim, analiz, destek ve diğer üçüncü taraf hizmetlerinin yurt dışı aktarım riskleri incelenecektir.
29. Her alternatifin maliyet, güvenlik, performans ve hukuki sonuçları ürün direktörüne sunulacaktır.
30. Nihai altyapı kararı ürün sahibinin onayıyla verilecektir.

E. Push bildirimlerinde veri minimizasyonu

31. APNs ve gelecekte FCM üzerinden gönderilen bildirim içeriklerinde şu bilgiler bulunmayacaktır:

* Çocuğun veya aile üyesinin adı.
* Telefon numarası.
* Açık adres.
* GPS koordinatları.
* Okul veya ev adı.
* Konum geçmişi.
* Sağlık bilgileri.
* Aile içi mesaj içerikleri.
* Doğrudan kişiyi tanımlayan hesap bilgileri.

32. Bildirimlerde yalnızca gerekli olay kategorisi, genel bildirim metni ve gerektiğinde kişiyi doğrudan tanımlamayan olay referansı kullanılacaktır.
33. Ayrıntılar uygulama açıldıktan sonra kimlik doğrulaması ve yetkilendirme kontrolleriyle sunucudan alınacaktır.
34. Bildirim tokenları ve bağlantılı teknik tanımlayıcılar da kişisel veri değerlendirmesine dahil edilecektir.
35. Bildirim içeriğinin anonimleştirilmesi, bütün aktarım yükümlülüklerinin ortadan kalktığı anlamına gelmeyecektir.

F. Bildirim metinleri

SOS:
“Acil yardım talebi var. Ayrıntıları görmek için uygulamayı açın.”

Güvenli bölge:
“Yeni bir güvenli bölge bildiriminiz var.”

Yardım isteği:
“Bir aile üyeniz yardım istiyor.”

Düşük pil:
“Bir aile cihazının pil seviyesi düşük.”

Yolculuk:
“Takip ettiğiniz yolculukla ilgili yeni bir bildirim var.”

Günlük durum:
“Bir aile durum kontrolü bekliyor.”

36. Bildirimler kilit ekranında kişisel konum veya kimlik bilgisi göstermeyecektir.
37. SOS bildirimleri uygun işletim sistemi önceliğiyle gönderilecektir.
38. Apple Critical Alerts yetkilendirmesi alınmadan sessiz modun veya Odak modunun kesin olarak aşılacağı vaat edilmeyecektir.
39. Bütün güvenlik bildirimleri 21 dilde insan kontrolünden geçirilecektir.

G. Çocukların gizliliği ve güvenliği

40. Çocukların konum verileri yüksek hassasiyet gerektiren kişisel veriler olarak ele alınacaktır.
41. Çocuk konumunun KVKK madde 6 anlamında otomatik olarak özel nitelikli veri olduğu varsayılmayacaktır; hukuki sınıflandırma uzman tarafından yapılacaktır.
42. Ebeveyn yetkilendirmesi ve velayet doğrulama süreçleri tasarlanacaktır.
43. Çocuğa yaşına uygun ve anlaşılır gizlilik bilgilendirmesi sunulacaktır.
44. Gizli takip modu geliştirilmeyecektir.
45. Yetişkin aile üyelerinin konum paylaşımı kendi açık ve bilgilendirilmiş tercihleriyle gerçekleşecektir.
46. Konum erişimleri aile üyeliği ve paylaşım yetkisine göre sınırlandırılacaktır.
47. Aileden çıkarılan kişilerin konum erişimi kaldırılacaktır.
48. Konum verileri reklam, pazarlama veya üçüncü taraflara satış amacıyla kullanılmayacaktır.
49. Reklam SDK’ları ve reklam amaçlı kullanıcı profilleme sistemleri kullanılmayacaktır.
50. Gereksiz kişisel veriler toplanmayacaktır.
51. Konum geçmişi belirlenen saklama süreleri dolduğunda otomatik silinecektir.
52. Hesap silme, aileden ayrılma ve konum paylaşımını sonlandırma mekanizmaları oluşturulacaktır.
53. Yetkisiz ebeveyn erişimi, velayet anlaşmazlıkları, aile içi şiddet ve takip amaçlı kötüye kullanım senaryoları güvenlik tasarımına dahil edilecektir.

H. Veri güvenliği ve teknik mimari

54. Veri aktarımı şifreli bağlantılar üzerinden gerçekleştirilecektir.
55. Veritabanı ve cihaz içi hassas veriler için uygun şifreleme ve erişim politikaları uygulanacaktır.
56. Supabase RLS politikaları bütün hassas tablolar için zorunlu olacaktır.
57. Aileler arasında çapraz veri erişimi engellenecektir.
58. Yönetici erişimleri sınırlandırılacak ve denetlenecektir.
59. Hata kayıtlarında çocukların konumları ve kişisel bilgileri bulunmayacaktır.
60. Konum verilerinin yedeklerde, önbelleklerde ve hata kayıtlarında tutulma süreleri ayrıca belirlenecektir.
61. Kişisel veri ihlali müdahale prosedürü hazırlanacaktır.
62. Veri işleme envanteri ve üçüncü taraf hizmet sağlayıcı listesi oluşturulacaktır.
63. Gerekli olduğu durumlarda veri koruma etki değerlendirmesi hazırlanacaktır.

I. Uluslararası yayın stratejisi

64. 21 dil desteği kararı korunacaktır.
65. 21 dil desteği, otomatik olarak bütün ülkelerde yayın yapılacağı anlamına gelmeyecektir.
66. Ülkeler hukuki uygunluk durumlarına göre ayrı ayrı yayın kapsamına alınacaktır.
67. Türkiye için KVKK, Avrupa için GDPR, ABD için uygulanabilir çocuk gizliliği düzenlemeleri incelenecektir.
68. COPPA ve diğer çocuk gizliliği yükümlülükleri hedef yaş grubu ve uygulamanın işleyişine göre hukuk uzmanıyla değerlendirilecektir.
69. Gizlilik politikaları, ebeveyn bilgilendirmeleri ve kullanıcı sözleşmeleri hedef pazarlara göre uyarlanacaktır.
70. Gerektiğinde yaş ve ülke bazlı kayıt sınırlamaları uygulanacaktır.
71. Hukuki uygunluğu doğrulanmamış ülkelerde ticari yayın yapılmayacaktır.

J. Supabase’e gönderilecek destek talebi

Subject: Turkey KVKK Standard Contractual Clauses for Cross-Border Data Transfers

Hello Supabase Support Team,

We are planning to develop FamilyGuard, a family safety application that may process personal data, including children’s location information, on Supabase infrastructure.

We are currently evaluating the legal requirements applicable to international personal data transfers under Turkish Personal Data Protection Law No. 6698 (KVKK), particularly Article 9.

Could you please clarify the following:

1. Is Supabase willing to execute the standard contractual clauses published by the Turkish Personal Data Protection Authority for controller-to-processor international data transfers, without modifying the mandatory contractual provisions?
2. Is there an established procedure for requesting and executing these Turkish standard contractual clauses?
3. Which Supabase legal entity would be the contracting party?
4. Can Supabase provide information regarding relevant subprocessors, data storage locations, backups, support access and onward international transfers?
5. Are there any additional fees or plan requirements for executing these contractual documents?
6. Are there any restrictions or additional requirements applicable to applications processing children’s location data?

We are currently a Supabase Pro customer and are considering the Frankfurt region for this project.

We would appreciate written clarification before finalizing our infrastructure and launching any pilot involving real personal data.

Thank you.

Best regards,
VDOX Lab
FamilyGuard Project

K. Hukuki kabul kriterleri

Gerçek kullanıcı pilotundan önce aşağıdaki maddelerin tamamlanması zorunludur:

* Uzman hukuk görüşü.
* Supabase yazılı cevabı.
* Veri barındırma kararı.
* Hukuka uygun veri aktarım mekanizması.
* Gerekiyorsa sözleşme imzası ve Kurum bildirimi.
* Çocuk gizliliği değerlendirmesi.
* Ebeveyn doğrulama ve kötüye kullanım önleme tasarımı.
* Gizlilik politikası ve kullanıcı sözleşmeleri.
* Veri silme ve saklama politikaları.
* Push bildirimlerinin kişisel veri içeriği denetimi.
* Yetkisiz erişim ve çapraz aile erişimi güvenlik testleri.
* Kişisel veri ihlali müdahale planı.
* Hedef ülkelere göre yayın uygunluğu değerlendirmesi.

L. Ekonomi kararı

Hukuki danışmanlık, veri güvenliği ve zorunlu mevzuat uyumluluğu giderleri ürünün başlangıç bütçesine ayrı kalem olarak eklenecektir.

Henüz teklif alınmadığı için bu giderlere varsayımsal kesin fiyat atanmayacaktır.

Karar 05: ONAYLANDI.

Hukuki durum: Uzman görüşü ve Supabase yazılı cevabı bekleniyor.

Kodlama durumu: Genel şartname değerlendirmesi tamamlanana kadar başlanmayacak. Sonrasında kişisel veri içermeyen teknik prototiplere izin verilecek; gerçek kullanıcı pilotu hukuki onaya bağlı kalacaktır.

Karar 01, 02, 03, 04 ve 05 kabul edilmiştir.

Şimdi altıncı itirazını sunabilirsin.


---

## KARAR 06 [TAM METİN]

FAMILYGUARD — KARAR 06 / ABONELİK YÖNETİMİ VE KÖTÜYE KULLANIM ÖNLEMLERİ

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 06 kapsamındaki tespitleri kabul edilmiştir.

FamilyGuard abonelik sistemi aile bazlı olacak, mükerrer ödemeler mümkün olduğunca önlenecek ve abonelik kaynaklı hiçbir sorun temel güvenlik özelliklerini etkilemeyecektir.

A. Karar 05 ek revizyonları

1. VDOX Lab, şirket değil marka adı olarak tanımlanacaktır.
2. Hukuki sözleşmelerde ve Supabase yazışmalarında veri sorumlusunun resmî adı ve bireysel geliştirici statüsü kullanılacaktır.
3. SOS bildirimleri iOS Time Sensitive önceliğiyle gönderilecektir.
4. Time Sensitive bildirimlerinin sessiz modu aşmadığı ve kullanıcı ayarlarına bağlı olduğu açıkça dikkate alınacaktır.
5. Critical Alerts yetkilendirme başvurusu P0 görevlerine eklenecektir.
6. Apple’ın Critical Alerts yetkisini onaylayacağı varsayılmayacaktır.
7. SOS dışındaki rutin bildirimlerde gereksiz yüksek öncelik kullanılmayacaktır.

B. Abonelik ekonomisi

8. Tek Premium aile paketi yaklaşımı korunacaktır.
9. Aylık abonelik fiyatı 5,99 USD olacaktır.
10. Yıllık abonelik fiyatı 39,99 USD olacaktır.
11. Yerel mağaza fiyatları ülke ve para birimine göre düzenlenecektir.
12. Ücretsiz aile kapasitesi 3 kişi olacaktır.
13. Premium aile kapasitesi 10 kişi olacaktır.
14. Ücretsiz güvenli bölge sınırı 2, Premium güvenli bölge sınırı 18 olacaktır.
15. Uygulama tamamen reklamsız olacaktır.
16. Abonelik satın alma yetkisi yalnızca yetişkin aile yöneticilerine verilecektir.
17. Çocuk modunda Premium satın alma ekranı gösterilmeyecektir.
18. SOS, SMS yedeği, acil arama ve temel güvenlik özellikleri ücretsiz kalacaktır.

C. Mükerrer satın alma önleme

19. Satın alma ekranı açılmadan önce ailenin Premium durumu sunucudan doğrulanacaktır.
20. Aile zaten Premium ise yeni satın alma düğmesi gösterilmeyecektir.
21. Yetkili aile yöneticilerine aboneliği yöneten kişi ve mağaza bilgisi gösterilecektir.
22. Sunucuya ulaşılamıyorsa yeni abonelik satın alma işlemi başlatılmayacaktır.
23. Mevcut abonelerin satın alım geri yükleme işlemleri desteklenecektir.
24. Satın alma başlatılmadan önce sunucu tarafında aileye özel, süreli satın alma rezervasyonu oluşturulacaktır.
25. Aynı ailede iki yöneticinin eşzamanlı satın alma başlatması mümkün olduğunca önlenecektir.
26. Satın alma rezervasyonları süreli olacak ve başarısız veya iptal edilmiş işlemlerden sonra güvenli biçimde kaldırılacaktır.
27. Askıda kalan mağaza işlemleri rezervasyon süresinin bitmesiyle geçersiz sayılmayacaktır.
28. Gecikmeli tamamlanan mağaza satın alımları ayrıca işlenecektir.
29. Sunucu tarafındaki önlemlerin mağaza düzeyindeki bütün mükerrer satın alımları kesin olarak engelleyebileceği varsayılmayacaktır.

D. Çift satın alma gerçekleşirse

30. Her iki satın alma işlemi de ayrı ayrı doğrulanacak ve kayıt altına alınacaktır.
31. İkinci satın alma kullanıcıdan gizlenmeyecektir.
32. Aynı aileye iki kat Premium hakkı veya ek üyelik kapasitesi verilmeyecektir.
33. Kullanıcıya mükerrer abonelik tespit edildiği bildirilecektir.
34. Abonelik iptali ve iade talebi için ilgili mağaza bağlantıları sunulacaktır.
35. Apple üzerinden gerçekleştirilen satın alımlar için aşağıdaki bağlantılar kullanılabilecektir:

Abonelik yönetimi:
https://apps.apple.com/account/subscriptions

İade talebi:
https://reportaproblem.apple.com

36. Kullanıcıya abonelik iptalinin otomatik para iadesi anlamına gelmediği açıklanacaktır.
37. Apple veya Google tarafından iade onayı verileceği garanti edilmeyecektir.
38. Mükerrer işlemler destek incelemesi için ayrı olay türüyle kaydedilecektir.
39. Satın alımın iptal veya iade edilmesi, diğer geçerli aboneliğin haklarını kaldırmayacaktır.

E. Apple Aile Paylaşımı

40. App Store Connect üzerinde FamilyGuard abonelikleri için Apple Family Sharing kapalı tutulacaktır.
41. Apple aile grubu ile FamilyGuard aile grubu birbirinden bağımsız kabul edilecektir.
42. Premium hakları yalnızca doğrulanmış FamilyGuard aile üyelikleri üzerinden dağıtılacaktır.
43. Apple Family Sharing özelliği ürün direktörünün yeni kararı olmadan etkinleştirilmeyecektir.

F. Aile üyesi değiştirme ve kötüye kullanım önlemleri

44. Premium ailede aynı anda en fazla 10 aktif üye bulunabilecektir.
45. Başlangıçta son 30 günlük hareketli dönem içinde en fazla 5 farklı yeni üyenin eklenmesi kuralı pilotta denenecektir.
46. Bu sayı ilk aile kurulumu sırasında 10 kişilik kapasitenin doldurulmasını engellemeyecektir.
47. Daha önce doğrulanmış aynı üyenin yeniden katılması otomatik olarak yeni üye hakkı tüketmeyecektir.
48. Yeni hesaplarla tekrar katılma ve hesap döndürme yoluyla sınırın aşılması engellenecektir.
49. Üye sınırı cihaz sayısına veya telefon değiştirmeye uygulanmayacaktır.
50. Yeni cihaz alan mevcut aile üyeleri güvenli doğrulama sonrasında hesaplarını kullanmaya devam edebilecektir.
51. Üye değişiklikleri, davetler ve aileden ayrılmalar sunucu tarafında kayıt altına alınacaktır.
52. Davet oluşturma ve kullanma işlemleri kötüye kullanıma karşı oran sınırlamasına tabi olacaktır.
53. Şüpheli üye döndürme durumlarında otomatik kalıcı hesap kapatma uygulanmayacaktır.
54. Gerçek ailelerin boşanma, velayet değişikliği, yeni aile üyesi veya bakım sorumluluğu gibi nedenlerle mağdur olmaması için güvenli destek istisnası bulunacaktır.
55. Destek istisnaları üyelerin açık paylaşım izinlerini veya aileye katılma onaylarını geçersiz kılmayacaktır.
56. Üye ekleme sınırının dolması mevcut aile üyelerinin güvenlik özelliklerini etkilemeyecektir.
57. Beş yeni üye sınırı kesinleşmiş ticari kural değil, pilot mühendislik parametresi olarak kabul edilecektir.

G. Satın alan kişinin aileden ayrılması

58. Mağaza aboneliğinin sahibi satın alan yetişkin kullanıcıdır.
59. Satın alma kaydı ile FamilyGuard ailesine sağlanan Premium hakkı ayrı veri yapılarında tutulacaktır.
60. Bir abonelik aynı anda yalnızca bir FamilyGuard ailesine Premium hakkı sağlayabilecektir.
61. Satın alan kişi aileden ayrılmak istediğinde işlemin abonelik üzerindeki etkileri önceden gösterilecektir.
62. Satın alanın ayrılması halinde eski aileye 7 günlük ücretsiz geçiş süresi verilecektir.
63. Bu süre içerisinde eski ailenin yetkili yöneticilerinden biri yeni Premium abonelik satın alabilecektir.
64. Satın alan kişi geçerli aboneliğini yeni ailesine bağlayabilecektir.
65. Aynı aboneliğin sürekli farklı ailelere aktarılması engellenecektir.
66. Aile değiştirme için başlangıçta 30 günlük bekleme süresi uygulanacaktır.
67. Gerçek aile değişikliklerinde güvenli destek istisnası bulunacaktır.
68. Eski aileye sağlanan 7 günlük geçiş hakkı, sürekli tekrarlanabilen ücretsiz Premium yöntemine dönüştürülemeyecektir.
69. Satın alan kişi eski aileden ayrıldığı anda eski ailenin konumlarına ve diğer özel bilgilerine erişimini kaybedecektir.
70. Aboneliğin satın alan kişiye ait olması, aile üyelerinin kişisel verileri üzerinde mülkiyet veya kalıcı erişim hakkı sağlamayacaktır.
71. Aileden ayrılan satın alan kişinin hesabındaki abonelik yönetimi erişimi korunacaktır.

H. Hesap silme ve abonelik

72. FamilyGuard hesabının silinmesi App Store veya Google Play aboneliğini otomatik olarak iptal etmez.
73. Hesap silme ekranında bu durum açıkça belirtilecektir.
74. Kullanıcıya ilgili mağazanın abonelik yönetimi seçeneği sunulacaktır.
75. Aktif abonelik bulunması kullanıcının hesap silme hakkını engellemeyecektir.
76. Hesap silindikten sonra yalnızca hukuki, finansal ve mağaza doğrulaması açısından tutulması zorunlu asgari işlem kayıtları saklanacaktır.
77. Konum, aile ilişkileri ve gereksiz kişisel veriler saklanmayacaktır.
78. Silinen hesaplara ait geçerli satın alımların güvenli biçimde geri yüklenmesi desteklenecektir.
79. Satın alım geri yükleme işlemi eski aileye veya silinmiş kişisel verilere yeniden erişim sağlamayacaktır.

I. İptal, iade ve ödeme sorunları

80. Kullanıcının otomatik yenilemeyi iptal etmesi Premium hakkını hemen sonlandırmayacaktır.
81. İptal edilen abonelik geçerli ücretli dönem sonuna kadar kullanılabilecektir.
82. Mağaza tarafından iade edilen veya iptal edilen satın alma hakları doğrulanmış mağaza durumuna göre güncellenecektir.
83. Ödeme başarısızlığı, mağaza kaynaklı Billing Grace Period ve FamilyGuard’ın kendi 7 günlük aile geçiş süresi ayrı kavramlar olarak yönetilecektir.
84. Apple Billing Grace Period özelliği değerlendirilecek ve uygun yapılandırmayla kullanılacaktır.
85. Mağaza ödeme sorunlarında uygulama kendi başına doğrulanmamış abonelik süresi üretmeyecektir.
86. Normal Premium sona ermesinde kullanıcıya önceden bildirim gönderilecektir.
87. Doğrulanmış iade, sahte satın alma veya abonelik hakkının geri alınması halinde mağaza durumu gecikmeden uygulanacaktır.
88. Yedi günlük aile geçiş hakkı, satın alanın aileden ayrılması gibi tanımlanmış aile değişikliklerinde kullanılacaktır; her iadede yeniden oluşturulmayacaktır.
89. Abonelik durumunun değişmesi SOS, SMS ve acil arama erişimini kaldırmayacaktır.

J. Premium sona erdiğinde uygulanacak güvenli düşürme politikası

90. Premium abonelik sona erdiğinde aile otomatik olarak silinmeyecektir.
91. Kullanıcılar aile grubundan otomatik çıkarılmayacaktır.
92. Mevcut 10 kişiye kadar olan aile üyeleri grupta kalabilecektir.
93. Ücretsiz 3 kişi sınırının üzerindeki ailelere yeni üye eklenemeyecektir.
94. Yeni kullanıcı davetleri kapasite tekrar uygun hale gelene veya Premium yenilenene kadar sınırlandırılacaktır.
95. Mevcut aile üyelerinin temel konum paylaşımı, SOS ve acil iletişim hakları korunacaktır.
96. Premium güvenli bölgelerinin sona ermesi önceden bildirilecektir.
97. Kullanıcı ücretsiz pakette aktif kalacak 2 güvenli bölgeyi kendisi seçebilecektir.
98. Seçim yapılmazsa önceden tanımlanmış öncelikli bölgeler kullanılacaktır.
99. Devre dışı bırakılan bölgeler aktifmiş gibi gösterilmeyecektir.
100. Premium sona erdiğinde yeni planlı yolculuk başlatma sınırlandırılabilecektir.
101. Devam eden güvenli yolculuklar ve aktif SOS olayları abonelik sona erdiği gerekçesiyle yarıda kesilmeyecektir.
102. Konum geçmişi ücretsiz saklama politikasına göre yönetilecektir.
103. Hukuki saklama sınırları ve silme yükümlülükleri dışında eski konum geçmişi gizli bir Premium arşivi olarak tutulmayacaktır.
104. V2 ebeveyn kontrolü sona erme davranışı ayrı güvenlik kararıyla tanımlanacaktır.
105. Abonelik sona ermesi çocuğun telefonunu kullanılmaz durumda bırakmayacaktır.

K. Sunucu tarafında abonelik doğrulama

106. iOS için StoreKit 2 kullanılacaktır.
107. Apple satın alımları sunucu tarafında doğrulanacaktır.
108. App Store Server Notifications V2 kullanılacaktır.
109. StoreKit appAccountToken, doğrulanmış FamilyGuard hesabıyla satın alma ilişkisinin kurulmasında kullanılacaktır.
110. Mağaza işlem kimlikleri benzersiz olarak saklanacaktır.
111. Aynı satın alma işlemi birden fazla hesaba veya aileye bağlanamayacaktır.
112. İstemciden gelen Premium bilgisi tek başına güvenilir kabul edilmeyecektir.
113. Bildirim imzaları doğrulanacaktır.
114. Mükerrer mağaza bildirimleri aynı işlem sonucunu birden fazla kez oluşturmayacaktır.
115. Gecikmeli ve sıra dışı gelen mağaza bildirimleri desteklenecektir.
116. Mağaza bildirimlerinin her zaman anında ulaşacağı varsayılmayacaktır.
117. Periyodik abonelik mutabakatı yapılacaktır.
118. Uygulama açılışında ve satın alım geri yükleme sırasında abonelik durumu yeniden doğrulanabilecektir.
119. Abonelik durumu sunucu otoritesinde tutulacaktır.
120. Satın alma ve Premium hak değişiklikleri atomik veritabanı işlemleriyle korunacaktır.
121. Sandbox ve Production satın alma kayıtları ayrılacaktır.
122. V1.5 için Google Play Billing ve Real-time Developer Notifications desteği eklenecektir.
123. Google Play bildirimleri alındığında güncel satın alma durumu Google Play Developer API üzerinden doğrulanacaktır.
124. Üçüncü taraf ücretli abonelik yönetim servisi zorunlu olmayacaktır.

L. Platformlar arası abonelik yönetimi

125. Apple ve Google mağazalarından alınan doğrulanmış abonelikler ortak Premium hak sistemine bağlanacaktır.
126. iPhone üzerinden satın alınan aile aboneliği Android aile üyelerine de Premium hakkı sağlayacaktır.
127. Android üzerinden satın alınan aile aboneliği iPhone aile üyelerine de Premium hakkı sağlayacaktır.
128. Abonelik hangi mağazadan satın alındıysa yönetim ve iptal işlemleri ilgili mağaza üzerinden yapılacaktır.
129. Kullanıcıya aboneliği yöneten mağaza açıkça gösterilecektir.
130. Abonelik satın alan kişinin yetkili aile yöneticilerine gösterilmesi dışında gereksiz ödeme ve hesap bilgileri paylaşılmayacaktır.
131. Platformlar arası satın alma ve abonelik yönetimi ekranları ilgili mağazaların güncel kurallarına uygun olacaktır.
132. Kullanıcı ikinci bir platformda yeniden ödeme yapmaya zorlanmayacaktır.

M. T07 kabul kriterleri

Aşağıdaki senaryolar zorunlu test kapsamına alınacaktır:

* İki ebeveynin aynı anda satın alma başlatması.
* Satın alma rezervasyonu zaman aşımı.
* Askıda kalan ve gecikmeli tamamlanan satın alma.
* Mükerrer satın alma ve iade yönlendirmesi.
* Aile Paylaşımı özelliğinin kapalı olması.
* Satın alım geri yükleme.
* Aboneliğin normal iptali.
* Ücretli dönem sonuna kadar hakların korunması.
* İade ve hak geri alma.
* Başarısız ödeme.
* Mağaza Billing Grace Period.
* Satın alan kişinin aileden ayrılması.
* Yedi günlük aile geçiş süresinin sona ermesi.
* Aboneliğin başka aileye bağlanması.
* Aboneliğin kötüye kullanım amacıyla aileler arasında döndürülmesi.
* Satın alan kişinin hesabını silmesi.
* Premium kapasitenin üzerinde mevcut üye bulunan ailenin ücretsiz pakete geçmesi.
* Premium sona ererken aktif SOS bulunması.
* Premium sona ererken devam eden yolculuk bulunması.
* Güvenli bölge kapasitesinin 18’den 2’ye düşmesi.
* Üye ekleme sınırına ulaşılması.
* Mevcut aile üyesinin telefon değiştirmesi.
* Gecikmeli mağaza bildirimleri.
* Mükerrer mağaza bildirimleri.
* Sahte satın alma verisi.
* Sunucu kesintisinde yeni satın alma engeli.
* Abonelik doğrulama servisi kesintisinde mevcut hakların güvenli yönetimi.
* Sandbox ve Production işlem ayrımı.
* V1.5 platformlar arası abonelik senaryoları.

N. Ekonomi kararı

Aylık 5,99 USD ve yıllık 39,99 USD fiyatlandırma korunacaktır.

RevenueCat veya benzeri ücretli abonelik yönetim hizmetleri başlangıçta kullanılmayacaktır. StoreKit 2 ve sunucu tarafındaki doğrulama mekanizmalarıyla kendi abonelik altyapımız oluşturulacaktır.

Yedi günlük aile geçiş haklarının ve mevcut aile üyelerini koruyan güvenli düşürme politikasının altyapı maliyetlerine etkisi pilot sırasında ölçülecektir.

TEMEL ÜRÜN İLKESİ

FamilyGuard, ailelerin güvenlik endişelerini abonelik satın almaya zorlamak için kullanmayacaktır.

Ödeme sorunları nedeniyle hiçbir çocuk aktif yardım talebi sırasında korumasız bırakılmayacak, hiçbir aile üyesinin özel konum verileri abonelik sahibine ait bir hak olarak görülmeyecektir.

Karar 06: ONAYLANDI.

Kodlama durumu: Henüz başlanmayacak.

Karar 01, 02, 03, 04, 05 ve 06 kabul edilmiştir.

Şimdi yedinci itirazını sunabilirsin.


---

## KARAR 07 [TAM METİN]

FAMILYGUARD — KARAR 07 / ÜCRETSİZ GÜVENLİK KATMANI VE PREMIUM EKONOMİSİNİN KORUNMASI

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 07 kapsamındaki gelir açığı tespiti kabul edilmiştir.

Karar 06 Bölüm J, aşağıdaki kurallarla revize edilecektir. Çelişen önceki maddeler yerine Karar 07 uygulanacaktır.

A. Karar 06 teknik eki

1. Abonelik yönetimi için StoreKit showManageSubscriptions kullanılacaktır.
2. İade talebi için StoreKit beginRefundRequest kullanılacaktır.
3. Apple abonelik yönetimi ve iade web bağlantıları yalnızca uygulama içi sistem ekranlarının kullanılamadığı durumlarda yedek olarak sunulacaktır.
4. İade talebinin Apple tarafından kabul edileceği garanti edilmeyecektir.

B. İki katmanlı ürün mimarisi

FamilyGuard özellikleri iki ayrı katmana ayrılacaktır:

GÜVENLİK KATMANI — Ücretsiz.

PREMIUM YÖNETİM KATMANI — Abonelik kapsamında.

Bu ayrım istemci arayüzünde olduğu kadar sunucu yetkilendirme ve veri işleme mimarisinde de uygulanacaktır.

C. Ücretsiz güvenlik katmanı

Aile grubunda bulunan bütün yetkili üyeler, abonelik durumundan bağımsız olarak aşağıdaki özellikleri kullanabilecektir:

* SOS gönderme.
* SOS bildirimi alma.
* SOS yardım talebini onaylama.
* SMS yedekleme.
* Acil durum kişileri.
* Acil telefon araması.
* Beni almaya gel.
* Güvendeyim bildirimi.
* Yardım talebi sırasında izinli konum paylaşımı.
* Mevcut acil olayların takibi.
* Aile içi temel iletişim.

5. Bu özellikler Premium satın alma şartına bağlanmayacaktır.
6. Acil yardım ekranlarında satın alma teklifi gösterilmeyecektir.
7. SOS konumu yalnızca ilgili ve yetkilendirilmiş alıcılarla paylaşılacaktır.
8. Bir kullanıcının aile grubunda bulunması, bütün üyelerin konumuna koşulsuz erişim hakkı sağlamayacaktır.
9. İzinler, paylaşım tercihleri ve güvenlik kuralları her durumda korunacaktır.

D. Premium yönetim katmanı

10. Ücretsiz ailelerde en fazla 3 aktif düzenli konum paylaşım profili bulunacaktır.
11. Premium ailelerde en fazla 10 aktif düzenli konum paylaşım profili bulunacaktır.
12. Ücretsiz ailelerde 2 güvenli bölge aktif olacaktır.
13. Premium ailelerde 18 güvenli bölge aktif olacaktır.
14. Ücretsiz aktif konum profilleri için 24 saatlik konum geçmişi sunulacaktır.
15. Premium aktif konum profilleri için 30 günlük konum geçmişi sunulacaktır.
16. Gelişmiş yolculuk planlama ve V2 ebeveyn kontrolü Premium kapsamında kalacaktır.
17. Premium abonelik aile kapasitesini ve gelişmiş yönetim özelliklerini genişletecektir; temel yardım isteme hakkını satın alınabilir bir ürüne dönüştürmeyecektir.

E. Premium sona erme mekanizması

18. Premium sona erdiğinde hiçbir mevcut üye otomatik olarak aileden çıkarılmayacaktır.
19. Aile grubundaki mevcut üyeler arasındaki izinli temel güvenlik iletişimi korunacaktır.
20. Normal abonelik süresinin sona ermesi halinde aileye bir defalık 7 günlük geçiş süresi tanınacaktır.
21. Geçiş süresince aile yöneticisi ücretsiz pakette aktif kalacak 3 konum profilini seçebilecektir.
22. Ücretsiz pakette aktif kalacak 2 güvenli bölge de yönetici tarafından seçilebilecektir.
23. Geçiş süresi sona erdiğinde yalnızca seçilmiş 3 profil için düzenli konum paylaşımı devam edecektir.
24. Diğer üyelerin aile üyeliği ve temel güvenlik hakları korunacaktır.
25. Diğer üyelerin düzenli konum paylaşımı ve konum geçmişi güncellemesi durdurulacaktır.
26. Premium sona ermeden önce başlatılmış SOS veya güvenli yolculuk, yalnızca abonelik sona erdiği gerekçesiyle yarıda kesilmeyecektir.
27. Geçiş süresinin sona ermesi yeni bir ücretlendirme oluşturmayacaktır.
28. Doğrulanmış sahte satın alma, mağaza tarafından hak geri alma veya kötüye kullanım durumları otomatik olarak yeni bir 7 günlük Premium hakkı doğurmayacaktır.
29. Yedi günlük geçiş süresi, kısa aralıklarla abonelik alıp iptal ederek tekrar tekrar kullanılabilecek bir sisteme dönüşmeyecektir.

F. Aktif konum profillerinin seçimi

30. Aile yöneticisi ücretsiz pakette aktif kalacak 3 profili geçiş süresi boyunca belirleyebilecektir.
31. Bu seçim kullanıcıların mevcut konum paylaşım izinlerini geçersiz kılmayacaktır.
32. Bir kullanıcının konum paylaşım izni yoksa yönetici seçimiyle takip başlatılamayacaktır.
33. Seçim yapılmazsa önceden kullanıcıya gösterilen güvenli ve deterministik varsayılan sıralama kullanılacaktır.
34. Varsayılan sıralamada çocuk profillerine öncelik verilmesi değerlendirilecektir.
35. Aynı öncelikteki profiller arasında aile tarafından belirlenen sıralama kullanılacaktır.
36. Otomatik seçim sonucu aile yöneticisine bildirilecektir.
37. Bir kullanıcının konum paylaşımını sonlandırma hakkı her durumda korunacaktır.

G. Ücretsiz konum profili değiştirme sınırı

38. Ücretsiz 3 profil kapasitesinin sürekli üye değiştirilerek aşılması engellenecektir.
39. Geçiş süresi boyunca yapılan seçim değişiklikleri bu sınıra dahil edilmeyecektir.
40. Geçiş süresi sona erdikten sonra başlangıç kuralı olarak 30 günlük hareketli dönem içerisinde en fazla 2 gönüllü aktif profil değişikliği yapılabilecektir.
41. Bu değer pilotta ölçülecek ve ürün direktörü tarafından yeniden değerlendirilebilecektir.
42. Bir üyenin aileden ayrılması veya konum paylaşım iznini kaldırması engellenmeyecektir.
43. Güvenlik nedeniyle gerekli profil değişiklikleri için uygun destek istisnası bulunacaktır.
44. Profil değiştirme sınırı SOS, yardım isteği veya acil iletişim özelliklerini etkilemeyecektir.
45. Mevcut bir kullanıcının telefon değiştirmesi yeni profil seçimi olarak sayılmayacaktır.

H. Harita arayüzü

46. Bütün mevcut aile üyeleri aile listesinde görünmeye devam edecektir.
47. Düzenli konum paylaşımı aktif olmayan kişiler için haritada eski konum işareti gösterilmeyecektir.
48. Bunun yerine aşağıdaki açıklama kullanılacaktır:

“Düzenli konum paylaşımı aktif değil. Acil yardım ve temel güvenlik özellikleri kullanılabilir.”

49. Premium ile etkinleştirilebilecek profiller için uygun abonelik bilgisi gösterilebilecektir.
50. Konum izni kapalı olması ile abonelik kapasitesi nedeniyle düzenli paylaşımın durması farklı durumlar olarak gösterilecektir.
51. Eski konum hiçbir zaman güncel konum olarak sunulmayacaktır.
52. Aktif SOS durumunda izin verilen son konum, ölçüm zamanı ve doğruluk bilgisiyle gösterilecektir.
53. SOS veya yardım talebi sonlandırıldığında geçici konum erişimi de ilgili güvenlik politikası doğrultusunda sona erecektir.

I. Sunucu maliyeti ve veri minimizasyonu

54. Düzenli konum paylaşım kapasitesi dışında kalan üyeler için gereksiz arka plan GPS çalışması durdurulacaktır.
55. Bu üyelerden düzenli konum geçmişi toplanmayacaktır.
56. Bu üyeler için normal konum Broadcast mesajları üretilmeyecektir.
57. Kullanıcı tarafından başlatılan SOS veya yardım taleplerinde gerekli ve izinli geçici konum paylaşımı desteklenecektir.
58. Yardım talebine ilişkin konum verileri amaçla sınırlı saklama politikasına tabi olacaktır.
59. Premium sona erdiğinde konum geçmişi ilgili saklama ve silme politikasına göre temizlenecektir.
60. Premium yeniden satın alınırsa önceden silinmiş konum geçmişi geri getirilemeyecektir.
61. Premium yeniden etkinleştirildiğinde geçerli izinler doğrulanacaktır.
62. Abonelik satın alınması, kullanıcının kapattığı konum paylaşımını kendiliğinden yeniden başlatmayacaktır.
63. Ücretsiz ailelerde Premium kapasitesinden kalan üyelerin altyapı maliyeti ayrıca ölçülecektir.

J. Kullanıcı bilgilendirme politikası

64. Premium satın alma ekranında abonelik sona erdiğinde uygulanacak kurallar açıkça gösterilecektir.
65. Kullanıcıya aşağıdaki bilgiler satın almadan önce sunulacaktır:

* Premium ile 10 kişiye kadar düzenli konum paylaşımı.
* Premium sona erdiğinde 7 günlük normal geçiş süresi.
* Geçiş sonunda 3 aktif düzenli konum profili.
* Ücretsiz 2 güvenli bölge.
* Mevcut aile üyelerinin grupta kalması.
* Temel güvenlik özelliklerinin ücretsiz devam etmesi.

66. Aboneliğin sona ermesi öncesinde mümkün olduğunda aile yöneticisine hatırlatma gönderilecektir.
67. Geçiş süresinin başlangıcında yeni paket kapasitesi açıklanacaktır.
68. Geçiş süresinin bitmesinden 24 saat önce hatırlatma gönderilecektir.
69. Düzenli konum paylaşımı duracak aile üyelerine durum bildirilecektir.
70. Bildirimlerde çocukların isimleri veya konumları üçüncü taraf push içeriğine dahil edilmeyecektir.
71. Kullanıcıyı korkutarak veya çocuğunun güvenliğinin tamamen sona ereceğini ima ederek abonelik satın almaya yönlendiren metinler kullanılmayacaktır.

K. Güncel paket ekonomisi

ÜCRETSİZ PAKET

* Yeni aile kurulumunda en fazla 3 üye.
* 3 aktif düzenli konum profili.
* 2 güvenli bölge.
* 24 saat konum geçmişi.
* SOS ve temel güvenlik özellikleri.
* Reklamsız kullanım.

PREMIUM PAKET

* En fazla 10 aile üyesi.
* 10 aktif düzenli konum profili.
* 18 güvenli bölge.
* 30 gün konum geçmişi.
* Gelişmiş güvenli yolculuk.
* Gelişmiş aile yönetimi.
* V2 ebeveyn kontrolü ve görev sistemi.
* Reklamsız kullanım.

AYLIK: 5,99 USD.

YILLIK: 39,99 USD.

Premium’dan ücretsiz pakete geçen mevcut ailelerde 10 üyeye kadar aile ilişkisi korunabilir; ancak düzenli konum paylaşımı 3 aktif profille sınırlıdır.

L. T07 ek kabul kriterleri

* Premium aileye 10 üye eklenmesi.
* Premium aboneliğin normal şekilde sona ermesi.
* Yedi günlük geçiş süresinin başlatılması.
* Geçiş süresinin tekrar tekrar oluşturulamaması.
* Üç aktif konum profilinin seçilmesi.
* Seçim yapılmadığında varsayılan sıralamanın uygulanması.
* Geçiş sonunda yalnızca 3 düzenli konum profilinin aktif kalması.
* Diğer üyelerin aileden çıkarılmaması.
* Diğer üyelerin SOS ve temel iletişim haklarının korunması.
* Aktif SOS sırasında Premium sona ermesi.
* Aktif güvenli yolculuk sırasında Premium sona ermesi.
* Yetkisiz SOS konum erişiminin engellenmesi.
* Ücretsiz profil değiştirme sınırının çalışması.
* Konum paylaşım izninin bağımsız olarak kaldırılabilmesi.
* Aktif olmayan profillerden gereksiz konum verisi toplanmaması.
* Aktif olmayan profiller için gereksiz Broadcast üretilmemesi.
* Premium güvenli bölge kapasitesinin 18’den 2’ye düşmesi.
* Konum geçmişinin saklama politikasına uygun silinmesi.
* Premium yeniden satın alındığında hakların doğru etkinleştirilmesi.
* Eski konumların güncel olarak gösterilmemesi.
* İstemci manipülasyonuyla ücretsiz kapasitenin aşılamaması.
* Satın alma ekranında geçiş kurallarının açıkça gösterilmesi.

TEMEL ÜRÜN İLKESİ

FamilyGuard yardım isteme hakkını değil, gelişmiş aile yönetimini satar.

Temel güvenlik bütün üyeler için ücretsiz kalırken, düzenli 10 kişilik konum paylaşımı ve gelişmiş takip özellikleri Premium aboneliğin sürdürülebilir ticari değerini oluşturacaktır.

Karar 07: ONAYLANDI.

Kodlama durumu: Henüz başlanmayacak.

Karar 01, 02, 03, 04, 05, 06 ve 07 kabul edilmiştir.

Şimdi sekizinci itirazını sunabilirsin.


---

## KARAR 08 [TAM METİN]

FAMILYGUARD — KARAR 08 / ÇOCUK HESABI, CİHAZ EŞLEŞTİRME VE OTURUM GÜVENLİĞİ

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 08 kapsamındaki önerileri kabul edilmiştir.

Çocuk hesaplarının kurulumu mümkün olduğunca kolay olacak, ancak kullanım kolaylığı uğruna kimlik doğrulama ve çocuk güvenliğinden ödün verilmeyecektir.

A. Karar 07 ek revizyonları

1. Düzenli konum paylaşımı kapalı olan üye SOS başlattığında, mevcut izinler kapsamında yeni konum ölçümü hemen başlatılacaktır.
2. SOS gönderimi yeni konum ölçümünün tamamlanmasını beklemeyecektir.
3. Eski konum varsa ölçüm zamanı ve eski konum uyarısıyla gösterilecektir.
4. Konum bulunmuyorsa SOS konumsuz gönderilebilecektir.
5. Düzenli konum paylaşımı kapalı üyelerde güvenli bölge izleme de durdurulacaktır.
6. Ebeveyn panelinde şu açıklama gösterilecektir:

“Bu üye için güvenli bölge bildirimleri aktif değil.”

7. Bildirim gelmemesi kişinin güvenli bölgede bulunduğunun kanıtı sayılmayacaktır.
8. V1 aile içi iletişim yalnızca güvenlik olaylarına bağlı hazır mesajlardan oluşacaktır.
9. Hazır yanıt örnekleri:

* Yoldayım.
* Geliyorum.
* Tamam.
* Güvendeyim.
* Yardım talebini gördüm.
* Seni almaya geliyorum.

10. Serbest aile sohbeti V1.1 kapsamındaki mevcut yerini koruyacaktır.

B. Çocuk profili oluşturma

11. Çocuklardan e-posta adresi istenmeyecektir.
12. Çocuklardan şifre oluşturmaları istenmeyecektir.
13. Tam doğum tarihi varsayılan olarak toplanmayacaktır.
14. Çocuk profili doğrulanmış ve yetkili ebeveyn veya yasal veli tarafından oluşturulacaktır.
15. Çocuk profilinde başlangıçta yalnızca gerekli bilgiler bulunacaktır:

* Benzersiz profil kimliği.
* Görünen ad veya takma ad.
* Yaş aralığı.
* İsteğe bağlı hazır avatar.
* Yetkilendirilmiş veli ilişkisi.
* Paylaşım ve cihaz durumu.

16. Gerçek ad ve soyad zorunlu olmayacaktır.
17. Profil fotoğrafı zorunlu olmayacaktır.
18. Okul adı, kimlik numarası, açık adres veya benzeri bilgiler profil oluşturmak için istenmeyecektir.
19. Yaş aralıkları ve hukuki yaş sınırları uzman hukuk görüşüne göre kesinleştirilecektir.
20. Çocuk hesabı ile ebeveyn hesabı teknik olarak ayrı kimlikler olacaktır.
21. Çocuk cihazında ebeveynin giriş bilgileri kullanılmayacaktır.
22. E-posta doğrulamasının tek başına ebeveynlik veya velayet kanıtı olduğu varsayılmayacaktır.
23. Gerekli ebeveyn doğrulaması ve hukuki yetkilendirme Karar 05 kapsamında tamamlanacaktır.

C. QR kodla güvenli eşleştirme

24. Ebeveyn panelinde çocuk profili için tek kullanımlık QR kod oluşturulabilecektir.
25. QR kodun başlangıç geçerlilik süresi 15 dakika olacaktır.
26. QR kod içeriği tahmin edilemeyen, kriptografik olarak güvenli bir eşleştirme anahtarından oluşacaktır.
27. QR kod içerisinde çocuk adı, aile kimliği, konum, telefon numarası veya ebeveyn oturum bilgileri bulunmayacaktır.
28. Eşleştirme anahtarı sunucuda güvenli biçimde saklanacaktır.
29. Anahtarın süresi sunucu saati üzerinden doğrulanacaktır.
30. Eşleştirme işlemi atomik olarak gerçekleştirilecektir.
31. Aynı QR kod ikinci kez kullanılamayacaktır.
32. Yeni QR kod oluşturulduğunda önceki kullanılmamış kod iptal edilecektir.
33. Ebeveyn eşleştirme talebini istediği anda iptal edebilecektir.
34. QR kod veya ekran görüntüsünün tek başına ele geçirilmesi, çocuk konumuna erişim sağlamayacaktır.
35. Eşleştirme isteklerine oran ve deneme sınırı uygulanacaktır.
36. QR kod taranamadığında kullanılabilecek alternatif manuel eşleştirme yöntemi aynı güvenlik kontrollerine tabi olacaktır.

D. Çift taraflı eşleştirme onayı

37. QR kodun taranması konum paylaşımını otomatik başlatmayacaktır.
38. Çocuk cihazında hangi aileye ve hangi veli profiline bağlanıldığı yaşa uygun biçimde gösterilecektir.
39. Çocuk cihazında eşleştirme işlemi açıkça onaylanacaktır.
40. Ebeveyn cihazında yeni cihaz eşleştirme talebi gösterilecektir.
41. Ebeveyn, yeni cihazı doğruladıktan sonra eşleştirme tamamlanacaktır.
42. Her iki cihazda gösterilen kısa doğrulama bilgisi eşleştirmenin doğru cihazlar arasında gerçekleştiğini kontrol etmek için kullanılabilecektir.
43. Eşleştirme tamamlandıktan sonra gerekli iOS izinleri ayrı aşamalarda istenecektir.
44. Eşleştirme onayı, işletim sistemi konum izni yerine geçmeyecektir.
45. Çocuklara yönelik hukuki izinler ve yaşa uygun bilgilendirme tamamlanmadan düzenli konum paylaşımı başlatılmayacaktır.
46. Çocuk cihazındaki onay, yasal veli doğrulamasının yerine geçmeyecektir.
47. Gizli eşleştirme, uzaktan habersiz takip veya görünmez takip modu geliştirilmeyecektir.

E. Çocuk hesabının teknik mimarisi

48. Supabase Anonymous Auth kullanılabilir.
49. Anonim oturum, doğrulanmış eşleştirme işlemi sonrasında çocuk profiline bağlanacaktır.
50. Eşleştirilmemiş anonim oturumlar hiçbir aile verisine erişemeyecektir.
51. Eşleştirilmemiş oturumlar konum gönderemeyecek, aile kanalına bağlanamayacak ve başka kullanıcıların profilini göremeyecektir.
52. Supabase anonim kullanıcılarının authenticated rolüyle işlem yapabildiği dikkate alınacaktır.
53. Yalnızca authenticated rolüne sahip olmak, aile verilerine erişim için yeterli kabul edilmeyecektir.
54. Bütün hassas RLS politikalarında aktif profil, aile üyeliği ve cihaz yetkisi doğrulanacaktır.
55. Çocuk rolü sunucu otoritesinde tutulacaktır.
56. İstemcinin gönderdiği rol veya düzenlenebilir kullanıcı metadata bilgileri yetki kaynağı olarak kabul edilmeyecektir.
57. Çocuk kendi rolünü ebeveyn veya yönetici olarak değiştiremeyecektir.
58. Çocuk başka aile üyelerini yönetemeyecektir.
59. Çocuk yeni bir aile oluşturamayacaktır.
60. Çocuk Premium satın alamayacaktır.
61. Çocuk başka üyelerin konumlarını ancak açıkça tanımlanmış paylaşım yetkileri kapsamında görebilecektir.
62. Anonim oturum açma işlemleri kötüye kullanıma karşı sınırlandırılacaktır.
63. Gerekirse CAPTCHA veya uygun cihaz doğrulama yöntemleri kullanılacaktır.
64. Eşleştirilmemiş ve 24 saatten eski anonim hesaplar güvenli temizleme işlemiyle silinecektir.
65. Aktif eşleştirilmiş çocuk hesapları anonim hesap temizleme işleminden etkilenmeyecektir.

F. Cihaz güvenliği

66. V1 kapsamında her çocuk profiline aynı anda bir aktif telefon bağlanabilecektir.
67. Oturum bilgileri iOS Keychain içerisinde saklanacaktır.
68. Keychain erişim sınıfı arka plan güvenlik görevleriyle uyumlu olacak şekilde seçilecektir.
69. Cihaz kimlik bilgileri mümkün olduğunca başka cihazlara taşınamayacak biçimde korunacaktır.
70. Oturum bilgileri UserDefaults veya şifrelenmemiş dosyalarda saklanmayacaktır.
71. Gereksiz kalıcı donanım tanımlayıcıları toplanmayacaktır.
72. Cihaz kaydında işletim sistemi, uygulama sürümü, eşleştirme zamanı, oturum ilişkisi ve yetki durumu bulunabilecektir.
73. Push tokenları ilgili cihaz kaydıyla ilişkilendirilecektir.
74. Cihaz kimliği tek başına kimlik doğrulama olarak kullanılmayacaktır.
75. Keychain kullanılması, oturumun kriptografik olarak cihaza bağlandığı anlamına gelmeyecektir. Gerekli ek cihaz doğrulaması P0 kapsamında değerlendirilecektir.
76. Apple App Attest veya uygun cihaz doğrulama yöntemleri güvenlik değerlendirmesine dahil edilecektir.

G. Telefon değişikliği ve hesap kurtarma

77. Çocuğun telefonu değiştiğinde yeni çocuk profili oluşturulması gerekmeyecektir.
78. Yetkili veli mevcut çocuk profili için yeni eşleştirme kodu oluşturabilecektir.
79. Yeni cihaz eşleştirme işlemi tamamlandığında önceki cihazın erişimi atomik olarak iptal edilecektir.
80. Yeni cihaz eşleştirmesi sırasında mevcut cihazın durumu kullanıcıya açıkça gösterilecektir.
81. Yeni cihaz eşleştirme işleminin başarısız olması mevcut geçerli cihazı gereksiz yere devre dışı bırakmayacaktır.
82. Ebeveyn panelinde şu seçenekler bulunacaktır:

* Bağlı cihazı görüntüle.
* Yeni cihaz eşleştir.
* Kayıp veya çalıntı cihazın erişimini kapat.
* Eşleştirme talebini iptal et.

83. Cihaz erişiminin iptali için ebeveynin yeniden kimlik doğrulaması istenecektir.
84. Eski cihazın aktif oturumları ve yenileme tokenları iptal edilecektir.
85. Eski cihazın push tokenı kaldırılacaktır.
86. Eski cihazın Realtime erişimi sonlandırılacaktır.
87. Eski cihaz yeniden bağlandığında aile verilerine erişemeyecektir.
88. Yeni cihaz eşleştirmesi mevcut aile üyeliğini veya Premium kapasitesini yeniden tüketmeyecektir.
89. Erişimi iptal edilmiş cihazın sonradan gönderdiği konum kayıtları kabul edilmeyecektir.

H. JWT ve anlık erişim iptali

90. Supabase erişim tokenlarının oturum iptalinden sonra geçerlilik süresi dolana kadar teknik olarak kullanılabileceği dikkate alınacaktır.
91. Bu nedenle yalnızca Supabase oturumunu kapatmak yeterli güvenlik önlemi olarak kabul edilmeyecektir.
92. Hassas veri okuma ve yazma işlemlerinde aktif cihaz yetkisi sunucudan doğrulanacaktır.
93. Gerektiğinde session_id ve cihaz yetkilendirme kayıtları birlikte kontrol edilecektir.
94. İptal edilmiş cihazın geçerli JWT taşıması aile verilerine erişim sağlamayacaktır.
95. Konum yükleme, SOS olayları, aile verileri, geçmiş kayıtları ve güvenlik ayarları bu doğrulamaya tabi olacaktır.
96. Mevcut Private Broadcast kanallarındaki erişimin de iptal edilebilmesi sağlanacaktır.
97. Gerekirse aile kanalının güvenlik sürümü değiştirilerek eski kanala yeni hassas verilerin gönderilmesi engellenecektir.
98. Realtime bağlantı yetkisinin yalnızca ilk bağlantı sırasında kontrol edilmesi yeterli kabul edilmeyecektir.
99. Cihaz iptali güvenlik testleri eski fakat süresi henüz dolmamış JWT ile de gerçekleştirilecektir.
100. Çevrimdışı cihazda önceden görüntülenmiş veya saklanmış verilerin uzaktan anında silinebileceği vaat edilmeyecektir.
101. Bu riski azaltmak için cihazdaki hassas aile verileri asgari seviyede tutulacaktır.

I. Çocuk güvenlik ekranı

102. Çocuk modunda anlaşılır bir güvenlik ekranı bulunacaktır.
103. Bu ekranda aşağıdaki bilgiler gösterilecektir:

* Hangi aileye bağlı olduğu.
* Konumunu kimlerin görebildiği.
* Düzenli konum paylaşımının durumu.
* Güvenli bölge izlemenin durumu.
* Konum izninin durumu.
* Bağlı cihaz bilgisi.
* Acil yardım kişileri.
* Güvenlik ve gizlilik yardımı.

104. Yeni bir kişiye konum erişim yetkisi verildiğinde çocuk yaşına uygun biçimde bilgilendirilecektir.
105. Çocuğun bilgisi dışında yeni bir konum izleyicisi eklenmeyecektir.
106. Çocuk kendisini güvende hissetmediğinde yardım isteyebilecektir.
107. Ebeveyn kontrolü, çocuğun kötüye kullanım veya güvenlik endişesi bildirmesini engellemeyecektir.
108. Çocuk modunda korkutucu, suçlayıcı veya cezalandırıcı paylaşım uyarıları kullanılmayacaktır.
109. Aile içi şiddet, yetkisiz veli ve velayet anlaşmazlığı senaryoları Karar 05 kapsamında ele alınacaktır.

J. Konum izni ve cihaz bağlantı durumları

110. Konum izni değişiklikleri, işletim sistemi uygulamanın bunları algılamasına izin verdiği zamanlarda işlenecektir.
111. Konum paylaşımının durdurulması ve işletim sistemi izninin kapatılması ayrı durumlar olacaktır.
112. Hassas konum izninin kapatılması, bütün konum paylaşımının durdurulması olarak gösterilmeyecektir.
113. Hassasiyet düştüğünde şu açıklama kullanılabilecektir:

“Yaklaşık konum paylaşılıyor. Konum doğruluğu sınırlı olabilir.”

114. Arka plan konum izni kaldırıldığında şu açıklama kullanılabilecektir:

“Arka plan konum paylaşımı aktif değil.”

115. Konum izninin tamamen kapatıldığı doğrulandığında şu açıklama kullanılabilecektir:

“Konum izni kapalı.”

116. Cihazdan veri alınamadığında bunun kesin nedeni bilinmiyorsa şu açıklama kullanılacaktır:

“Son konum ölçümü X süre önce alındı. Cihazın güncel durumu bilinmiyor.”

117. Uygulamanın silindiği doğrulanamıyorsa “Uygulama silindi” bildirimi gösterilmeyecektir.
118. Cihazın kapatıldığı, internetinin kesildiği veya çocuğun paylaşımı bilerek durdurduğu doğrulanmadan iddia edilmeyecektir.
119. Konum izinlerinin kapatılması uygulamanın bütün güvenlik özelliklerini devre dışı bırakmayacaktır.
120. Konumsuz SOS, SMS yedeği ve telefon araması kullanılabilir durumda kalacaktır.
121. İzin değişiklikleri anında sunucuya iletilemezse bağlantı yeniden sağlandığında güncellenecektir.
122. V1 kapsamında uygulamanın silinmesini veya iOS izinlerinin değiştirilmesini kesin olarak engelleme vaadi verilmeyecektir.
123. V2 Family Controls yetenekleri Apple onayı ve hukuki uygunluk kapsamında ayrıca değerlendirilecektir.

K. Çocuk hesabının yetişkin hesabına dönüşmesi

124. Çocuk profili ileride bağımsız yetişkin hesabına dönüştürülebilecektir.
125. Yaş geçişi yalnızca istemcinin değiştirdiği yaş bilgisine dayanmayacaktır.
126. Yaş aralıkları kullanılacak olsa da hukuki yaş geçişinin nasıl doğrulanacağı ayrıca tanımlanacaktır.
127. Yetişkinliğe geçişte önceki ebeveyn yetkileri otomatik olarak süresiz devam etmeyecektir.
128. Yetişkin kullanıcının konum paylaşımı kendi bilgilendirilmiş tercihine bağlanacaktır.
129. Kullanıcının yetişkin hesabına geçmesi ebeveynin ticari abonelik kararına bağlı olmayacaktır.
130. Bağımsız hesap kimlik doğrulaması oluşturulacaktır.
131. Aile üyeliğinin devam etmesi kişinin kendi tercihine bağlı olacaktır.
132. Eski ebeveyn erişimlerinin kaldırılması sunucu tarafında doğrulanacaktır.
133. Yaş geçişinde konum geçmişinin erişim ve saklama politikası ayrıca değerlendirilecektir.
134. Bu mekanizmanın ayrıntıları Karar 05 kapsamındaki uzman hukuk görüşüyle kesinleştirilecektir.

L. Ücretsiz ve Premium ekonomi kuralları

135. Çocuk profili oluşturma, güvenli eşleştirme ve cihaz erişimini iptal etme ücretsiz olacaktır.
136. Telefon değiştirme ve kayıp cihaz kurtarma Premium şartına bağlanmayacaktır.
137. Yeni ailelerde ücretsiz 3 üye kapasitesi korunacaktır.
138. Premium ailelerde 10 üye kapasitesi korunacaktır.
139. Cihaz değiştirme yeni aile üyesi ekleme hakkı tüketmeyecektir.
140. Premium sona erdiğinde Karar 07 güvenlik katmanı kuralları uygulanacaktır.
141. Çocuk güvenliğiyle ilgili cihaz erişimini kapatma veya hesap kurtarma işlemleri ücretli destek kapsamına alınmayacaktır.
142. V1 kapsamında ücretli SMS doğrulama servisi zorunlu tutulmayacaktır.
143. Hukuki ebeveyn doğrulaması için ek bir hizmet gerekirse maliyet ve yöntem ürün sahibinin onayına sunulacaktır.

M. T01 ek kabul kriterleri

Aşağıdaki senaryolar zorunlu test kapsamına alınacaktır:

* Çocuk profili e-posta ve şifre olmadan oluşturulabiliyor.
* Çocuk profili ile ebeveyn hesabı birbirinden ayrı.
* QR kod içerisinde kişisel veri bulunmuyor.
* Geçerli QR kodla eşleştirme yapılabiliyor.
* Süresi dolmuş QR kod reddediliyor.
* Daha önce kullanılmış QR kod reddediliyor.
* İptal edilmiş QR kod reddediliyor.
* Eşzamanlı QR kod tüketme girişiminde yalnızca bir işlem başarılı oluyor.
* QR kod kaba kuvvet denemeleri engelleniyor.
* Çift taraflı onay olmadan konum paylaşımı başlamıyor.
* Eşleştirilmemiş anonim hesap aile verilerini göremiyor.
* Eşleştirilmemiş anonim hesap konum gönderemiyor.
* Çocuk rol yükseltme işlemi gerçekleştiremiyor.
* Çocuk satın alma başlatamıyor.
* Yetkisiz kişi çocuk profili oluşturamıyor veya mevcut profili devralamıyor.
* Aileler arasında çapraz veri erişimi engelleniyor.
* Yeni cihaz eşleştirmesi başarılı oluyor.
* Eski cihazın erişimi iptal ediliyor.
* Eski cihaz geçerli JWT ile bile hassas verilere erişemiyor.
* Eski cihaz konum gönderemiyor.
* Eski cihaz yeni Broadcast mesajlarını alamıyor.
* Eski cihaz yeniden bağlandığında erişim sağlayamıyor.
* Başarısız cihaz değişikliği mevcut cihazı gereksiz yere devre dışı bırakmıyor.
* Telefon değiştirme yeni üye kapasitesi tüketmiyor.
* Eşleştirilmemiş anonim hesap temizleme işlemi aktif çocuk hesaplarını silmiyor.
* Hassas konum izninin kapatılması doğru gösteriliyor.
* Arka plan konum izninin kapatılması doğru gösteriliyor.
* Konum izninin tamamen kapatılması doğru gösteriliyor.
* Uygulama silindiğinde doğrulanmamış silinme bildirimi üretilmiyor.
* Konum güncellenmediğinde ölçüm yaşı doğru gösteriliyor.
* Konum izni olmadan SOS kullanılabiliyor.
* Çocuk güvenlik ekranında konumu görebilen kişiler doğru listeleniyor.
* Yetişkin hesabına dönüşüm sonrasında eski ebeveyn yetkileri kaldırılıyor.
* Güvenlik ve eşleştirme metinleri 21 dilde insan kontrolünden geçiyor.

TEMEL ÜRÜN İLKESİ

FamilyGuard çocukları gizlice izleyen bir uygulama olmayacaktır.

Çocuk hesapları kolay kurulabilmeli, güvenli biçimde yönetilebilmeli ve yetkisiz erişime karşı korunmalıdır. Hiçbir ebeveyn, aile yöneticisi veya abonelik sahibi kendisine tanımlanmamış kişisel veri erişim hakkı elde edemeyecektir.

Karar 08: ONAYLANDI.

Kodlama durumu: Henüz başlanmayacak.

Karar 01, 02, 03, 04, 05, 06, 07 ve 08 kabul edilmiştir.

Şimdi dokuzuncu itirazını sunabilirsin.


---

## KARAR 09 [TAM METİN]

FAMILYGUARD — KARAR 09 / V1 KAPSAM KİLİDİ VE NİHAİ ŞARTNAME

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 09 kapsamındaki proje büyüklüğü, geliştirme kapasitesi ve kalite riski tespitleri kabul edilmiştir.

FamilyGuard V1, kapsam genişliği yerine güvenilirlik, güvenlik, kullanım kolaylığı ve sürdürülebilir işletme üzerine kurulacaktır.

A. Karar 08 teknik eki

1. QR kod taranamadığında manuel eşleştirme kullanılabilecektir.
2. Manuel eşleştirme kodu en az 8 karakterden oluşacaktır.
3. Karıştırılabilecek karakterler kullanılmayacaktır.
4. Örnek biçim: K7MX-4QPR.
5. Kod kriptografik olarak güvenli rastgele üretilecektir.
6. Geçerlilik süresi 15 dakika olacaktır.
7. Kod tek kullanımlık olacaktır.
8. Başlangıçta 5 başarısız denemeden sonra kod iptal edilecektir.
9. Kod, hesap, cihaz ve bağlantı düzeyinde uygun oran sınırlamaları uygulanacaktır.
10. Manuel eşleştirme, QR eşleştirmesindeki çift taraflı onay ve veli doğrulama kurallarını değiştirmeyecektir.

B. V1 — KESİN ÜRÜN KAPSAMI

V1 aşağıdaki sekiz ana modülle sınırlandırılmıştır.

MODÜL 01 — Hesap ve aile yönetimi

* Ebeveyn hesabı.
* Aile oluşturma.
* Yetişkin aile üyesi daveti.
* Çocuk profili oluşturma.
* QR ve manuel eşleştirme.
* Çift taraflı eşleştirme onayı.
* Cihaz değiştirme.
* Kayıp cihaz erişimini iptal etme.
* Aile üyeliği ve paylaşım yetkileri.
* Çocuk güvenlik ekranı.

MODÜL 02 — Adaptif konum motoru

* Dinlenme profili.
* Normal hareket profili.
* SOS konum profili.
* Adaptif GPS hassasiyeti.
* Hareket ve mesafe tabanlı güncelleme.
* Çevrimdışı konum kuyruğu.
* Konum ölçüm zamanı.
* Konum doğruluğu.
* Eski konum uyarısı.
* Pil ve izin durumu.

Yolculuk profili V1.1 kapsamına taşınacaktır.

MODÜL 03 — Aile haritası

* Apple MapKit.
* Yetkili aile üyelerinin son konumları.
* Konum yaşı ve doğruluk göstergesi.
* Ücretsiz 3 aktif konum profili.
* Premium 10 aktif konum profili.
* Harita açıkken Private Broadcast.
* Harita kapalıyken sıfır konum Broadcast mesajı.
* Konum geçmişi.
* Ücretsiz 24 saat geçmiş.
* Premium 30 gün geçmiş.

MODÜL 04 — SOS ve acil yardım

* Tek tuşla SOS.
* Son bilinen konum.
* Yeni konum ölçümü.
* SMS yedekleme.
* Acil durum kişileri.
* Yerel acil yardım numarası.
* Telefon araması.
* Çevrimdışı SOS kuyruğu.
* Mükerrer olay önleme.
* SOS durum doğrulaması.
* Yardım talebini görme ve onaylama.
* Bağımsız sunucu izleme.
* Time Sensitive bildirimler.
* Critical Alerts başvurusu.

Critical Alerts yetkisinin alınması yayın için zorunlu olmayacaktır. Ancak standart SOS ve yedek iletişim mekanizmalarının güvenilir çalışması zorunludur.

MODÜL 05 — Güvenli bölgeler

* Ev, okul, iş yeri ve özel bölgeler.
* Bölge giriş bildirimi.
* Bölge çıkış bildirimi.
* Ücretsiz 2 bölge.
* Premium 18 bölge.
* Bir sistem kalkış bölgesi.
* Bir gelecekteki yolculuk bölgesi rezervi.
* Yanlış bölge bildirimlerini azaltma.
* Bölge izleme durumunun gösterilmesi.

V1’de yolculuk için ayrılan sistem bölgesi kullanılmayacaktır.

MODÜL 06 — Temel aile güvenliği

* Güvendeyim bildirimi.
* Beni almaya gel isteği.
* Yardım isteğini kabul etme.
* Olay bazlı hazır yanıtlar.
* Düşük pil bildirimi.
* Konum izni durumu.
* Son cihaz bağlantısı bilgisi.

Hazır yanıtlar yalnızca ilgili güvenlik ve yardım olayları kapsamında kullanılacaktır.

Beni almaya gel özelliği V1’de gelişmiş rota hesaplama, sürekli araç takibi veya otomatik varış tahmini içermeyecektir.

MODÜL 07 — Abonelik ve ekonomi

* StoreKit 2.
* Sunucu tarafında satın alma doğrulaması.
* App Store Server Notifications V2.
* Satın alma rezervasyonu.
* Mükerrer abonelik yönetimi.
* Satın alım geri yükleme.
* Aile bazlı Premium hakları.
* İade ve iptal yönetimi.
* Yedi günlük geçiş mekanizması.
* Ücretsiz pakete güvenli düşürme.
* Üye ve aktif profil kapasitesi.
* Kötüye kullanım önlemleri.

MODÜL 08 — Gizlilik ve hukuki uygunluk

* KVKK ve uygulanabilir uluslararası düzenlemeler.
* Hukuki veli doğrulaması.
* Yaşa uygun bilgilendirme.
* Hesap silme.
* Aileden ayrılma.
* Konum paylaşımını durdurma.
* Veri saklama ve silme.
* Güvenli cihaz erişim iptali.
* RLS ve yetkilendirme.
* Veri minimizasyonu.
* Kişisel veri içermeyen push bildirimleri.
* Veri ihlali müdahale prosedürü.

V1 için bu sekiz modül dışında yeni ürün özelliği eklenmeyecektir.

C. V1.1 — İLK İÇERİK VE ÖZELLİK GÜNCELLEMESİ

Aşağıdaki özellikler V1 kapsamından çıkarılarak V1.1 yol haritasına taşınacaktır:

1. Güvenli yolculuk.
2. Planlı varış zamanı.
3. Gecikme hatırlatması.
4. Yolculuk varış bölgesi.
5. Gelişmiş yolculuk konum profili.
6. Günlük durum kontrolü.
7. Yaşlı aile bireyleri için planlı durum hatırlatmaları.
8. Genişletilmiş hazır mesaj sistemi.
9. Serbest aile sohbeti.
10. Gelişmiş aile iletişimi.

Serbest sohbet için gerekli içerik güvenliği, engelleme, bildirme ve kötüye kullanım önlemleri ayrıca tasarlanacaktır.

V1.1 özellikleri V1’in yayınlanması ve gerçek kullanım verilerinin değerlendirilmesi sonrasında yeniden önceliklendirilecektir.

Bu özelliklerin tamamının tek güncellemede yayınlanması zorunlu değildir.

D. V1.5 — ANDROID

Karar 01 korunacaktır.

* Kotlin.
* Jetpack Compose.
* Ortak Supabase altyapısı.
* Ortak aile hesapları.
* Platformlar arası abonelik.
* Android arka plan konum yönetimi.
* Google Play Billing.
* FCM bildirimleri.
* Google Play arka plan konum incelemesi.
* Uygulanabilir kapalı test şartları.
* Android gerçek cihaz testleri.

Android istemcisi V1 kapsamında geliştirilmeyecektir.

Sunucu mimarisinin platform bağımsız olması zorunluluğu devam edecektir.

E. V2 — DİJİTAL EBEVEYN KONTROLÜ

* Family Controls.
* Device Activity.
* Managed Settings.
* Ekran süresi.
* Ders modu.
* Uyku modu.
* Uygulama sınırlamaları.
* Görev ve ödül sistemi.
* Platforma uygun gelişmiş ebeveyn kontrolü.

Bu özellikler Apple yetkilendirmesine, hukuki uygunluğa ve işletim sistemi sınırlarına bağlı olacaktır.

V2 özellikleri için V1’de çalışan özellik izlenimi oluşturulmayacaktır.

F. GÜNCEL V1 EKONOMİSİ

ÜCRETSİZ PAKET

* Yeni ailelerde 3 üye.
* 3 aktif düzenli konum profili.
* 2 güvenli bölge.
* 24 saat konum geçmişi.
* SOS.
* SMS yedeği.
* Acil durum kişileri.
* Acil arama.
* Güvendeyim.
* Beni almaya gel.
* Düşük pil bildirimi.
* Olay bazlı hazır yanıtlar.
* Güvenli cihaz eşleştirme ve kurtarma.
* Reklamsız kullanım.

PREMIUM PAKET

* 10 aile üyesi.
* 10 aktif düzenli konum profili.
* 18 güvenli bölge.
* 30 gün konum geçmişi.
* Ücretsiz paketin bütün özellikleri.
* Reklamsız kullanım.

AYLIK: 5,99 USD.

YILLIK: 39,99 USD.

Karar 06 ve Karar 07 kapsamındaki abonelik geçişi, güvenli düşürme ve kötüye kullanım önleme kuralları korunacaktır.

V1.1, V1.5 ve V2 özellikleri mevcut Premium avantajı olarak gösterilmeyecektir.

Kullanıcı henüz geliştirilmemiş bir özellik için ödeme yapmaya yönlendirilmeyecektir.

V1.1 ve V2 özellikleri yayınlandığında mevcut Premium abonelerine ek ücret alınmadan sunulması hedeflenecektir. Yeni paket veya fiyat değişikliği ayrı ürün kararı gerektirecektir.

G. KABUL TESTLERİNİN SINIFLANDIRILMASI

Kabul testleri üç önem seviyesine ayrılacaktır.

P0 — KRİTİK / YAYIN ENGELİ

* Yetkisiz kişisel veri erişimi.
* Çapraz aile erişimi.
* Yetkisiz çocuk eşleştirme.
* Rol yükseltme.
* İptal edilmiş cihazın erişim sağlaması.
* SOS’un sessizce başarısız olması.
* Yanlış SOS başarı veya teslimat bilgisi.
* SMS ve arama yedeğinin çalışmaması.
* Eski konumun güncel olarak gösterilmesi.
* Kritik güvenli bölge hataları.
* Abonelik nedeniyle temel güvenliğin kapanması.
* Veri silme ve saklama yükümlülüklerinin ihlali.
* Hukuki uygunluğun tamamlanmaması.
* Kritik güvenlik açığı.
* Kritik güvenlik ve izin metinlerinin yanlış çevrilmesi.

Bu kategoride başarısız test sayısı sıfır olacaktır.

P1 — ÖNEMLİ / YAYIN ENGELİ

* Temel kullanıcı akışlarının tamamlanamaması.
* Hesap oluşturma ve cihaz değiştirme hataları.
* Abonelik hakkının yanlış hesaplanması.
* Mükerrer satın alma yönetimi hataları.
* Normal kullanımda tekrarlanan uygulama çökmesi.
* Adaptif konum motorunun kabul edilemez performansı.
* Kabul edilmiş pil tüketimi hedeflerinin karşılanmaması.
* Güvenli bölgelerin işlevsel olarak çalışmaması.
* Konum ve izin durumlarının yanlış gösterilmesi.
* Erişilebilirlik nedeniyle temel güvenlik işlevlerinin kullanılamaması.
* Yayınlanacak dillerde kritik lokalizasyon eksikleri.

P1 başarısızlıkları da varsayılan olarak yayın engeli olacaktır.

Herhangi bir P1 kriterinin değiştirilmesi teknik gerekçe, risk analizi ve ürün direktörü onayı gerektirecektir.

Güvenlik, hukuki uygunluk veya temel işlevlerle ilgili P1 kriterleri keyfî biçimde ertelenmeyecektir.

P2 — YAYIN SONRASI İYİLEŞTİRME

* Kritik olmayan görsel kusurlar.
* Küçük animasyon iyileştirmeleri.
* İkincil ekranlardaki boşluk ve hizalama sorunları.
* Güvenliği etkilemeyen performans optimizasyonları.
* Kritik olmayan metin ve görünüm iyileştirmeleri.
* Kullanım kolaylığına yönelik ek düzenlemeler.

P2 sorunları kayıt altına alınabilecek ve gerekçeli olarak yayın sonrasına ertelenebilecektir.

Başarısız bir P0 veya P1 testinin yayını hızlandırmak amacıyla P2 olarak yeniden sınıflandırılması yasaktır.

Ertelenmiş V1.1 veya V2 özelliklerine ait testler V1 başarısızlığı olarak değerlendirilmeyecektir.

H. TEK KAYNAK BELGE

Bütün onaylanmış kararlar tek bir güncel şartnamede birleştirilecektir.

Belge adı:

FAMILYGUARD — V1.1 NİHAİ ÜRÜN ŞARTNAMESİ

Buradaki V1.1, şartname sürüm numarasıdır. Uygulamanın ilk yayın sürümü V1.0 olacaktır.

Sürüm isimlerinin karıştırılmaması için her belgede şartname sürümü ve hedef uygulama sürümü ayrı belirtilecektir.

Nihai belgede:

* Yalnızca geçerli kurallar bulunacaktır.
* Yürürlükten kalkmış maddeler bulunmayacaktır.
* Çelişen eski kurallar temizlenecektir.
* V1, V1.1, V1.5 ve V2 kapsamları ayrılacaktır.
* Kabul kriterleri ilgili modüllere bağlanacaktır.
* Kesinleşmemiş parametreler açıkça işaretlenecektir.
* Hukuki bağımlılıklar belirtilecektir.
* Teknik varsayımlar ölçülmüş sonuçlardan ayrılacaktır.
* Ekonomi tabloları güncellenecektir.

Karar 01–09 ayrı bir karar geçmişi belgesinde saklanacaktır.

Kodlama sırasında eski karar metinleri bağımsız talimat kaynağı olarak kullanılmayacaktır.

Nihai şartname, güncel görev tanımı ve ilgili kabul testleri birlikte uygulama otoritesini oluşturacaktır.

I. PROJE DOSYALARI

Geliştirme başladığında aşağıdaki temel belge yapısı kullanılacaktır:

* docs/SPEC.md — Güncel ürün şartnamesi.
* docs/ARCHITECTURE.md — Teknik mimari.
* docs/DECISIONS.md — Karar geçmişi.
* docs/ROADMAP.md — Sürüm yol haritası.
* docs/TEST-PLAN.md — Kabul testleri ve önem seviyeleri.
* docs/SECURITY.md — Güvenlik kuralları ve tehdit modeli.
* docs/PRIVACY.md — Veri işleme ve saklama kuralları.
* docs/ECONOMY.md — Paketler ve maliyet modeli.
* docs/STATUS.md — Güncel geliştirme durumu.
* docs/QA/ — Test raporları ve kanıtlar.

SPEC.md ürün kuralları için tek geçerli ana kaynak olacaktır.

Diğer belgeler SPEC.md ile çelişmeyecektir.

J. KAPSAM KİLİDİ

Nihai şartname onaylandıktan sonra V1 kapsamı kilitlenecektir.

Yeni özellik fikirleri doğrudan geliştirme listesine eklenmeyecektir.

Yeni fikirler yol haritasına kaydedilecek ve sonraki sürümlerde değerlendirilecektir.

Yalnızca aşağıdaki nedenlerle V1 kapsam kilidi açılabilecektir:

* Kritik güvenlik açığı.
* Hukuki zorunluluk.
* App Store yayın zorunluluğu.
* İşletim sistemi kaynaklı teknik engel.
* Temel ürün işlevinin çalışmasını engelleyen durum.

Kapsam değişiklikleri gerekçeli karar kaydı gerektirecektir.

K. GELİŞTİRME SIRASI

FAZ 0 — Teknik ve hukuki fizibilite.

FAZ 1 — Hesap, aile ve cihaz güvenliği.

FAZ 2 — Adaptif konum motoru ve aile haritası.

FAZ 3 — Güvenli bölgeler ve bildirimler.

FAZ 4 — SOS ve yedek iletişim.

FAZ 5 — Temel aile güvenliği.

FAZ 6 — StoreKit 2 ve abonelik ekonomisi.

FAZ 7 — Ürün arayüzü ve lokalizasyon.

FAZ 8 — Güvenlik, gerçek cihaz ve yük testleri.

FAZ 9 — Hukuki yayın kontrolü ve TestFlight.

FAZ 10 — App Store yayın hazırlığı.

SOS’un teknik fizibilitesi Faz 0’da doğrulanacaktır. Tam SOS entegrasyonu Faz 4’te yapılacaktır.

Her faz kendi kabul kriterlerini tamamlamadan sonraki faza geçilmeyecektir.

L. YAYIN ONAYI

V1’in yayınlanması için:

* Bütün P0 testleri başarılı olmalıdır.
* Bütün geçerli P1 yayın engelleri kapatılmış olmalıdır.
* En az iki gerçek iPhone ile test yapılmalıdır.
* Pil ve konum ölçümleri tamamlanmalıdır.
* Hukuki uygunluk onayı alınmalıdır.
* Supabase barındırma ve aktarım kararı kesinleşmelidir.
* Yayınlanacak dillerde güvenlik metinleri insan kontrolünden geçmelidir.
* Abonelik sistemi gerçek sandbox senaryolarıyla doğrulanmalıdır.
* Sunucu kesintisi ve çevrimdışı SOS senaryoları test edilmelidir.
* Veri güvenliği denetimi tamamlanmalıdır.
* Test kanıtları ve raporları kayıt altına alınmalıdır.
* Ürün direktörü ve proje sahibi yayın onayı vermelidir.

M. EKONOMİ VE İŞLETME YÜKÜ

V1 kapsamının küçültülmesiyle azaltılması hedeflenen yükler:

* Sunucu işlem sayısı.
* Bildirim trafiği.
* Zamanlanmış görevler.
* Lokalizasyon yükü.
* Gerçek cihaz test sayısı.
* Müşteri destek yükü.
* Hata ve bakım maliyeti.
* Geliştirme karmaşıklığı.

Bu tasarruflar henüz ölçülmemiştir.

V1 maliyet modeli P0 ölçümleri ve güncel kapsam üzerinden yeniden hesaplanacaktır.

N. GÖREV VE KARAR YETKİLERİ

PROJE SAHİBİ

Nihai bütçe, yatırım ve yayın onayı.

CHATGPT

Ürün direktörü, mekanik ve ekonomi kararları, kapsam yönetimi, teknik önerilerin değerlendirilmesi ve kalite kontrol.

CLAUDE

Teknik danışmanlık, mimari uygulama, kodlama, testler, hata analizi ve geliştirme raporları.

Claude, onaylanmış şartnameyi bağımsız olarak değiştirmeyecektir.

Teknik engeller gerekçeli olarak ürün direktörüne sunulacaktır.

TEMEL ÜRÜN İLKESİ

FamilyGuard’ın ilk sürümü her şeyi yapan bir uygulama olmayacaktır.

Temel işlevlerini güvenilir, güvenli, anlaşılır ve sürdürülebilir biçimde yerine getiren bir aile güvenliği uygulaması olacaktır.

Karar 09: ONAYLANDI.

Kodlama durumu: Henüz başlanmayacak.

Karar 01–09 kabul edilmiştir.

Varsa kalan itirazlarını ve tespit ettiğin çelişkileri sun.

Bütün itirazlar tamamlandığında nihai şartname birleştirilecek, tekrar denetlenecek ve kapsam kilitlenecektir. Ürün direktörünün nihai onayından önce geliştirme başlatılmayacaktır.


---

## KARAR 10 [TAM METİN]

FAMILYGUARD — KARAR 10 / MARKA KİMLİĞİ VE YAYIN ADI

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 10 kapsamındaki marka çakışması, mağaza görünürlüğü ve hukuki risk tespitleri kabul edilmiştir.

A. Mevcut proje adı

1. FamilyGuard yalnızca geçici iç proje kod adı olarak kullanılacaktır.
2. FamilyGuard adıyla ticari yayın yapılmayacaktır.
3. Mevcut şartname ve karar kayıtlarında geçici olarak FamilyGuard kullanılmaya devam edilebilir.
4. Yeni marka adı kesinleştiğinde güncel ürün şartnamesi ve proje belgeleri yeni isimle düzenlenecektir.
5. Geçmiş karar kayıtları tarihsel bütünlük açısından korunacaktır.

B. Yeni marka adı kriterleri

Yeni marka adı aşağıdaki kriterlere göre değerlendirilecektir:

* Uluslararası kullanıma uygun.
* Ultra premium marka hissi.
* Güven, aile, bağlılık ve huzur çağrışımı.
* Kolay okunabilir ve telaffuz edilebilir.
* Kolay hatırlanabilir.
* Tercihen 1–3 hece.
* Tercihen en fazla 12 karakter.
* Özgün ve ayırt edilebilir.
* Sesli aramaya uygun.
* Uygulama ikonunda ve mağaza görsellerinde güçlü durabilecek.
* 21 dilde olumsuz veya uygunsuz anlam taşımayacak.
* Yalnızca çocuk takibini değil, bütün aile güvenliğini kapsayabilecek.
* Gelecekte Android, Apple Watch ve diğer platformlara genişlemeye uygun.

6. Family, Kids, GPS, Tracker, Guard gibi yaygın kelimelerin marka adında bulunması zorunlu olmayacaktır.
7. Özgün marka isimlerine öncelik verilecektir.
8. Uygulamanın işlevi App Store alt başlığı, açıklaması ve yerelleştirilmiş mağaza metinleriyle anlatılabilecektir.
9. Marka adı, sırf anahtar kelime avantajı sağlamak için jenerik veya rakiplerle karışabilecek şekilde seçilmeyecektir.
10. Kullanıcıda resmî acil yardım kuruluşu veya kamu güvenlik hizmeti izlenimi oluşturan isimlerden kaçınılacaktır.

C. Marka araştırması

Claude, 8 aday isim hazırlayacaktır.

Her aday için aşağıdaki ön kontroller yapılacaktır:

11. Apple App Store araması.
12. Google Play Store araması.
13. Aynı veya benzer kategorilerde kullanılan marka isimleri.
14. Genel internet araması.
15. .com alan adı durumu.
16. .app alan adı durumu.
17. Alan adı satın alma ve yenileme maliyeti.
18. Türk Patent ve Marka Kurumu marka araştırması.
19. EUIPO marka araştırması.
20. WIPO Global Brand Database araştırması.
21. ABD pazarı için USPTO marka araştırması.
22. İlgili marka sınıflarının kontrolü.

Başlangıçta aşağıdaki Nice sınıfları incelenecektir:

* Sınıf 9: İndirilebilir yazılımlar ve mobil uygulamalar.
* Sınıf 42: Yazılım ve teknolojik hizmetler.
* Sınıf 45: İlgili kişisel güvenlik hizmetleri.

Nihai marka sınıfları, uygulamanın hizmet kapsamına göre marka uzmanı tarafından belirlenecektir.

23. Yalnızca birebir aynı isimler değil, benzer yazılışlar ve telaffuzlar da kontrol edilecektir.
24. Aynı sektörde faaliyet gösteren benzer markalar özellikle değerlendirilecektir.
25. Marka veritabanında sonuç bulunmaması hukuki uygunluk garantisi olarak sunulmayacaktır.
26. Yapılan bütün ön kontrollerin kaynakları ve kontrol tarihleri kaydedilecektir.
27. Doğrulanamayan alan adı veya marka durumları açıkça belirsiz olarak işaretlenecektir.
28. App Store arama sonuçlarında isim bulunmaması, ismin App Store Connect üzerinde kesin olarak alınabileceği anlamına gelmeyecektir.

D. Aday isim değerlendirme sistemi

Her aday toplam 100 puan üzerinden değerlendirilecektir:

* Özgünlük ve ayırt edilebilirlik: 20 puan.
* Uluslararası telaffuz: 15 puan.
* Premium marka hissi: 15 puan.
* Güven ve aile çağrışımı: 15 puan.
* Marka çakışma riskinin düşüklüğü: 15 puan.
* Alan adı uygunluğu: 10 puan.
* Mağaza görünürlüğü ve hatırlanabilirlik: 10 puan.

Ciddi marka çakışması veya olumsuz dil anlamı bulunan adaylar, toplam puanı yüksek olsa bile elenecektir.

Her aday için aşağıdaki bilgiler sunulacaktır:

* Marka adı.
* Telaffuzu.
* İsmin anlamı veya oluşum mantığı.
* Marka hikâyesi.
* Güvenlik uygulamasına uygunluğu.
* App Store ve Google Play ön kontrol sonucu.
* Alan adı durumu ve maliyeti.
* Marka veritabanı ön kontrol sonucu.
* Dil ve kültür riski.
* Toplam değerlendirme puanı.

E. İsim seçim süreci

29. Claude, sekiz aday ismi araştırma sonuçlarıyla birlikte ürün direktörüne sunacaktır.
30. Ürün direktörü adayları değerlendirecek, gerekirse yeni isimler önerecektir.
31. En güçlü üç aday kısa listeye alınacaktır.
32. Nihai marka seçimi proje sahibine ait olacaktır.
33. Marka adı kesinleşmeden logo ve uygulama ikonu tasarımı başlatılmayacaktır.
34. Marka adı kesinleşmeden 21 dilde mağaza metinleri hazırlanmayacaktır.
35. Nihai marka adı, mümkün olduğu ölçüde hukuki marka incelemesinden geçirilecektir.

F. Teknik kimliklerin oluşturulması

Marka adı kesinleşmeden aşağıdaki kalıcı üretim kayıtları oluşturulmayacaktır:

* Production Bundle ID.
* App Store Connect uygulama kaydı.
* Android Package Name.
* Google Play Console uygulama kaydı.
* Production Supabase projesi.
* Ticari alan adı.
* Resmî destek e-posta adresi.
* Marka sosyal medya hesapları.
* Production abonelik ürün kimlikleri.

36. Gerekli görülürse sentetik verilerle yapılacak teknik fizibilite çalışmaları için geçici geliştirme kimlikleri kullanılabilecektir.
37. Geçici geliştirme kimlikleri ticari marka seçimini sınırlandırmayacaktır.
38. Production Bundle ID oluşturulduktan sonra kalıcı teknik kimlik olarak ele alınacaktır.
39. Bundle ID ile mağaza görünen adının farklı kavramlar olduğu dikkate alınacaktır.
40. Seçilen marka adının değiştirilmesi halinde teknik kimliklerin gereksiz yere değiştirilmesi gerekmeyecek şekilde mimari kurulacaktır.

G. Alan adı ve marka tescili

41. Alan adı satın alma işlemi proje sahibinin onayı olmadan yapılmayacaktır.
42. Yüksek fiyatlı premium alan adları başlangıçta tercih edilmeyecektir.
43. Alan adı yenileme ücretleri ayrıca kontrol edilecektir.
44. Uygun fiyatlı .com alan adına öncelik verilecektir.
45. .app alan adı güçlü bir alternatif olarak değerlendirilecektir.
46. Marka tescili maliyetleri ayrı bütçe kalemi olarak sunulacaktır.
47. Türkiye, Avrupa Birliği ve ABD marka koruması seçenekleri ayrı ayrı değerlendirilecektir.
48. Marka tescili ve hukuki danışmanlık konusunda kesin maliyet, teklif alınmadan belirlenmeyecektir.
49. VDOX Lab geliştirici markası olarak korunacaktır.
50. Uygulamanın ticari adı ile geliştirici markası birbirinden ayrı olacaktır.
51. Marka sahipliği ve hukuki sözleşme tarafı, proje sahibinin resmî statüsüne uygun düzenlenecektir.

H. Ürün kapsamı ve ekonomi

Bu karar yalnızca marka kimliği ve yayın adıyla ilgilidir.

Aşağıdaki kararlar değişmeyecektir:

* V1 kapsamındaki sekiz temel modül.
* iOS V1 ve Android V1.5 yol haritası.
* 21 dil desteği.
* Ücretsiz 3 aktif konum profili.
* Premium 10 aktif konum profili.
* Ücretsiz 2 güvenli bölge.
* Premium 18 güvenli bölge.
* Ücretsiz 24 saat konum geçmişi.
* Premium 30 gün konum geçmişi.
* Ücretsiz temel güvenlik katmanı.
* Aylık 5,99 USD.
* Yıllık 39,99 USD.
* Reklamsız kullanım.

TEMEL MARKA İLKESİ

Yeni markamız korku değil güven, gözetleme değil aile bağı, karmaşa değil huzur çağrıştıracaktır.

Başka bir uygulamanın benzeri olarak değil, kendine ait kimliği olan uluslararası bir aile güvenliği markası olarak konumlandırılacaktır.

Karar 10: ONAYLANDI.

Marka durumu: Yeni isim araştırması yapılacak.

Kodlama durumu: Henüz başlanmayacak.

Karar 01–10 kabul edilmiştir.

Sekiz aday isim için araştırma görevini kaydet. Önce İtiraz 11’i ve varsa kalan şartname itirazlarını sun. Bütün ürün kararları tamamlandıktan sonra marka adaylarını birlikte değerlendireceğiz.


---

## KARAR 10-A ve 10-B — MARKA KISA LİSTELERİNİN REDDİ [ÖZET KAYIT]

- 10-A: Sevra, Havelo, Orvel şirket, web sitesi ve Companies House kayıtlarında kullanımda bulunduğu için reddedildi; 12 yeni aday istendi.
- 10-B: Cuvara (uygulama + ABD markası), Tenvara (tenvara.io), Velunna (UK şirketi) reddedildi. Hız değil doğruluk önceliği; yeterli aday yoksa listeyi doldurmak için riskli isim eklenmemesi kuralı getirildi.
- Elenen bütün adlar (yeniden önerilmez): FamilyGuard, Veyla, Tendly, Hearthly, Kindora, Halvy, Lunari, Tovia, Elvora, Kinvo, Aurel, Havelo, Sevra, Orvel, Ailora, Nestora, Aurelo, Kinlo, Nuvela, Calyra, Nevaro, Lunessa, Mavira, Haluma, Corvessa, Ombryn, Cuvara, Tenvara, Velunna, Sheltra, Sonvia, Kinward, Nearkin, Keepnear, Hearthbeam, Nestwise, Kinpath, Circlekeep, Bondkeep, Kinstead, Wardlight, Tendwell, Kinlight, Ourhaven, Kinmark, Nearnest, Tethermind, Kinharbor, Lumikin, Homewend, Brightkin, Fernway, Tuckly, Alderly, Embertide, Dovely, Hollin, Treehold, Burrowly, Wovenly.


---

## KARAR 10-D — ALAN ADI VE GÖRSEL YÖN [ÖZET KAYIT]

- Uygulamaya özel .com/.app alınmayacak; VDOX Lab web altyapısı, ürün sayfası, yasal sayfalar, alt alan adları ve Universal Links kullanılacak. Alan adı müsaitliği kriter olmaktan çıkarıldı.
- 12 özgün aday üretilecek, kalabalık köklerden kaçınılacak, en güçlü 5 aday kaynaklarıyla sunulacak; nihai seçim proje sahibinin.
- Soft Premium palet: #F8F6F1, #183D38, #A8C5B5, #E7D9C8, #C63838 (SOS), #222B29; açık ve koyu görünüm; altın çerçeve, metalik/ağır doku, lacivert-altın, mermer, ipek yok. Marka kesinleşmeden logo veya ekran yok.
- Karar 01–11 geçerli; 5,99 / 39,99 USD; reklamsız; iOS V1, Android V1.5.


---

## KARAR 10-E — DÖRDÜNCÜ MARKA ARAŞTIRMASI [ÖZET KAYIT]

- Wingfold: koşullu birinci aday. ABD Sınıf 36 başvurusu (99124965) ve Wingfold España (pazarlama/web) nedeniyle tamamen temiz değil; doğrudan aile güvenliği çakışması yok.
- Treehold: elendi (aile ağacı uygulaması ve mobil oyun). Burrowly: elendi (burrowly.app). Wovenly: elendi (aynı adlı uygulamalar ve hizmetler).
- Eavely: koşullu yedek aday.
- Yeni strateji: sürekli marka turlarıyla ürün geciktirilmeyecek; her sektörde kullanılmamış isim şartı yok; benzer sektör çakışması öncelikli risk; resmî inceleme olmadan hukuki garanti yok; uygulamaya özel alan adı yok; birleştirme marka nedeniyle bekletilmeyecek.


---

## KARAR 11 [TAM METİN]

FAMILYGUARD — KARAR 11 / TASARIM ÖNCELİKLİ GELİŞTİRME VE LOKALİZASYON

Karar durumu: REVİZYONLA ONAYLANDI

Claude’un İtiraz 11 kapsamındaki tasarım sıralaması, geliştirme maliyeti ve lokalizasyon tespitleri kabul edilmiştir.

FamilyGuard, tasarım öncelikli geliştirme yöntemiyle oluşturulacaktır. Onaylanmamış hiçbir ürün ekranı kodlanmayacaktır.

A. Karar 10 araştırma notu

1. Claude’un marka araştırmasına ilişkin teknik sınırlamaları kabul edilmiştir.
2. App Store, Google Play ve genel internet araştırması gerçekleştirilecektir.
3. Kesin olarak doğrulanamayan alan adı müsaitliği “BELİRSİZ” olarak işaretlenecektir.
4. Marka veritabanlarında güvenilir sonuç alınamadığında ilgili araştırma bağlantıları sunulacaktır.
5. Doğrulanmamış marka veya alan adı müsaitliği kesin bilgi olarak gösterilmeyecektir.
6. Nihai marka ve alan adı kontrolleri proje sahibi veya marka uzmanı tarafından tamamlanacaktır.
7. Sekiz aday marka araştırması Karar 11 sonrasında başlayabilecektir.

B. TASARIM ÖNCELİKLİ GELİŞTİRME

8. Ürün mekanikleri kesinleştirilmeden ekran tasarımına başlanmayacaktır.
9. Marka adı kesinleşmeden nihai görsel kimlik oluşturulmayacaktır.
10. Tasarım sistemi onaylanmadan ürün ekranları kodlanmayacaktır.
11. Her ekranın görsel tasarımı ve kullanıcı etkileşimleri kodlamadan önce onaylanacaktır.
12. Claude bağımsız olarak ekran tasarımı değiştirmeyecektir.
13. Onaylanmış tasarım teknik olarak uygulanamıyorsa gerekçesi ürün direktörüne sunulacaktır.
14. Tasarım değişiklikleri onaylanmadan kodlanmayacaktır.
15. Geçici ve kişisel veri içermeyen teknik fizibilite prototipleri bu kuralın istisnasıdır.
16. Teknik prototip arayüzleri nihai ürün ekranı olarak kullanılmayacaktır.
17. Ürün sahibinin ultra premium tasarım beklentisi korunacaktır.

C. MARKA VE GÖRSEL KİMLİK

Marka adı kesinleştikten sonra aşağıdaki varlıklar hazırlanacaktır:

* Ana logo.
* Alternatif logo.
* 1024 × 1024 uygulama ikonu.
* Açılış ekranı.
* Marka renk paleti.
* Tipografi sistemi.
* İkon ailesi.
* Harita işaretleri.
* Aile üyesi avatarları.
* Güvenlik durumu simgeleri.
* SOS görsel kimliği.
* Premium üyelik görsel kimliği.
* Bildirim ve durum ikonları.
* Boş durum illüstrasyonları.
* App Store görsel kimliği.

18. Bütün görsel varlıklar aynı tasarım ailesine ait olacaktır.
19. Hazır ve birbiriyle uyumsuz ikon setleri kullanılmayacaktır.
20. Görsel varlıkların kullanım hakları kontrol edilecektir.
21. Üretim dosyaları uygun çözünürlük ve formatlarda saklanacaktır.
22. Kodla çizilen görseller açıkça belirtilecektir.
23. Onaylanmamış kodla çizilmiş görseller, özel olarak tasarlanmış görsel varlıkların yerine geçirilmeyecektir.
24. Sistem ikonlarının kullanılması gereken erişilebilirlik ve işletim sistemi işlevlerinde Apple standartları korunacaktır.

D. TASARIM SİSTEMİ

Aşağıdaki tasarım kuralları kodlamadan önce hazırlanacaktır:

* Ana ve yardımcı renkler.
* Açık ve koyu görünüm.
* Tipografi ölçeği.
* Başlık ve açıklama stilleri.
* Kart bileşenleri.
* Ana ve ikincil düğmeler.
* Acil yardım düğmeleri.
* Alt navigasyon.
* Form alanları.
* Onay pencereleri.
* Bildirim kartları.
* Harita bilgi panelleri.
* Durum göstergeleri.
* Yükleniyor ekranları.
* Boş durum ekranları.
* Hata ekranları.
* Çevrimdışı durumlar.
* Animasyon ilkeleri.
* Dokunsal geri bildirim.
* Kenar boşlukları ve hizalama.
* Köşe yuvarlaklıkları.
* Kontrast ve okunabilirlik.
* Dynamic Type.
* VoiceOver.
* Sağdan sola dil desteği.
* Küçük ve büyük iPhone ekranlarına uyum.

25. Tasarım değerleri merkezi tasarım tokenları üzerinden yönetilecektir.
26. Her ekran için bağımsız ve tutarsız renk veya ölçü değerleri kullanılmayacaktır.
27. Ultra premium görünüm, okunabilirlik ve kullanım kolaylığından üstün tutulmayacaktır.
28. Güvenlik durumları yalnızca renklerle ifade edilmeyecektir.
29. Renk körlüğü ve görme güçlüğü olan kullanıcılar için metin ve simge desteği sağlanacaktır.
30. Kritik düğmeler Apple’ın erişilebilir dokunma alanı ilkelerine uygun olacaktır.

E. V1 EKRAN TASARIM LİSTESİ

Kesin ekran envanteri nihai şartnameden oluşturulacaktır. Başlangıç tasarım kapsamı aşağıdaki ekran gruplarından oluşacaktır.

GRUP 01 — KARŞILAMA VE HESAP

* Açılış ekranı.
* Karşılama.
* Uygulama tanıtımı.
* Kullanıcı rolü seçimi.
* Ebeveyn hesabı oluşturma.
* Yetişkin hesabı girişi.
* Hesap kurtarma.
* Gizlilik bilgilendirmesi.
* Konum izin rehberi.
* Bildirim izin rehberi.

GRUP 02 — AİLE KURULUMU

* Aile oluşturma.
* Aileye katılma.
* Yetişkin daveti.
* Çocuk profili oluşturma.
* QR kod gösterme.
* QR kod tarama.
* Manuel eşleştirme.
* Çift taraflı eşleştirme onayı.
* Başarılı eşleştirme.
* Başarısız veya süresi dolmuş eşleştirme.
* Yeni cihaz eşleştirme.
* Kayıp cihaz erişimini iptal etme.

GRUP 03 — EBEVEYN ANA EKRANI

* Aile haritası.
* Aile üyesi listesi.
* Aile üyesi detay paneli.
* Son konum bilgisi.
* Konum doğruluğu.
* Konum geçmişi.
* Düşük pil durumu.
* Eski konum durumu.
* Bağlantı kesintisi.
* Konum paylaşımı kapalı durumu.
* Güvenli bölge izleme kapalı durumu.

GRUP 04 — ÇOCUK MODU

* Çocuk ana ekranı.
* SOS düğmesi.
* Beni almaya gel.
* Güvendeyim.
* Acil durum kişileri.
* Güvenlik ve gizlilik ekranı.
* Konumumu kimler görebilir?
* Paylaşım durumu.
* Konum izin durumu.
* Olay bazlı hazır yanıtlar.

GRUP 05 — SOS VE ACİL YARDIM

* SOS başlatma.
* SOS gönderiliyor.
* Konum alınıyor.
* Sunucu tarafından kaydedildi.
* Bildirim sağlayıcısına iletildi.
* Aile üyesi tarafından görüldü.
* Yardım talebi onaylandı.
* Gönderilemedi.
* Çevrimdışı SOS.
* SMS yedekleme.
* Acil telefon araması.
* Gelen SOS bildirimi.
* Aktif yardım talebi.
* SOS sonlandırma.

GRUP 06 — GÜVENLİ BÖLGELER

* Güvenli bölge listesi.
* Yeni bölge ekleme.
* Haritadan konum seçme.
* Bölge yarıçapı.
* Bölge adı ve simgesi.
* Takip edilecek aile üyeleri.
* Bildirim tercihleri.
* Bölge düzenleme.
* Bölge silme.
* Bölge kapasitesi.
* Bölge izleme hatası.

GRUP 07 — TEMEL AİLE GÜVENLİĞİ

* Güvendeyim bildirimi.
* Beni almaya gel isteği.
* Gelen alma isteği.
* İstek kabulü.
* İstek iptali.
* Hazır yanıtlar.
* Güvenlik bildirimleri.
* Olay geçmişi.
* Düşük pil bildirimi.

GRUP 08 — PREMIUM VE ABONELİK

* Ücretsiz ve Premium karşılaştırması.
* Aylık ve yıllık plan seçimi.
* Satın alma ekranı.
* Başarılı satın alma.
* Başarısız satın alma.
* Aile zaten Premium durumu.
* Mükerrer satın alma bilgilendirmesi.
* Satın alım geri yükleme.
* Abonelik yönetimi.
* Yedi günlük geçiş süreci.
* Ücretsiz kalacak 3 profilin seçilmesi.
* Ücretsiz kalacak 2 bölgenin seçilmesi.
* Premium sona erme bilgilendirmesi.

GRUP 09 — AYARLAR VE GİZLİLİK

* Profil ayarları.
* Aile yönetimi.
* Aile üyesi yetkileri.
* Cihaz yönetimi.
* Konum paylaşım tercihleri.
* Bildirim ayarları.
* Acil durum kişileri.
* Dil seçimi.
* Görünüm seçimi.
* Gizlilik merkezi.
* Veri ve hesap yönetimi.
* Hesap silme.
* Aileden ayrılma.
* Yardım ve destek.
* Yasal belgeler.

31. Bu liste ekran ve durum envanteri için başlangıç kaynağıdır.
32. Her madde ayrı bir ekran olmak zorunda değildir.
33. Birden fazla durum aynı ekranın farklı varyantları olarak tasarlanabilir.
34. Gereksiz ekran sayısını artıran kullanıcı akışları oluşturulmayacaktır.
35. Nihai ekran envanteri ürün direktörü tarafından onaylanacaktır.

F. SOS TASARIMINDA ÖZEL GÜVENLİK KURALLARI

36. SOS düğmesi kolay bulunabilir olacaktır.
37. SOS işlemi tek elle kullanılabilecektir.
38. Yanlışlıkla SOS başlatma ihtimali azaltılacaktır.
39. Basılı tutma, kısa iptal penceresi veya benzeri mekanizmalar gerçek cihazlarda karşılaştırılacaktır.
40. Yardım göndermeyi gereksiz yere geciktiren çok aşamalı onay ekranları kullanılmayacaktır.
41. VoiceOver kullanıcıları SOS işlemini tamamlayabilecektir.
42. Büyük yazı boyutunda kritik düğmeler erişilebilir kalacaktır.
43. SOS durumları birbirinden açıkça ayrılacaktır.
44. Başarısız gönderim başarılı görünmeyecektir.
45. Konum alınamadığında SOS kullanılamaz hale gelmeyecektir.
46. SMS ve telefon araması seçenekleri kolay erişilebilir olacaktır.
47. SOS ekranında reklam veya Premium satın alma teklifi bulunmayacaktır.
48. Resmî acil yardım hizmeti ile FamilyGuard arasındaki fark açıkça belirtilecektir.
49. SOS ekranı yalnızca estetik değerlendirmeyle onaylanmayacaktır.
50. Gerçek cihaz kullanılabilirlik testleri zorunlu olacaktır.

G. TASARIM ONAY SÜRECİ

Her ekran veya ekran grubu aşağıdaki süreçten geçecektir:

1. Ürün mekaniklerinin tanımlanması.
2. Kullanıcı akışının hazırlanması.
3. Görsel tasarımın oluşturulması.
4. Ürün direktörü değerlendirmesi.
5. Gerekli revizyonlar.
6. Proje sahibi görsel onayı.
7. Teknik uygulanabilirlik değerlendirmesi.
8. Nihai tasarımın kilitlenmesi.
9. Claude tarafından kodlanması.
10. Tasarımla kodlanmış ekranın karşılaştırılması.
11. Gerçek cihaz testi.
12. Kabul veya düzeltme kararı.
13. Claude’a her görevde ilgili onaylı tasarım referansları verilecektir.
14. Onaylı ekran referansları proje klasöründe saklanacaktır.
15. Kodlanmış ekranların ekran görüntüleri tasarım referanslarıyla karşılaştırılacaktır.
16. Claude, tasarım değişikliklerini teknik kolaylık gerekçesiyle kendi başına uygulamayacaktır.
17. Uygulanması mümkün olmayan tasarım detayları açıkça raporlanacaktır.
18. Tasarım değişiklikleri ilgili referans dosyalarına da işlenecektir.

H. LOKALİZASYON MİMARİSİ

57. Lokalizasyon mimarisi Faz 1’den itibaren zorunlu olacaktır.
58. Swift String Catalog kullanılacaktır.
59. Kullanıcıya gösterilen hiçbir ürün metni kaynak kod içerisinde sabit olarak yazılmayacaktır.
60. Erişilebilirlik etiketleri de lokalizasyon kapsamında olacaktır.
61. Hata mesajları lokalizasyon kapsamında olacaktır.
62. Bildirim metinleri lokalizasyon kapsamında olacaktır.
63. İzin açıklamaları ve sistem izin metinleri de uygun kaynak dosyaları üzerinden yerelleştirilecektir.
64. Sunucu kaynaklı olaylar sabit İngilizce veya Türkçe hata metinlerine bağımlı olmayacaktır.
65. Sunucu olay kodları ve gerekli parametreleri gönderecek, uygulama uygun yerelleştirilmiş metni gösterecektir.
66. Tarih, saat, mesafe, fiyat ve sayılar kullanıcının yerel biçimine göre gösterilecektir.
67. Çoğul ekleri ve dilbilgisi kuralları String Catalog yetenekleriyle yönetilecektir.
68. Kelime parçalarını birleştirerek cümle oluşturma yaklaşımından kaçınılacaktır.
69. Sağdan sola diller ilk günden mimari olarak desteklenecektir.
70. Uzun Almanca metinler ve Arapça düzen gibi farklı dil koşulları tasarım testlerine dahil edilecektir.
71. Türkçe ve İngilizce pilot dilleri başlangıçtan itibaren doldurulacaktır.
72. Diğer 19 dil Faz 7’de tamamlanacaktır.
73. Genel yayın için 21 dil desteği hedefi korunacaktır.
74. Güvenlik, SOS, gizlilik, izin ve abonelik metinleri 21 dilde yetkin insan kontrolünden geçirilecektir.
75. Eksik güvenlik metni veya yanlış kritik çeviri yayın engeli olacaktır.
76. İnsan kontrollü çeviri giderleri ayrıca bütçelendirilecektir.

I. GÜNCEL GELİŞTİRME SIRASI

HAZIRLIK AŞAMASI

* Karar 01–11 birleştirme.
* Nihai şartname oluşturma.
* Çelişki denetimi.
* Ürün kapsamı kilidi.
* Sekiz marka adayı araştırması.
* Marka seçimi.
* Gerekli marka ve alan adı kontrolleri.

FAZ 0 — TEKNİK VE HUKUKİ FİZİBİLİTE

* Supabase standart sözleşme görüşmeleri.
* Hukuki uzman incelemesi.
* Sentetik veriyle teknik prototip.
* Konum motoru fizibilitesi.
* Pil tüketimi ölçüm yöntemi.
* SOS ve çevrimdışı iletişim fizibilitesi.
* Critical Alerts başvurusu için gerekli hazırlıklar.
* İki gerçek iPhone test altyapısı.

TASARIM AŞAMASI — FAZ D

* Marka görsel kimliği.
* Logo ve uygulama ikonu.
* Tasarım sistemi.
* Kullanıcı akışları.
* Bütün V1 ekranlarının tasarımı.
* Kritik ekran durumları.
* Görsel varlıklar.
* Erişilebilirlik tasarımı.
* SOS kullanılabilirlik değerlendirmesi.
* Ürün direktörü ve proje sahibi onayı.

Faz 0 teknik prototipleri ile Faz D hazırlıkları, bağımlılıkları uygun olduğu sürece paralel ilerleyebilecektir.

FAZ 1 — Hesap, aile ve cihaz güvenliği.

FAZ 2 — Adaptif konum motoru ve aile haritası.

FAZ 3 — Güvenli bölgeler ve bildirimler.

FAZ 4 — SOS ve yedek iletişim.

FAZ 5 — Temel aile güvenliği.

FAZ 6 — StoreKit 2 ve abonelik ekonomisi.

FAZ 7 — Arayüz cilası ve lokalizasyon tamamlama.

FAZ 8 — Güvenlik, gerçek cihaz ve yük testleri.

FAZ 9 — Hukuki yayın kontrolü ve TestFlight.

FAZ 10 — App Store yayın hazırlığı.

77. Faz 1–6 arasında ekranlar geçici ürün arayüzleriyle kodlanmayacaktır.
78. Faz 1–6 arasında onaylı tasarım referansları kullanılacaktır.
79. Faz 7’de ekranların baştan tasarlanması veya topluca yeniden yazılması planlanmayacaktır.
80. Faz 7 yalnızca görsel kalite kontrolü, animasyon, ince ayar, erişilebilirlik iyileştirmeleri ve lokalizasyonun tamamlanması için kullanılacaktır.
81. Teknik veya güvenlik nedeniyle gerekli tasarım değişiklikleri karar kaydıyla gerçekleştirilecektir.

J. TASARIM DOSYA YAPISI

Önerilen proje dosya düzeni:

* docs/DESIGN-SYSTEM.md
* docs/SCREEN-INVENTORY.md
* docs/USER-FLOWS.md
* docs/LOCALIZATION.md
* design-reference/brand/
* design-reference/screens/
* design-reference/icons/
* design-reference/components/
* design-reference/states/
* assets/branding/
* assets/icons/
* assets/illustrations/
* docs/QA/design/

82. Her ekranın benzersiz referans kimliği bulunacaktır.
83. Her ekranın onay durumu kayıt altına alınacaktır.
84. Güncel ve eski tasarım dosyaları birbirinden ayrılacaktır.
85. Kodlama ajanı yalnızca güncel ve onaylı tasarım referanslarını kullanacaktır.

K. EK KABUL KRİTERLERİ

* Tasarım sistemi onaylandı.
* V1 ekran envanteri oluşturuldu.
* Kritik ekran durumları tanımlandı.
* Kodlanan ekranlar onaylı referanslarla uyumlu.
* Küçük ekranlı iPhone testi başarılı.
* Büyük ekranlı iPhone testi başarılı.
* Açık ve koyu görünüm testi başarılı.
* Dynamic Type testi başarılı.
* VoiceOver ile temel güvenlik akışları başarılı.
* Sağdan sola dil düzeni başarılı.
* Uzun çevirilerde taşma bulunmuyor.
* Kullanıcıya görünen sabit ürün metni bulunmuyor.
* SOS tek elle kullanılabiliyor.
* SOS başarısızlık durumları doğru gösteriliyor.
* SMS ve acil arama seçeneklerine kolay erişiliyor.
* Kritik metinler insan kontrolünden geçmiş.
* Premium satın alma ekranı yalnızca mevcut özellikleri gösteriyor.
* Onaylanmamış ekran tasarımı kullanılmıyor.

Güvenliği veya temel işlevleri etkileyen tasarım ve erişilebilirlik başarısızlıkları yayın engeli olacaktır.

Kritik olmayan küçük görsel kusurlar Karar 09 kapsamındaki P2 sınıfına alınabilecektir.

L. PROJE KAPSAMI VE EKONOMİ

Karar 11 yeni bir ürün özelliği eklememektedir.

Aşağıdaki kurallar değişmemiştir:

* V1 kapsamındaki sekiz temel modül.
* iOS V1.
* V1.1 ek özellikler.
* Android V1.5.
* V2 dijital ebeveyn kontrolü.
* 21 dil desteği.
* Ücretsiz 3 aktif konum profili.
* Premium 10 aktif konum profili.
* Ücretsiz 2 güvenli bölge.
* Premium 18 güvenli bölge.
* Ücretsiz 24 saat geçmiş.
* Premium 30 gün geçmiş.
* Ücretsiz temel güvenlik katmanı.
* Aylık 5,99 USD.
* Yıllık 39,99 USD.
* Reklamsız kullanım.

M. NİHAİ ŞARTNAME SÜRECİ

Claude’un ürün şartnamesine ilişkin son itirazı değerlendirilmiştir.

Karar 01–11 kapsamında ürün mekanikleri, güvenlik, ekonomi, teknik mimari, marka ve geliştirme yöntemi üzerinde mutabakat sağlanmıştır.

Bundan sonraki işlem sırası:

1. Sekiz aday marka ismini araştır.
2. Her aday için Karar 10 değerlendirme tablosunu hazırla.
3. Doğrulanmış sonuçları belirsiz sonuçlardan ayır.
4. Marka adaylarını ürün direktörüne sun.
5. Nihai marka seçimini proje sahibinin onayına bırak.
6. Karar 01–11’i tek bir güncel nihai şartnamede birleştir.
7. Yürürlükten kalkmış ve çelişen kuralları temizle.
8. V1 kapsamını ve kabul kriterlerini kesinleştir.
9. Nihai şartnameyi ürün direktörünün denetimine sun.
10. Onay sonrasında teknik fizibilite ve tasarım aşamasına geç.

Nihai şartname birleştirilmeden ve onaylanmadan üretim kodlamasına başlanmayacaktır.

TEMEL TASARIM İLKESİ

FamilyGuard’ın yeni markası altında geliştirilecek uygulama, ultra premium görünümü güvenilirlik, erişilebilirlik ve sadelikle birleştirecektir.

Önce karar, sonra tasarım, ardından uygulama ve kalite kontrol.

Karar 11: ONAYLANDI.

Ürün şartnamesi itiraz aşaması: TAMAMLANDI.

Marka seçimi: BEKLİYOR.

Nihai şartname birleştirme: BEKLİYOR.

Kodlama durumu: BAŞLANMAYACAK.

Karar 01–11 kabul edilmiştir.

Şimdi Karar 10 kapsamında sekiz marka adayı araştırmasını sunabilirsin.


---

## KARAR 12 [TAM METİN]

**FAMILYGUARD — KARAR 12 / NİHAİ ŞARTNAME AÇIK KONULARININ ÇÖZÜMLENMESİ**

**Karar durumu: AÇIK KONULAR ONAYLANDI — NİHAİ BELGE DENETİMİ BEKLİYOR**

**A. KONUM TAZELİĞİ VE HAREKETSİZ CİHAZLAR**

1. Sabit 10 dakikalık konum eskime kuralı bütün hareket profillerine uygulanmayacaktır.
2. Adaptif konum motorunun enerji tasarrufu ilkesi korunacaktır.
3. Aşağıdaki zaman bilgileri birbirinden ayrı tutulacaktır:

- Son başarılı GPS ölçümü.
- Son doğrulanmış hareket bilgisi.
- Son doğrulanmış hareketsizlik bilgisi.
- Son başarılı sunucu iletişimi.
- Son konum izni durumu.

4. Yeni GPS ölçümü yapılmadığında ölçüm zamanı güncellenmeyecektir.
5. Sunucu iletişiminin devam etmesi, konumun güncel olduğunu tek başına kanıtlamayacaktır.
6. Hareket algılanmaması, kişinin kesinlikle aynı konumda bulunduğunun kanıtı sayılmayacaktır.
7. Kullanıcıya gerektiğinde aşağıdaki gibi bilgiler gösterilecektir:

"Son konum ölçümü 35 dakika önce."

"Son hareket bilgisi 3 dakika önce: hareket algılanmadı."

8. Yeni bir konum ölçümü bulunmadığında eski konum güncel konum olarak gösterilmeyecektir.
9. Hareketsiz cihazlar yalnızca eski konum uyarısını önlemek için sürekli GPS ölçümüne zorlanmayacaktır.
10. Haritayı açan ebeveyn, diğer cihazda zorunlu GPS ölçümünü tetiklemeyecektir.
11. Dinlenme, normal hareket ve SOS profillerinin tazelik eşikleri Faz 0 gerçek cihaz ölçümleriyle belirlenecektir.
12. Yanlış güncel konum gösterimi P0 yayın engeli olacaktır.

**B. ÇEVRİMDIŞI SOS KUYRUĞU**

13. Bekleyen SOS olayları için başlangıç geçerlilik süresi 15 dakika olarak belirlenecektir.
14. Bu süre Faz 0 testlerinde güvenlik ve kullanılabilirlik açısından değerlendirilecektir.
15. SOS başlatıldığı anda yerel olay kimliği oluşturulacaktır.
16. Olayın gerçek oluşturulma zamanı korunacaktır.
17. İnternet bağlantısı bulunmadığında SMS ve telefon araması seçenekleri hemen gösterilecektir.
18. Kullanıcıya SOS'un henüz sunucuya ulaşmadığı açıkça bildirilecektir.
19. Geçerlilik süresi içinde bağlantı sağlanırsa aktif ve iptal edilmemiş SOS otomatik gönderilebilecektir.
20. Gecikmeli gönderimlerde olayın gerçek oluşturulma zamanı ve gönderim gecikmesi korunacaktır.
21. Kullanıcı tarafından iptal edilmiş SOS hiçbir koşulda yeniden gönderilmeyecektir.
22. Süresi dolan ve sunucuya hiç ulaşmamış SOS otomatik gönderilmeyecektir.
23. Uygulama açıldığında kullanıcıya şu seçenek sunulacaktır:

"Önceki yardım talebiniz gönderilemedi. Hâlâ yardıma ihtiyacınız var mı?"

- Yeni SOS gönder.
- Talebi kapat.
- SMS gönder.
- Telefonla ara.

24. Yeni SOS ayrı olay kimliğiyle oluşturulacaktır.
25. Süresi dolan bekleyen SOS ile sunucuda kayıtlı aktif SOS birbirine karıştırılmayacaktır.
26. Sunucuda kayıtlı aktif SOS yalnızca çevrimdışı kuyruk süresi dolduğu gerekçesiyle kapatılmayacaktır.
27. Sunucuya ulaşmış fakat istemci tarafından yanıtı alınamamış olaylar idempotent sorgulama ile doğrulanacaktır.
28. Süresi dolmuş, iptal edilmiş ve mükerrer SOS senaryoları P0 test kapsamına alınacaktır.

**C. DÜZENLİ KONUM PAYLAŞIMI AKTİF OLMAYAN ÜYELER**

Temel güvenlik özelliklerinin ücretsiz ve abonelikten bağımsız olması ilkesi korunacaktır.

**GÜVENDEYİM**

29. Düzenli konum paylaşımı kapalı üyeler de Güvendeyim bildirimi gönderebilecektir.
30. Konum paylaşılması zorunlu olmayacaktır.
31. Kullanıcı isterse mevcut izinler kapsamında tek seferlik konum ekleyebilecektir.
32. Konum ekleme seçeneği varsayılan olarak kapalı olacaktır.
33. Konum eklenmemesi bildirimin gönderilmesini engellemeyecektir.
34. Güvendeyim bildirimi sürekli konum takibini yeniden başlatmayacaktır.
35. Bildirim, kişinin güvenliğinin sistem tarafından doğrulandığı anlamına gelmeyecektir.

**BENİ ALMAYA GEL**

36. Beni almaya gel özelliği temel yardım talebi olarak kabul edilecektir.
37. Bütün yetkili aile üyeleri tarafından ücretsiz kullanılabilecektir.
38. Kullanıcı mevcut izinleri kapsamında bulunduğu konumu paylaşabilecektir.
39. Konum alınamaması yardım talebini engellemeyecektir.
40. Paylaşım yalnızca ilgili yardım olayı ve yetkili alıcılarla sınırlı olacaktır.
41. Talep tamamlandığında veya iptal edildiğinde geçici konum erişimi sona erecektir.
42. V1 kapsamında bu özellik sürekli yolculuk takibine dönüşmeyecektir.

**DÜŞÜK PİL BİLDİRİMİ**

43. Düşük pil bildirimi temel ücretsiz güvenlik özelliği olarak korunacaktır.
44. Düzenli konum paylaşımı kapalı üyelerde de işletim sisteminin izin verdiği ölçüde çalışacaktır.
45. Düşük pil bilgisini almak için GPS motoru yeniden başlatılmayacaktır.
46. Yalnızca pil durumunu kontrol etmek amacıyla gereksiz arka plan işlemleri oluşturulmayacaktır.
47. iOS uygulamanın çalışmasına izin vermediğinde pil değişikliklerinin anlık algılanması garanti edilmeyecektir.
48. Başlangıç düşük pil eşiği yüzde 20 olacaktır.
49. Aynı düşük pil olayı nedeniyle sürekli tekrar bildirim gönderilmeyecektir.
50. Pil verisi paylaşımı ayrı güvenlik ve gizlilik tercihlerine tabi olacaktır.
51. Son pil ölçümünün zamanı gerektiğinde gösterilecektir.
52. Bu özelliklerin hiçbiri Premium düzenli konum profili kapasitesini tüketmeyecektir.

**D. PREMIUM 7 GÜNLÜK GEÇİŞ MEKANİZMASI**

53. Yedi günlük ürün geçiş hakkı aile bazında tanımlanacaktır.
54. Başlangıç kuralı olarak bir aile, 365 günlük hareketli dönem içerisinde en fazla bir kez ücretsiz ürün geçiş süresi kullanabilecektir.
55. Yönetici değişikliği, cihaz değişikliği veya abonelik sahibinin değişmesi bu hakkı sıfırlamayacaktır.
56. Yeni bir abonelik işlemi tek başına yeni geçiş hakkı oluşturmayacaktır.
57. Bu kural pilot kullanım sonuçlarına göre ürün direktörü tarafından yeniden değerlendirilebilecektir.

Geçiş davranışları:

**Normal abonelik iptali:**

- Ödenmiş abonelik dönemi sonuna kadar Premium devam eder.
- Dönem sona erdiğinde uygun aileler için 7 günlük ürün geçişi başlar.

**Ödeme başarısızlığı:**

- Mağazanın doğrulanmış Billing Grace Period durumu varsa ilgili mağaza hakkı korunur.
- Mağaza kaynaklı geçerli Premium hakkı sona ermeden ürün geçiş süresi başlatılmaz.
- Ödeme başarısızlığı sonucunda abonelik hakkı kesin olarak sona erdiğinde uygun aileler için ürün geçişi uygulanabilir.

**İade veya mağaza tarafından hak geri alınması:**

- Doğrulanmış mağaza kararı uygulanır.
- Otomatik 7 günlük ürün geçişi oluşturulmaz.

**Sahte satın alma veya kötüye kullanım:**

- Geçersiz Premium hakkı kaldırılır.
- Yeni geçiş süresi oluşturulmaz.
- Temel ücretsiz güvenlik özellikleri korunur.

58. Apple Billing Grace Period ile FamilyGuard ürün geçişi teknik ve görsel olarak ayrı tutulacaktır.
59. Ürün geçişi hiçbir şekilde mağaza aboneliğinin uzatıldığı anlamına gelmeyecektir.
60. Geçiş süresinde yeniden geçerli Premium satın alınırsa abonelik hakkı doğru şekilde etkinleştirilecektir.
61. Kullanılmış geçiş hakkı yeniden satın alma nedeniyle sıfırlanmayacaktır.
62. Geçiş hakkı bulunmayan aileler ücretsiz pakete düşürülecektir.
63. Ailelerin ücretsiz pakette kalacak 3 aktif profil ve 2 güvenli bölge tercihlerini Premium kullanırken önceden belirleyebilmeleri sağlanacaktır.
64. Geçiş hakkı olmasa bile mevcut aile üyeleri otomatik olarak aileden çıkarılmayacaktır.
65. SOS ve temel güvenlik hakları bütün abonelik durumlarında korunacaktır.
66. Geçiş kuralları satın alma öncesinde açıkça gösterilecektir.
67. Abonelik sona ermesi ve hak hesaplama işlemleri sunucu otoritesinde gerçekleştirilecektir.

**E. VDOX LAB DESTEK ALTYAPISI**

68. Yeni uygulama için bağımsız alan adı satın alınmayacaktır.
69. Mevcut VDOX Lab web altyapısı kullanılacaktır.
70. Destek e-posta adresi için önerilen standart:

support@vdoxlab.com

71. Bu adresin kullanılabilmesi mevcut alan adı sahipliği, posta altyapısı ve adresin aktif çalışmasının doğrulanmasına bağlıdır.
72. Doğrulanmamış e-posta adresi uygulamada veya App Store kayıtlarında kullanılmayacaktır.
73. VDOX Lab uygulamaları ortak destek adresini kullanabilir.
74. Destek talepleri ürün bazında sınıflandırılacaktır.
75. Gizlilik ve kişisel veri talepleri ayrı iş akışıyla yönetilecektir.
76. Destek taleplerinde çocukların konum bilgileri, şifreler veya oturum tokenları istenmeyecektir.
77. E-posta üzerinden acil yardım müdahalesi sağlandığı izlenimi oluşturulmayacaktır.
78. Destek hizmetinin 7/24 canlı acil müdahale merkezi olmadığı açıkça belirtilecektir.
79. Gizlilik politikası, kullanım koşulları, destek ve hesap silme sayfaları VDOX Lab web altyapısında oluşturulacaktır.
80. Kesin destek adresi ve sayfa bağlantıları yayın hazırlığı öncesinde doğrulanacaktır.

**F. REALTIME YÜZDE 90 TASARRUF HEDEFİ**

81. Realtime mesaj hacminde yüzde 90 azaltma hedefi korunacaktır.
82. Bu hedef doğrudan P0 veya P1 yayın engeli olarak sınıflandırılmayacaktır.
83. Bu oran ölçülmüş sonuç elde edilmeden garanti edilmiş tasarruf olarak gösterilmeyecektir.
84. Realtime mesaj azalması toplam Supabase faturasının aynı oranda azalması anlamına gelmeyecektir.
85. Harita izleyicisi bulunmadığında gereksiz konum Broadcast üretmeme kuralı zorunlu kalacaktır.
86. İzleyici oturumunun sona ermesi, lease süresi ve bağlantı kesintisi davranışları ayrıca test edilecektir.
87. SOS ve güvenlik bildirimleri Realtime maliyet optimizasyonundan olumsuz etkilenmeyecektir.
88. Aşağıdaki değerler Faz 0 ve Faz 8 raporlarında ölçülecektir:

- Aile başına günlük konum kaydı.
- Aile başına günlük Broadcast mesajı.
- Aktif harita izleme süresi.
- İzleyici bulunmayan süre.
- Eşzamanlı bağlantı sayısı.
- Veritabanı işlem hacmi.
- Veri transferi.
- Push bildirim hacmi.
- Ücretsiz ve Premium aile başına tahmini maliyet.

89. Tasarruf oranı aynı kullanıcı davranışı ve konum güncelleme hacmine sahip karşılaştırılabilir referans model üzerinden hesaplanacaktır.
90. Yüzde 90 hedefinin karşılanmaması tek başına yayın engeli olmayacaktır.
91. Ancak yanlış yetkilendirme, gereksiz Broadcast üretimi veya kontrolsüz altyapı maliyeti ayrı teknik sorun olarak değerlendirilecektir.
92. Ekonomi modelinin sürdürülebilir olmadığı tespit edilirse ürün direktörünün değerlendirmesi olmadan genel yayına geçilmeyecektir.

**G. NİHAİ ŞARTNAME GÜNCELLEMESİ**

93. Bu kararlar Bölüm 18.B'deki altı açık konunun yerine işlenecektir.
94. Eski ve çelişen maddeler nihai şartnameden çıkarılacaktır.
95. Faz 0 ölçümüne bırakılan parametreler kesinleşmiş teknik sonuç olarak gösterilmeyecektir.
96. Karar 12 ayrı karar geçmişine kaydedilecektir.
97. V1 kapsamına yeni bağımsız ürün modülü eklenmeyecektir.
98. Nihai belge yeniden ürün direktörüne sunulacaktır.
99. Nihai şartname denetimi tamamlanmadan kapsam kilidi kesinleştirilmeyecektir.
100. Üretim kodlaması başlatılmayacaktır.

**H. DEĞİŞMEYEN ÜRÜN KARARLARI**

- iOS V1.
- Android V1.5.
- Sekiz temel V1 modülü.
- 21 dil desteği.
- Soft Premium tasarım.
- VDOX Lab web altyapısı.
- Ücretsiz 3 aktif konum profili.
- Premium 10 aktif konum profili.
- Ücretsiz 2 güvenli bölge.
- Premium 18 güvenli bölge.
- Ücretsiz 24 saat konum geçmişi.
- Premium 30 gün konum geçmişi.
- Aylık 5,99 USD.
- Yıllık 39,99 USD.
- Reklamsız kullanım.
- Ücretsiz temel güvenlik katmanı.
- Tasarım onayı olmadan ekran kodlamama kuralı.

**Karar 12: ONAYLANDI.**

**Nihai şartname: TAM BELGE DENETİMİ BEKLİYOR.**

**Marka adı: KOŞULLU OLARAK WINGFOLD, NİHAİ SEÇİM BEKLİYOR.**

**Üretim kodlaması: BAŞLANMAYACAK.**

Altı açık konuyu güncelle ve birleştirilmiş nihai şartnameyi tam belge olarak tekrar sun.


---

## KARAR 13 [TAM METİN]

**FAMILYGUARD — KARAR 13 / ABONELİK GEÇİŞ HAKKI VE DESTEK ADRESİ**

**Karar durumu: ONAYLANDI**

Karar 12 denetiminde tespit edilen iki açık konu aşağıdaki şekilde çözümlenmiştir.

**A. Abonelik sahibinin aileden ayrılması**

1. Abonelik sahibinin aileden ayrılması durumunda eski aileye uygulanabilecek 7 günlük geçiş süresi, Karar 12 kapsamındaki ortak yıllık geçiş hakkına tabi olacaktır.

2. Her aile, 365 günlük hareketli dönem içerisinde en fazla bir kez 7 günlük ücretsiz Premium ürün geçişi kullanabilecektir.

3. Aşağıdaki olaylar aynı ortak geçiş hakkı üzerinden değerlendirilecektir:

- Normal abonelik süresinin sona ermesi.
- Ödeme başarısızlığı sonrasında mağaza kaynaklı Premium hakkının kesin olarak sona ermesi.
- Abonelik sahibinin aileden ayrılması sonucunda ailenin geçerli Premium hakkını kaybetmesi.

4. Her olay için bağımsız geçiş hakkı oluşturulmayacaktır.

5. Ailenin geçerli başka bir Premium aboneliği bulunuyorsa ürün geçişi başlatılmayacaktır.

6. Ortak geçiş hakkı daha önce kullanılmışsa ve 365 günlük dönem henüz dolmamışsa aile ücretsiz pakete düşürülecektir.

7. Abonelik sahibinin aileden ayrılması ve tekrar katılması geçiş hakkını sıfırlamayacaktır.

8. Yönetici değişikliği, cihaz değişikliği veya yeni abonelik satın alınması geçiş hakkını sıfırlamayacaktır.

9. Geçiş süresi başladıktan sonra aynı aile için ikinci bir geçiş süresi başlatılarak süre uzatılmayacaktır.

10. Geçiş hakkının tüketilmesi ve abonelik durumunun güncellenmesi sunucu tarafında atomik ve idempotent olarak gerçekleştirilecektir.

11. Abonelik sahibinin aileden ayrılma hakkı ticari gerekçelerle engellenmeyecektir.

12. Ayrılan kişinin eski ailenin kişisel verilerine erişimi derhal kaldırılacaktır. Yedi günlük ürün geçişi, ayrılan kişiye veri erişim yetkisi sağlamayacaktır.

13. Ücretsiz pakete düşürülen ailelerde:

- Mevcut aile üyelikleri korunacaktır.
- SOS hakları korunacaktır.
- Temel güvenlik özellikleri korunacaktır.
- Düzenli konum paylaşımı 3 aktif profille sınırlandırılacaktır.
- Güvenli bölge kapasitesi 2 olacaktır.
- Konum geçmişi 24 saatlik saklama politikasına tabi olacaktır.
- Önceden belirlenmiş aktif profil ve bölge seçimleri uygulanacaktır.
- Aktif yardım olayları yalnızca abonelik değişikliği nedeniyle yarıda kesilmeyecektir.

14. İade, mağaza tarafından hak geri alınması ve doğrulanmış kötüye kullanım durumları otomatik geçiş hakkı oluşturmayacaktır.

15. Karar 06 ve Karar 12 arasındaki çelişen hükümler bu güncel kurallarla değiştirilecektir.

**B. Destek e-posta adresi**

16. VDOX Lab uygulamalarında kullanılan mevcut genel iletişim adresi tercih edilmiştir:

info@vdoxlab.com

17. support@vdoxlab.com adresi oluşturulmayacaktır.

18. Mevcut adresin aktif çalıştığı yayın öncesinde gönderme ve alma testleriyle doğrulanacaktır.

19. Uygulama içindeki destek ekranında, App Store kayıtlarında ve ilgili VDOX Lab ürün sayfalarında doğrulanmış iletişim adresi kullanılacaktır.

20. Destek talepleri ürün bazında sınıflandırılacaktır.

21. Gizlilik ve kişisel veri talepleri ayrı iş akışıyla yönetilecektir.

22. E-posta desteğinin acil müdahale hizmeti olmadığı açıkça belirtilecektir.

23. Karar 12 kapsamındaki diğer destek ve gizlilik kuralları korunacaktır.

**C. Ek kabul testleri**

Aşağıdaki senaryolar M07 ve ilgili güvenlik testlerine eklenecektir:

- Abonelik sahibinin geçiş hakkı bulunan aileden ayrılması.
- Abonelik sahibinin geçiş hakkını kullanmış aileden ayrılması.
- Ayrılma ve yeniden katılma döngüsü.
- Aynı ailede farklı abonelik sahiplerinin değişmesi.
- Ailenin başka geçerli Premium aboneliğine sahip olması.
- Normal abonelik bitişi ve ayrılma olaylarının aynı anda gerçekleşmesi.
- Mükerrer olayların yeni geçiş hakkı oluşturmaması.
- Mevcut geçiş süresinin yeniden başlatılamaması veya uzatılamaması.
- Ayrılan kişinin eski aile verilerine erişememesi.
- Ücretsiz pakete geçişte SOS ve temel güvenlik özelliklerinin korunması.
- Destek adresinin gönderme ve alma testleri.

Abonelik haklarının yanlış hesaplanması P1, yetkisiz kişisel veri erişimi veya temel güvenlik özelliklerinin kaybedilmesi P0 yayın engeli olarak sınıflandırılacaktır.

**D. Nihai şartname güncellemesi**

24. Karar 13 nihai şartnameye işlenecektir.
25. Bölüm 18.C kapsamındaki iki açık konu kapatılacaktır.
26. Çelişen eski kurallar kaldırılacaktır.
27. Yeni ürün özelliği veya bağımsız modül eklenmeyecektir.
28. Karar 13 karar geçmişine kaydedilecektir.
29. Güncellenmiş nihai şartname tam belge olarak ürün direktörüne sunulacaktır.

**E. Değişmeyen kararlar**

- V1 sekiz temel modül.
- iOS V1 ve Android V1.5.
- 21 dil desteği.
- Soft Premium tasarım.
- VDOX Lab ortak web altyapısı.
- Ücretsiz temel güvenlik katmanı.
- Ücretsiz 3 aktif konum profili.
- Premium 10 aktif konum profili.
- Ücretsiz 2 güvenli bölge.
- Premium 18 güvenli bölge.
- Ücretsiz 24 saat konum geçmişi.
- Premium 30 gün konum geçmişi.
- Aylık 5,99 USD.
- Yıllık 39,99 USD.
- Reklamsız kullanım.
- Tasarım onayı olmadan ekran kodlamama kuralı.

**Karar 01–13: ONAYLI.**

**Açık iki ürün konusu: ÇÖZÜLDÜ.**

**Nihai şartname: TAM BELGE DENETİMİ BEKLİYOR.**

**Marka: Wingfold koşullu birinci aday.**

**Üretim kodlaması: BAŞLANMAYACAK.**

Karar 13'ü işle ve nihai şartnamenin güncel tam sürümünü sun.


---

## KARAR 14 — ÜRÜN KAPSAM KİLİDİ [ÖZET KAYIT]

- Durum: koşullu onay. Karar 01–13 onaylı; açık ürün konusu yok; V1 sekiz modülle sınırlı; yeni özellik eklenmeyecek; yeni fikirler yol haritasına.
- Kesinleşen parametreler: native SwiftUI, minimum iOS 17, Android V1.5, 21 dil, Soft Premium, açık/koyu görünüm, VDOX Lab ortak web altyapısı, info@vdoxlab.com, reklamsız, ücretsiz temel güvenlik, 3/10 profil, 2/18 bölge, 24 saat/30 gün geçmiş, 5,99/39,99 USD.
- Tam belgenin .md veya .txt olarak sunulması istendi; PDF/Word yanında Markdown sürümü saklanacak.
- Faz 0 konuları ve marka sonrası Faz D tasarım listesi belirlendi. Üretim kodlaması başlamayacak.


---

## NİHAİ ŞARTNAME DENETİMİ VE KAPSAM KİLİDİ ONAYI [TAM METİN]

**FAMILYGUARD — NİHAİ ŞARTNAME DENETİMİ VE KAPSAM KİLİDİ ONAYI**

**Denetlenen belge:** V1.1 — Revizyon 3.

Markdown ve TXT dosyalarının tam içeriği ürün direktörü tarafından incelenmiştir. İki dosyanın içerikleri birebir aynıdır.

**SONUÇ: ÜRÜN ŞARTNAMESİ ONAYLANDI.**

Karar 01–14 kapsamında belirlenen ürün mekanikleri, güvenlik ilkeleri, abonelik ekonomisi, marka stratejisi, tasarım yöntemi ve geliştirme yol haritası kabul edilmiştir.

Yeni ürün kararı veya özellik araştırması başlatılmayacaktır.

**A. Son editoryal ve teknik netleştirmeler**

Aşağıdaki düzeltmeler mevcut kararların uygulanmasını netleştirmek amacıyla yapılacaktır. Yeni ürün kapsamı oluşturmaz.

1. Bölüm 0 madde 2'deki Karar 01–11 ifadesini Karar 01–14 ve ilgili marka ek kararları olarak güncelle. Belge başlığındaki kaynak ve durum bilgilerini de güncelle.

2. M04 madde 21'deki otomatik yeniden gönderim ifadesini madde 26–30 ile açıkça ilişkilendir. Yalnızca geçerlilik süresi dolmamış, aktif ve iptal edilmemiş SOS otomatik gönderilebilir. Yanıt alınmamış olayın sunucu durumu idempotent olarak doğrulanır. İptal ve gönderimin eşzamanlı gerçekleşmesi durumunda olay yeniden aktif hale getirilemez.

3. M02-10, M03-06 ve Bölüm 7.3'te düzenli konum paylaşımı kapalı üyeler için konum yasağının düzenli takip kapsamında olduğunu açıkça belirt. Kullanıcı tarafından başlatılan izinli SOS, Güvendeyim ve Beni almaya gel olaylarının amaçla sınırlı konum paylaşımı korunacaktır. Bu olaylar sürekli takibi yeniden başlatmayacaktır.

4. M03-01 testini aktif ve süresi dolmamış yetkili izleyici kaydı bulunmadığında sıfır konum Broadcast mesajı olarak netleştir. Normal harita kapanışında izleyici kaydı sonlandırılır. Beklenmedik bağlantı kesilmesinde süreli izleyici kaydının sona ermesi dikkate alınır. Yetki iptali için lease süresinin dolması beklenmez.

5. Bölüm 10 madde 3'te sunucu olay kodu yaklaşımı ile uygulama kapalıyken görüntülenen APNs bildirimlerinin yerelleştirilmesini ayrı tanımla. APNs yerelleştirme anahtarları veya güvenli yerelleştirilmiş sunucu metinleri teknik olarak değerlendirilecektir. Push içeriklerine kişisel veri eklenmeyecektir.

6. Bölüm 4'te aile yöneticisi yetkisinin otomatik hukuki veli yetkisi oluşturmadığını açıkça belirt. Çocuk verilerine erişim ve çocuk cihaz yönetimi için ayrıca doğrulanmış ilişki ve gerekli yetkilendirme aranacaktır.

7. M08 saklama tablosunda hesap silme ve aileden ayrılmayı ayrı satırlarda tanımla. Aileden ayrılan kişinin eski aile verilerine erişimi hemen kaldırılacaktır. Aileden ayrılma bağımsız kullanıcı hesabının otomatik silinmesi anlamına gelmeyecektir. Eski aile ilişkisindeki verilerin saklama ve silme politikası hukuki değerlendirmeye tabi olacaktır.

8. M01-09 kabul testini çift taraflı onay olmadan eşleştirmenin tamamlanamaması ve konum paylaşımının başlatılamaması şeklinde güncelle.

9. SOS ve diğer geçici yardım olaylarında konum erişiminin sona ermesiyle ilgili testleri koru. Düzenli konum paylaşımının kapatılması, cihazın iptal edilmesi ve aileden ayrılma sonrasında bekleyen konum kayıtlarının yetkisiz yüklenemediğini doğrula.

10. SOS yüksek hassasiyet profilinin azami çalışma süresi, bekleyen yardım olaylarının geçici konum erişimi ve ilgili saklama sınırları Faz 0'da ölçülerek kesinleştirilecektir. Süresiz yüksek hassasiyetli GPS veya süresiz olay konumu erişimi oluşturulmayacaktır.

**B. Kapsam kilidi**

V1 kapsamı aşağıdaki sekiz modülle sınırlıdır:

M01 — Hesap, aile ve cihaz güvenliği.

M02 — Adaptif konum motoru.

M03 — Aile haritası.

M04 — SOS ve acil yardım.

M05 — Güvenli bölgeler.

M06 — Temel aile güvenliği.

M07 — Abonelik ve ekonomi.

M08 — Gizlilik ve hukuki uygunluk.

V1.1, V1.5 ve V2 kapsamındaki özellikler ilk yayın sürümüne eklenmeyecektir.

**C. Değişmeyecek ürün kararları**

- Native SwiftUI.
- Minimum iOS 17.
- Android V1.5.
- 21 dil.
- Soft Premium tasarım.
- Açık ve koyu görünüm.
- VDOX Lab ortak web altyapısı.
- info@vdoxlab.com.
- Ücretsiz temel güvenlik.
- Ücretsiz 3 aktif konum profili.
- Premium 10 aktif konum profili.
- Ücretsiz 2 güvenli bölge.
- Premium 18 güvenli bölge.
- Ücretsiz 24 saat geçmiş.
- Premium 30 gün geçmiş.
- Aylık 5,99 USD.
- Yıllık 39,99 USD.
- Reklamsız kullanım.
- Aile başına ortak yıllık 7 günlük geçiş hakkı.
- Onaylanmamış ürün ekranının kodlanmaması.

**D. Son belge düzenlemesi**

Yukarıdaki netleştirmeleri mevcut şartnameye işle.

Belgeyi V1.1 — Revizyon 4 / Onaylı Ürün Baz Çizgisi olarak kaydet.

Karar geçmişini ayrı dosyada koru.

Yeni ürün itirazı, marka araştırma turu veya özellik önerisi başlatma.

Yalnızca güvenlik, hukuk, işletim sistemi ve temel teknik uygulanabilirlik açısından zorunlu engeller raporlanacaktır.

**E. Faz 0 hazırlığı**

Mevcut 17 teknik belirsizlik için bir fizibilite görev listesi oluştur.

Her görev için:

- Amaç.
- Doğrulanacak varsayım.
- Test yöntemi.
- Gerekli cihaz veya hesap.
- Kabul kriteri.
- Kanıt biçimi.
- Başarısızlık durumundaki alternatif.
- Hukuki bağımlılık.
- Bütçe gereksinimi.

Henüz üretim kodlamasına veya canlı altyapı kurulumuna başlanmayacaktır.

Gerçek kişisel veriler hukuki uygunluk sağlanmadan üretim altyapısına aktarılmayacaktır.

**F. Marka ve tasarım**

FamilyGuard iç kod adı olarak korunacaktır.

Wingfold koşullu birinci aday, Eavely koşullu yedek adaydır.

Nihai marka seçimi proje sahibine aittir.

Marka kesinleştikten sonra Faz D tasarım sürecine geçilecektir. Soft Premium görsel yön korunacaktır.

Logo, uygulama ikonu, tasarım sistemi ve bütün V1 ekranlarının tasarımları ürün direktörü ve proje sahibi tarafından onaylanacaktır.

**G. Nihai durum**

Karar 01–14: ONAYLI.

Nihai şartname denetimi: TAMAMLANDI.

Ürün kapsamı: KİLİTLENDİ.

Son metin netleştirmeleri: UYGULANACAK.

Marka seçimi: PROJE SAHİBİ ONAYI BEKLİYOR.

Faz 0 teknik fizibilite: BEKLİYOR.

Hukuki uygunluk: BEKLİYOR.

Faz D tasarım: BEKLİYOR.

Üretim kodlaması: BAŞLANMAYACAK.

App Store yayın onayı: VERİLMEDİ.

**ÜRÜN DİREKTÖRÜ ONAYI VERİLMİŞTİR.**

Nihai bütçe, marka ve proje başlangıç onayı proje sahibine aittir.
