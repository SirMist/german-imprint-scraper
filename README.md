[German Imprint Scraper](https://apify.com/codescraper/german-imprint-scraper?fpr=data)

# 🇩🇪 German Impressum Scraper – Extract Legal Details Automatically

This Apify actor automatically detects and extracts **Impressum (legal disclosure)** data from German websites.
It helps you collect structured company and legal information for **compliance**, **CRM enrichment**, and **business intelligence**.

---

## 🚀 What It Does

The scraper visits each website, finds its Impressum page, and extracts:

- 🏢 **Company name**, **decision maker name** and **decision maker role** (e.g., Geschäftsführer, Inhaber)
- 🏠 **Full address** + separated fields (street, house number, postal code, city, country)
- ☎️ **Phones** and 📧 **emails**
- 🧾 **Register number**, **register court**, and **tax ID**
- 🌐 **Social media links** (Facebook, Instagram, X/Twitter, LinkedIn, etc.)
- 🧠 **Meta title** and **meta description**

The output is fully structured and **Excel-ready**.

---

## ⚙️ Input Configuration

| Field | Type | Description |
| --- | --- | --- |
| `startUrls` | Array | One or more website URLs to scrape. |
| `useProxy` | Boolean | Enable Apify proxy or custom proxy. |
| `proxyConfig` | Object | Custom proxy configuration (optional). |
| `userAgent` | String | Override default User-Agent header. |
| `excludeFields` | Object | Toggle off fields you don’t want (address, phones, emails, etc.). |

---

### 🧩 Example Input

```
{
  "startUrls": [
    { "url": "https://www.marley.de" },
    { "url": "https://www.dr-johanna-budwig.de" }
  ],
  "useProxy": false,
  "userAgent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
  "excludeFields": {
    "phones": false,
    "emails": false,
    "taxId": false
  }
}
```

---

### 📊 Example Output

```
{
  "mainUrl": "https://www.marley.de",
  "impressumUrl": "https://www.marley.de/impressum",
  "address": "Adolf-Oesterheld-Str. 28, 31515 Wunstorf, DE",
  "address/street": "Adolf-Oesterheld-Str.",
  "address/house number": "28",
  "address/postal code": "31515",
  "address/city": "Wunstorf",
  "address/country": "DE",
  "companyName": "Marley Deutschland GmbH",
  "decisionMakerName": "Stefan Ostertag",
  "decisionMakerRole": "Geschäftsführer",
  "phones": "+495031530",
  "emails": "info@marley.de",
  "registerNumber": "HRB 110009",
  "registerCourt": "Amtsgericht Hannover",
  "taxId": "DE811119134",
  "social/x": "https://twitter.com/marleyeurope",
  "metaTitle": "Marley Deutschland GmbH",
  "metaDescription": "Marley – Innovative Haustechnik und Dachentwässerungssysteme."
}
```

---

## 🧠 Features

- 🇩🇪 Extracts Impressum data from any German website
- 🔍 Automatically finds Impressum links even if nested in menus or footers
- 🏠 Provides both full address and separated address fields
- ☎️ Detects phones, emails, and social links
- 🌍 Supports proxies and custom User-Agent
- ⚙️ Flexible Exclude Fields toggles in input
- 📊 Clean Excel/CSV output with consistent column order

---

## 💡 Use Cases

- Build databases of German businesses
- Legal & compliance verification (Impressum law)
- Contact data enrichment for CRMs
- Market research and lead generation

---

## ⚖️ Legal Disclaimer

This actor only extracts publicly available business information from Impressum pages in accordance with §5 TMG.
Data such as company representative names are collected solely for transparency, compliance, or research purposes — not for unsolicited contact or personal data processing under GDPR.

---

## 🧑‍💻 Developer Info

**Author:** `codescraper`
**Contact:** `codescraper011@gmail.com`

## 🏷️ Tags

`impressum` · `web-scraping` · `legal` · `data-extraction` · `germany` · `automation`

---