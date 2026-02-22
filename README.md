# 🛒 Hepsiburada Mobile Test Automation

Hepsiburada Android uygulaması için [Maestro](https://maestro.mobile.dev/) ile yazılmış uçtan uca (E2E) mobil test otomasyon projesidir.

## 📋 Test Senaryosu

Uygulama açılışından sepet doğrulamasına kadar tam bir alışveriş akışını test eder:

**Uygulama Açılışı → Ürün Arama → Filtre Uygulama → Ürün Seçimi → Sepete Ekleme → Sepet Doğrulama**

| Adım | Sayfa | Açıklama |
|------|-------|----------|
| 1 | `home_page` | Uygulama temiz state ile başlatılır |
| 2 | `search_page` | Arama çubuğuna ürün sorgusu yapılır |
| 3 | `filter_page` | Cinsiyet, renk, beden ve fiyat aralığı filtreleri uygulanır |
| 4 | `product_listing_page` | Filtrelerin aktif olduğu doğrulanır, ilk ürün seçilir |
| 5 | `product_detail_page` | Ürün detayında "Sepete Ekle" butonuna tıklanır |
| 6 | `login_handler` | Giriş/sepet yönlendirmesi yapılır |
| 7 | `cart_page` | Sepet sayfası ve fiyat doğrulaması yapılır |

## 📁 Proje Yapısı

```
├── tests/
│   └── filter_test.yaml            # Ana test dosyası
├── flows/
│   └── pages/
│       ├── home_page.yaml           # Uygulama başlatma
│       ├── search_page.yaml         # Ürün arama
│       ├── filter_page.yaml         # Filtre uygulama
│       ├── product_listing_page.yaml # Ürün listeleme & seçim
│       ├── product_detail_page.yaml  # Ürün detay & sepete ekleme
│       ├── login_handler.yaml        # Giriş yönlendirme
│       └── cart_page.yaml            # Sepet doğrulama
```

## ⚙️ Environment Değişkenleri

Test, aşağıdaki environment değişkenleri ile parametrik olarak çalışır:

| Değişken | Açıklama | Örnek Değer |
|----------|----------|-------------|
| `APPID` | Uygulama paket adı | `com.pozitron.hepsiburada` |
| `SEARCH_QUERY` | Aranacak ürün | `Adidas ayakkabi` |
| `SEARCH_PLACEHOLDER` | Arama çubuğu placeholder metni | `Ürün, kategori veya marka ara` |
| `FILTER_GENDER` | Cinsiyet filtresi | `Erkek` |
| `FILTER_COLOR` | Renk filtresi | `Beyaz` |
| `FILTER_SIZE` | Beden filtresi | `42` |
| `FILTER_PRICE_MIN` | Minimum fiyat | `3000` |
| `FILTER_PRICE_MAX` | Maksimum fiyat | `5000` |
| `PRODUCT_NAME` | Sepette doğrulanacak ürün adı | `copyTextFrom ile otomatik atanır` |

### Environment Ayarları

<p align="center">
  <img src="assets/environment_settings.png" alt="Environment Settings" width="600"/>
</p>

## 🚀 Kurulum & Çalıştırma

### Gereksinimler

- [Maestro CLI](https://maestro.mobile.dev/getting-started/installing-maestro)
- Android Emulator veya fiziksel cihaz
- Hepsiburada uygulaması (`com.pozitron.hepsiburada`)

### Kurulum

```bash
# Maestro kurulumu
curl -Ls "https://get.maestro.mobile.dev" | bash

# Kurulumu doğrula
maestro --version
```

### Testi Çalıştırma

```bash
# Testi çalıştır
maestro test tests/filter_test.yaml

# Belirli environment değişkenleri ile çalıştır
maestro test -e SEARCH_QUERY="Adidas ayakkabi" -e FILTER_GENDER="Erkek" -e FILTER_COLOR="Beyaz" -e FILTER_SIZE="42" -e FILTER_PRICE_MIN="3000" -e FILTER_PRICE_MAX="5000" tests/filter_test.yaml
```

## 🎥 Test Videosu

<p align="center">
https://github.com/user-attachments/assets/8de46dd5-8e58-4cf9-a70c-642db1d22256
</p>

## 🛠️ Kullanılan Maestro Komutları

| Komut | Kullanım Amacı |
|-------|----------------|
| `launchApp` | Uygulamayı temiz state ile başlatma |
| `tapOn` | Elemente tıklama |
| `doubleTapOn` | Çift tıklama (koordinat & id bazlı) |
| `assertVisible` | Elementin görünür olduğunu doğrulama |
| `scrollUntilVisible` | Elemente kadar kaydırma |
| `setClipboard` / `pasteText` | Panodan metin yapıştırma |
| `inputText` / `eraseText` | Metin girişi ve silme |
| `pressKey` | Klavye tuşuna basma |
| `copyTextFrom` | Element metnini değişkene kaydetme |
| `runFlow` | Alt akışları çalıştırma |



