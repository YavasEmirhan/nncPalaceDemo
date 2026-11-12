# Palace Istanbul — GitHub Pages Teslimi

Bu klasör, **Palace Istanbul Kebab House** için hazırlanan statik web sitesidir. Dosyalar doğrudan GitHub Pages üzerinde çalışır. Bu aşamada Supabase, veritabanı ve gerçek Instagram/Google API bağlantısı **özellikle kurulmamıştır**.

## 1. GitHub’a hangi dosyaları yükleyeceğim?

`PalaceIstanbul_GitHubPages_Final.zip` dosyasını açın. ZIP’in içindeki bütün dosya ve klasörleri `nncPalaceDemo` repository’sinin kök dizinine yükleyin.

Önemli dosyalar:

- `index.html`: Ana sayfa.
- `menu.html`, `story.html`, `gallery.html`, `events.html`, `reservations.html`, `reviews.html`, `contact.html`, `qr-menu.html`: Müşteri sayfaları.
- `styles.css` ve `app.js`: Tasarım ve müşteri tarafı etkileşimler.
- `assets/`: Yerel görseller ve QR kodu.
- `admin-website.html`: Website Management frontend prototipi.
- `admin-menu.html`: QR Menu Management frontend prototipi.
- `.nojekyll`: GitHub Pages’in dosyaları olduğu gibi yayımlaması için.

ZIP’in içinde ayrıca bir ana klasör yoktur; `index.html` doğrudan ZIP kökündedir.

## 2. Web sitesini nasıl yayımlayacağım?

1. GitHub’da `YavasEmirhan/nncPalaceDemo` repository’sini açın.
2. ZIP içindeki bütün dosyaları repository köküne yükleyin.
3. GitHub’da **Settings → Pages** bölümüne girin.
4. **Deploy from a branch** seçin.
5. Branch olarak `main`, klasör olarak `/ (root)` seçin.
6. Kaydedin ve GitHub Pages adresinin hazırlanmasını bekleyin.

Beklenen adres: `https://yavasemirhan.github.io/nncPalaceDemo/`

Bu teslim sırasında repository’ye push yapılmadı ve canlı restoran sitesi değiştirilmedi.

## 3. Şu anda çalışan özellikler

- Dokuz müşteri sayfası ve mobil menü.
- Yerel, GitHub Pages uyumlu restoran görselleri.
- 41° North marka hikâyesi.
- Kategori filtreli dinamik menü.
- Gerçek Google Maps gömülü haritası, yol tarifi, adres kopyalama ve telefon bağlantısı.
- Mevcut QR menü adresine giden yerel QR PNG dosyası.
- Resmî rezervasyon sayfasına yönlendirme.
- Galeri lightbox, yorum kaydırma ve erişilebilir klavye kontrolleri.
- Website Management ve QR Menu Management için iki ayrı mobil uyumlu frontend paneli.
- Panellerde örnek verilerle ürün ekleme/düzenleme/silme, bulunabilirlik, kategori sırası, kampanya oluşturma, yorum ve vitrin seçimi.
- Panel değişikliklerini aynı tarayıcıda `localStorage` ile taslak olarak kaydetme ve yayımlama.
- `noindex` ve `robots.txt` ile demo sitesinin resmî siteyle arama sonuçlarında yarışmasını önleme.
- Online ödeme, checkout veya ödeme bağlantısı yoktur.

## 4. Yönetim panelleri nasıl açılır?

- Website Management: `admin-website.html`
- QR Menu Management: `admin-menu.html`

Giriş ekranındaki **Open frontend prototype** butonu yalnızca tasarım akışını gösterir. Bu gerçek kimlik doğrulama değildir. Veriler sadece o tarayıcıda saklanır ve başka cihaza gitmez.

## 5. Supabase bağlantısını nasıl kuracağım?

Bu aşamada Supabase kurulmadı. Güvenlik nedeniyle GitHub Pages içine sahte giriş veya gizli anahtar eklenmedi.

İleride yapılacaklar:

1. Ayrı bir Supabase projesi oluşturun.
2. `profiles`, `campaigns`, `showcase_posts`, `featured_reviews`, `menu_categories` ve `menu_items` tablolarını oluşturun.
3. Yönetici kullanıcılarını Supabase Auth ile oluşturun.
4. Her tablo için Row Level Security (RLS) açın.
5. Müşteri sayfalarına yalnızca yayımlanmış içerik için okuma yetkisi verin.
6. Yazma yetkisini yalnızca doğrulanmış yönetici rolüne verin.
7. Instagram ve Google token işlemlerini frontend yerine Edge Function veya başka güvenli sunucu tarafında çalıştırın.

Bu kurulum ayrı bir backend aşamasıdır. `INTEGRATION-NOTES.md` dosyasında önerilen veri modeli bulunur.

## 6. Instagram API bağlantısı için ne gerekli?

- Profesyonel Instagram hesabı (Business veya Creator).
- Uygun bir Facebook Page bağlantısı.
- Meta Developer uygulaması.
- Gerekli Instagram Graph API izinleri ve Meta onayı.
- Uzun ömürlü token yenileme işlemini yapan güvenli bir serverless/edge function.
- Tokenların GitHub repository’sine veya frontend JavaScript’e yazılmaması.

Bağlantı yapılana kadar panel açıkça **Integration required** gösterir ve sahte senkronizasyon yapmaz.

## 7. Google yorum bağlantısı için ne gerekli?

- Restoranın doğrulanmış Google Business Profile / Place kimliği.
- Kullanılacak Google API için açık bir Cloud projesi ve faturalandırma/izin ayarları.
- Google’ın yorum gösterimi, atıf ve veri saklama kurallarına uygun uygulama.
- API anahtarını sınırlayan güvenli sunucu tarafı bağlantısı.

Yorum metni ve yıldızı değiştirilmemelidir. Mevcut demoda yalnızca resmî web sitesinde zaten gösterilen kısa alıntılar vardır.

## 8. Yönetici kullanıcılarını nasıl oluşturacağım?

Şu anda gerçek yönetici kullanıcı sistemi yoktur. Frontend prototip giriş ekranı güvenlik sağlamaz.

Gerçek sistemde:

1. Kullanıcıyı güvenli kimlik doğrulama hizmetinde oluşturun.
2. Yönetici rolünü sunucu tarafında veya korumalı profil tablosunda tutun.
3. RLS ile yalnızca yönetici rolüne yazma izni verin.
4. Yetkisi olmayan kullanıcıyı hem arayüzde hem API/veritabanı katmanında engelleyin.

## 9. Harici erişim bekleyen özellikler

- Instagram Graph API canlı gönderi senkronizasyonu.
- Google yorum API canlı senkronizasyonu.
- Supabase/veritabanı ve cihazlar arası yayınlama.
- Gerçek güvenli yönetici girişi ve rol kontrolü.
- Görsel dosya yükleme servisi.

Bu bağlantılar olmadan müşteri web sitesi, QR bağlantısı, harita, telefon, rezervasyon yönlendirmesi ve tarayıcı içi panel prototipleri çalışır.

## 10. Görsel kaynağı ve kullanım notu

Paketlenen fotoğraflar, Palace Istanbul’un mevcut resmî web sitesinde yayımlanan kaynaklardan yerelleştirilmiştir. Canlıya alınmadan önce restoranın ve web sağlayıcısının görsel kullanım izni teyit edilmelidir. Galeri canlı Instagram akışı değildir.

## 11. SEO geçiş notu

Bu demo `noindex` olarak teslim edilmiştir. Resmî domain’e geçiş yapılacaksa:

- Eski URL’leri koruyun veya tek tek 301 yönlendirmesi yapın.
- Canonical URL’leri canlı domaine çevirin.
- `robots.txt` engelini kaldırın.
- Sitemap’i canlı domain ile güncelleyin.
- Search Console ve Analytics kontrollerini geçişten sonra yapın.

