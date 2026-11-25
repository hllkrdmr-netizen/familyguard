# FamilyGuard (iç kod adı)

Aile güvenliği ve konum uygulaması — VDOX Lab. Bu depo şu an yalnızca **belge, tasarım referansı ve görev** deposudur. Üretim kodu bulunmaz.

## Çalışma düzeni
| Rol | Sorumluluk |
|---|---|
| Proje sahibi | Nihai ürün, tasarım, bütçe ve marka onayı |
| ChatGPT (ürün direktörü) | Ürün yönetimi, görsel tasarım, kalite kontrol |
| Claude | Teknik araştırma, kodlama (izin verildiğinde), teknik testler ve raporlar |

## Klasörler
| Klasör | İçerik |
|---|---|
| `docs/SPEC.md` | Tek geçerli ürün şartnamesi (V1.1 Revizyon 4) |
| `docs/DECISIONS.md` | Karar geçmişi (tarihsel kayıt, talimat kaynağı değildir) |
| `docs/STATUS.md` | Güncel durum |
| `docs/QA/` | Faz 0 ve test raporları |
| `design-reference/` | Onaylı tasarım referansları (brand, screens, icons, components, states) |
| `tasks/pending/` | Onay bekleyen görev talimatları |
| `tasks/approved/` | Onaylanmış, uygulanacak görevler |
| `tasks/completed/` | Tamamlanan görevler ve sonuçları |

## Kurallar
1. Ürün kuralları için tek kaynak `docs/SPEC.md`'dir; diğer belgeler onunla çelişemez.
2. `design-reference/` içine yalnızca proje sahibinin onayladığı tasarımlar konur. Onaysız ekran kodlanmaz.
3. Bir görev ancak `tasks/approved/` klasörüne taşındıktan sonra uygulanır.
4. Gerçek kişisel veri bu depoya konmaz.
