# Gelecek Entegrasyon Aşaması — Teknik Notlar

Bu doküman yalnızca sonraki aşamayı tarif eder. Mevcut teslimde backend, Supabase veya gerçek API kodu yoktur.

## Önerilen veri modeli

- `profiles`: `user_id`, `role`, `display_name`, `active`.
- `campaigns`: başlık, açıklama, görsel, Chicago başlangıç/bitiş zamanı, yayın durumu.
- `showcase_posts`: Instagram media ID, tür, thumbnail, permalink, seçili durumu, sıra.
- `featured_reviews`: Google review ID, orijinal metin, puan, tarih, yazar, seçili durumu, sıra.
- `menu_categories`: ad, sıra, yayın durumu.
- `menu_items`: kategori, ad, açıklama, fiyat, fotoğraf yolu, bulunabilirlik, sıra.
- `publish_revisions`: taslak/yayın sürümleri ve yönetici denetim izi.

## Güvenlik sınırı

- GitHub Pages yalnızca müşteri frontend’ini sunar.
- Yönetici yazma işlemleri güvenli bir API/edge function üzerinden yapılır.
- Meta ve Google tokenları yalnızca sunucu tarafı secret store içinde tutulur.
- RLS varsayılan olarak tüm yazmayı reddeder; yalnızca `admin` rolü yazabilir.
- Müşteri frontend’i sadece yayımlanmış ve aktif kayıtlara anonim okuma yapar.
- Görsel yüklemeleri dosya türü, boyut ve yetki kontrolünden geçer.

## Kampanya saat dilimi

Kampanyalar veritabanında UTC tutulmalı, panelde `America/Chicago` olarak girilip gösterilmelidir. Başlangıç dahil, bitiş anı geçtiğinde içerik otomatik gizlenmelidir.

## Instagram

Meta’nın güncel resmî yöntemleri kullanılmalı; hesap tipi ve izin gereksinimleri entegrasyon anında tekrar doğrulanmalıdır. Token frontend’e konmamalıdır.

## Google yorumları

Google’ın güncel API, atıf, cache ve veri saklama koşulları entegrasyon anında doğrulanmalıdır. Orijinal yorum metni, puan, yazar ve tarih değiştirilmemelidir.

