# FAMILYGUARD — DURUM

**Son güncelleme:** 25 Kasım 2026

| Konu | Durum |
|---|---|
| Ürün şartnamesi | ONAYLI — V1.1 Revizyon 4 / Onaylı Ürün Baz Çizgisi (`docs/SPEC.md`) |
| Ürün kapsamı | KİLİTLİ (8 modül) |
| Karar geçmişi | KABUL EDİLDİ (`docs/DECISIONS.md`) |
| Faz 0 görev planı | ONAYLI (`docs/QA/faz0/FAZ0-GOREV-LISTESI.md`) |
| Faz 0 ilerlemesi | 0/19 PASS |
| Görev 001 (ücretsiz hazırlık) | RAPOR KABUL EDİLDİ (`docs/QA/faz0/GOREV-001-RAPORU.md`); Apple ve izleme doğrulaması devam ediyor |
| Marka seçimi | BEKLİYOR — Wingfold koşullu birinci, Eavely koşullu yedek; iç kod adı FamilyGuard |
| Hukuki uygunluk | BEKLİYOR |
| Faz D tasarım | DEVAM EDİYOR — proje sahibi ve ürün direktörü ebeveyn ana ekranı için 3 konsept hazırlıyor |
| Üretim kodlaması | BAŞLANMADI |
| App Store yayın onayı | VERİLMEDİ |

## Görev 001 denetimi ile verilen teknik kararlar
1. **Realtime kanal güvenlik sürümü — ONAYLI:** Kanallar `family:<id>:v<n>`; iptalde sürüm atomik olarak değişir; F0-02'ye 12 ek test eklendi.
2. **iOS 17 test stratejisi — KOŞULLU ONAYLI:** iOS 17 simülatörde; arka plan konumu, bölge, pil, yeniden başlatma, zorla kapatma, App Attest, SMS/arama, APNs ve veri koruma testleri yalnızca gerçek cihazda geçerli. Cihazların iOS sürümleri izinsiz değiştirilmez.
3. **Cihaz içi konum ölçümü — HUKUKİ ÖN DEĞERLENDİRMEYE SUNULACAK:** F0-01, F0-08, F0-15, F0-19 için. Hukuki ön değerlendirme bitmeden gerçek konum ölçümü başlamaz; çocuk konumu kullanılmaz; gerçek koordinatlar depoya veya sohbetlere konmaz.

## Çalışma düzeni
Claude depoya yazar; ChatGPT yalnızca okur; ürün direktörü kararları proje sahibi aracılığıyla Claude'a iletilir.

## Bekleyen proje sahibi girdileri (sırayla)
1. Mac ortam kontrol komutunun çıktısı (Görev 001, Bölüm 1).
2. Yerel Supabase (OrbStack/Docker) kurulum onayı.
3. Ödünç ikinci iPhone'un modeli ve iOS sürümü.
4. Supabase Pro organizasyonu Usage ekranı verileri.

## Faz 0 görev durumu
| Görev | Durum |
|---|---|
| F0-01 … F0-08 | NOT STARTED |
| F0-09 | IN PROGRESS (araştırma) |
| F0-10 | BLOCKED (Pro organizasyon erişimi yok) |
| F0-11 … F0-19 | NOT STARTED |
