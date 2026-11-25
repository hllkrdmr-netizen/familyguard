# FAMILYGUARD — GELİŞTİRME ORTAMI RAPORU (Görev 001, Bölüm 1)

**Tarih:** 25 Kasım 2026
**Kaynak:** Proje sahibinin Mac'inde çalıştırılan salt okunur komut çıktısı. Hiçbir şey kurulmadı veya değiştirilmedi.
**Durum:** Bölüm 1 artık BLOCKED değil; veri alındı.

## 1. Mevcut ortam

| Bileşen | Değer |
|---|---|
| Mac | MacBook Pro (Apple silicon, arm64) |
| macOS | 26.7.1 (25G241) |
| Xcode | 27.2 (27B52) |
| Swift | 6.4.2 |
| iOS SDK | iOS 27.2 |
| iOS Simulator SDK | iOS 27.2 |
| Kurulu simülatör çalışma zamanları | **Yalnızca iOS 26.5** |
| Kurulu simülatör cihazları (iOS 26.5) | iPhone 17 Pro, 17 Pro Max, 17, 17e, Air, 15 Pro, SE (3. nesil) ve diğer projelere ait özel adlı simülatörler |

Diğer projelere (Paintlings, Underworld, Brain Lab) ait simülatörlere dokunulmayacaktır.

## 2. iOS 17 uyumu — Apple resmî bilgisi

Apple'ın Xcode destek tablosuna göre (developer.apple.com/support/xcode):

| Xcode | Minimum macOS | iOS deployment target | En eski iOS simülatörü |
|---|---|---|---|
| 27.2 (kurulu) | macOS Tahoe 26.6+ | iOS 15–27 | **iOS 17** |

**Sonuçlar:**
- ✅ **Minimum deployment target iOS 17 bu ortamda desteklenir.** Mevcut macOS (26.7.1) Xcode 27.2 gereksinimini karşılar.
- ✅ Xcode 27.x, iOS 17 simülatörünü resmî olarak destekleyen en eski sürümdür.
- ❌ **iOS 17 simülatör çalışma zamanı kurulu değil.** iOS 27.2 çalışma zamanı da kurulu değil; yalnızca iOS 26.5 var.

## 3. Riskler ve belirsizlikler

1. **iOS 17 çalışma zamanının kurulabilirliği — BELİRSİZ.** Apple Developer Forums'ta, Xcode 27'nin `xcodebuild -downloadPlatform` komutuyla eski iOS simülatörlerini (18, 17) indiremediği bildirilmiştir (FB24836279). Resmî tablo desteği gösterse de kurulumun bu ortamda çalışacağı denenmeden varsayılmayacaktır.
2. **Disk alanı:** Her iOS simülatör çalışma zamanı birkaç GB yer kaplar. Kurulumdan önce boş alan kontrol edilmelidir.
3. **Bilgi notu:** Forumda, Xcode 27 ile derlenip iOS 17'den eski sürümlerde çalıştırılan uygulamalarda Swift çalışma zamanı çökmesi bildirilmiştir. FamilyGuard'ın minimumu iOS 17 olduğu için doğrudan etkilenmez; F0 testlerinde iOS 17 davranışı yine de ayrıca doğrulanacaktır.

## 4. Kurulum gerektiren adımlar (proje sahibi onayı olmadan yapılmayacak)
1. iOS 17 simülatör çalışma zamanı (Görev 001 Denetimi B-2 için).
2. iOS 27.2 simülatör çalışma zamanı (güncel iOS testleri için; gerçek cihaz iPhone 17 Pro Max zaten güncel iOS'ta olabilir).
3. Yerel Supabase için OrbStack veya Docker.

## 5. Gerçek cihaz testine yönelik mevcut araçlar
- Xcode 27.2 (Instruments ve cihaz konsolu dahil) mevcut.
- iPhone 17 Pro Max: iOS sürümü bu raporda alınmadı; ilk gerçek cihaz testinden önce kaydedilecek (Ayarlar > Genel > Hakkında).
- Apple Developer hesabı mevcut. Hesaptaki yetenekler (App Attest, Time Sensitive, Critical Alerts), kalıcı Bundle ID oluşturulmadan doğrulanamaz.

## Kaynaklar
- https://developer.apple.com/support/xcode/
- https://developer.apple.com/forums/thread/847134
- https://developer.apple.com/forums/thread/847531
