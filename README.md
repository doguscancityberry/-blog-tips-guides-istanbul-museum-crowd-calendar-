# Istanbul Museum Crowd Calendar – prototip

istanbultouristpass.com/blog/tips-guides/istanbul-museum-crowd-calendar-visit-quietest-days sayfasının yeni halinin iç inceleme prototipi (İngilizce). `noindex` ve `robots.txt` ile arama motorlarına kapalı.

## Yayınlama (GitHub Pages)

1. Yeni repo açın, bu klasördeki dosyaları köke yükleyin: `index.html`, `crowd-data.json`, `robots.txt`, `README.md` (gizli `.nojekyll` dosyası görünmezse sorun değil, zorunlu değil).
2. Settings → Pages → Source: `main` / `root`.
3. Link: `https://<kullanıcı-veya-org>.github.io/<repo>/`

## Sayfadaki prototip kontrolü

Alttaki koyu barda **Review notes** düğmesi var. Açınca sarı Türkçe notlar görünür: her bilginin kaynağı ve yayından önce kontrol edilecekler.

## Veri

Sayfadaki her şey (saatler, kapalı günler, kaynaklar, yoğunluk tahminleri, aylık ziyaretçi, namaz vakitleri, tatiller) `crowd-data.json` dosyasından üretildi; sayfada aynı bilgiler HTML ve SVG olarak hazır basılı. Yoğunluk seviyeleri tahmin (model `crowd-data.json` içindeki `method` alanında anlatılıyor). Pass giriş verisi gelirse sadece bu dosya değişir.

"Today in Istanbul" kutusu tarayıcıda İstanbul tarihine göre kendini günceller: bugün kapalı yerler, o günün namaz vakitleri (26 Ekim–1 Kasım 2026 haftası dosyada var) ve sıradaki tatil. Canlıda namaz vakitleri günlük otomatik çekilmeli.

## Satış alanları, fiyatlar ve ölçüm (27 Ekim)

- Her yer kartında ısı haritasının altında tek bir satış alanı var: pass'in o yerde ne verdiği (sıra beklemeden giriş, sabit saatli tur/hosted entry, ücretsiz girişli yerlerde tur), fiyat ve ITP ürün sayfasına giden buton.
- Fiyatlar 27 Ekim 2026'da ürün sayfalarımızdan alındı ve `crowd-data.json` içinde `offer` alanında duruyor. Canlıda bloglardaki gibi fiyat sisteminden otomatik gelmeli; her satış alanında `data-price-slug` (ürün slug'ı) var.
- Tıklama ölçümü: `a[data-cta]` linklerine tıklanınca `dataLayer`'a `crowd_cta_click` olayı gidiyor (`cta`, `sight`, `product`, `kind`, `link_url`). GTM'de bu olay için GA4 event etiketi kurulmalı. `cta` değerleri: `crowd-card` (kart butonu), `crowd-pass-section`, `crowd-related`.
- istanbul.com'a giden rehber butonları kaldırıldı. Saatini istanbul.com'dan aldığımız 10 yerde kaynak satırı "our sister site" diyor ve link `rel="nofollow"`.

## Header ve footer

Header ve footer istanbultouristpass.com'un kopyası; sayfa stilleriyle karışmasın diye ayrı katmanda (shadow DOM) duruyor, linkler canlı siteye gidiyor. Canlıya alırken bu kopya kullanılmaz; sayfa sitenin kendi layout'una girer.

## Yayından önce

- Koyu prototip barını ve tüm `.note` öğelerini kaldırın.
- `<meta name="robots" content="noindex, nofollow">` satırını silin. Canonical mevcut URL olarak kalır. `robots.txt` sadece bu prototip repo içindir.
- JSON-LD: BlogPosting (yazar Ekim Erkan), BreadcrumbList, Dataset, ItemList (20 TouristAttraction, net olan 7'sinde openingHoursSpecification), FAQPage. Canlı blog şablonu zaten BlogPosting ve BreadcrumbList basıyor (26 Ekim 2026 kontrolü); canlıda bunlar çift olmasın: şablondakiler kalsın (tarih ve yazar güncellenerek), bizim bloktan sadece Dataset, ItemList ve FAQPage eklensin.
- Çelişen ve doğrulanamayan saat bilgileri ayrı notta listelendi (Rumeli Hisarı restorasyonu, Yerebatan kapanış saati, ürün sayfalarındaki saat farkları). Product ile netleşmeden yayına almayın.
