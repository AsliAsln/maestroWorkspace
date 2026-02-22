# 🛒 Hepsiburada Mobile Test Automation

[![tr](https://img.shields.io/badge/lang-tr-red.svg)](README.tr.md)
[![en](https://img.shields.io/badge/lang-en-blue.svg)](README.md)

End-to-end (E2E) mobile test automation project for the Hepsiburada Android app, built with [Maestro](https://maestro.mobile.dev/).

## 📋 Test Scenario

Tests a complete shopping flow from app launch to cart verification:

**App Launch → Product Search → Apply Filters → Product Selection → Add to Cart → Cart Verification**

| Step | Page | Description |
|------|------|-------------|
| 1 | `home_page` | App launches with a clean state |
| 2 | `search_page` | Product search query is entered |
| 3 | `filter_page` | Gender, color, size, and price range filters are applied |
| 4 | `product_listing_page` | Active filters are verified, first product is selected |
| 5 | `product_detail_page` | "Add to Cart" button is tapped |
| 6 | `login_handler` | Login/cart redirection is handled |
| 7 | `cart_page` | Cart page and price validation are performed |

## 🎥 Test Video

https://github.com/user-attachments/assets/1320e755-1a43-486e-8161-7f53f5b31937

## 📁 Project Structure

```
├── tests/
│   └── filter_test.yaml              # Main test file
├── flows/
│   └── pages/
│       ├── home_page.yaml             # App launch
│       ├── search_page.yaml           # Product search
│       ├── filter_page.yaml           # Filter application
│       ├── product_listing_page.yaml  # Product listing & selection
│       ├── product_detail_page.yaml   # Product detail & add to cart
│       ├── login_handler.yaml         # Login redirection
│       └── cart_page.yaml             # Cart verification
```

## ⚙️ Environment Variables

The test runs parametrically with the following environment variables:

| Variable | Description | Example Value |
|----------|-------------|---------------|
| `APPID` | Application package name | `com.pozitron.hepsiburada` |
| `SEARCH_QUERY` | Product to search | `Adidas ayakkabi` |
| `SEARCH_PLACEHOLDER` | Search bar placeholder text | `Ürün, kategori veya marka ara` |
| `FILTER_GENDER` | Gender filter | `Erkek` |
| `FILTER_COLOR` | Color filter | `Beyaz` |
| `FILTER_SIZE` | Size filter | `42` |
| `FILTER_PRICE_MIN` | Minimum price | `3000` |
| `FILTER_PRICE_MAX` | Maximum price | `5000` |
| `PRODUCT_NAME` | Product name to verify in cart | `Auto-assigned via copyTextFrom` |

## 🚀 Setup & Run

### Requirements

- [Maestro CLI](https://maestro.mobile.dev/getting-started/installing-maestro)
- Android Emulator or physical device
- Hepsiburada app (`com.pozitron.hepsiburada`)

### Installation

```bash
# Install Maestro
curl -Ls "https://get.maestro.mobile.dev" | bash

# Verify installation
maestro --version
```

### Running the Test

```bash
# Run the test
maestro test tests/filter_test.yaml

# Run with specific environment variables
maestro test -e SEARCH_QUERY="Adidas ayakkabi" -e FILTER_GENDER="Erkek" -e FILTER_COLOR="Beyaz" -e FILTER_SIZE="42" -e FILTER_PRICE_MIN="3000" -e FILTER_PRICE_MAX="5000" tests/filter_test.yaml
```

## 🛠️ Maestro Commands Used

| Command | Purpose |
|---------|---------|
| `launchApp` | Launch the app with a clean state |
| `tapOn` | Tap on an element |
| `doubleTapOn` | Double tap (coordinate & id based) |
| `assertVisible` | Verify element visibility |
| `scrollUntilVisible` | Scroll until element is found |
| `setClipboard` / `pasteText` | Paste text from clipboard |
| `inputText` / `eraseText` | Text input and deletion |
| `pressKey` | Press a keyboard key |
| `copyTextFrom` | Copy element text to a variable |
| `runFlow` | Run sub-flows |
