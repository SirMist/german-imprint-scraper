[German Imprint Scraper](https://apify.com/winningsolutions/german-imprint-scraper?fpr=data)

# German Impressum Scraper – Decision Makers, Email Verification & Company Data

An **AI-powered** Apify Actor that scrapes and extracts **contact details** from German website Impressum pages.

It automatically detects **imprint links**, navigates pages reliably, and returns **structured JSON** with **company name**, **contact person**, **address**, **phone**, **email** (with optional **validation**), **VAT ID**, and **register numbers** - perfect for **lead generation** or **compliance checks**.

Designed for **lead generation**, **CRM enrichment**, and **compliance workflows**, the scraper ensures high **data accuracy** through intelligent **page detection**, robust **parsing** logic, and optional **email validation**. It supports **batch processing**, handles **edge cases** like non-standard layouts, and includes **retry mechanisms** for scalable **data extraction**.

## Use Cases

- Generate **B2B leads** with **verified contact data**
- Enrich your **CRM** with **German company information**
- Build **outreach lists** with **validated emails**
- Run **market** and **competitor research**
- Automate **data collection** workflows

## Index

- Release Notes
- Features
- Use Cases
- Advanced Email Validation
- Pricing
- Input
- Input Example
- API and MCP usage
- Output Structure
- Output Example

## Release Notes

### 🚀 v2.0 - Coming Soon

> **Automated lead discovery** - automatically find and scrape new leads, including their full imprint data, without providing URLs manually.

### 🔌 v1.3 - API and MCP readiness

- **API and MCP usage guide** - new README section with copyable `curl`, `apify-client` (JavaScript), and Apify MCP examples
- **Improved schema descriptions** - input, output, and dataset descriptions sharpened for programmatic and AI tool callers; no field names or runtime behavior changed

### ⚡ v1.2 - Faster processing & smarter AI analysis

- **Improved parallel processing** - Actor is now 50% faster
- **Improved imprint analysis with fallbacks** - LLM is always used for the best result
- **Added "PerformanceMax" option** - for faster processing (requires at least 2 GB RAM)
- **Improved log formatting**
- **`imprint_url` is `null` when not found** - if the imprint URL is not found, it will now show as `null`
- **New `imprint_status` field** - indicates the outcome of imprint URL discovery (`FOUND`, `NOT_FOUND`, `FETCH_ERROR`, `URL_ERROR`, `ERROR`, `UNKNOWN`)

### 🔧 v1.1 - Bug fixes & reliability improvements

- **Reliability fixes** - graceful charge-limit handling under concurrency, input-schema cleanup, and several scraper edge-case fixes
- **Improved AI analysis reliability** - more robust handling of LLM responses with multi-provider fallback
- **Slimmer Build image** - faster cold starts and smaller pulls

### 🎉 v1.0 - Initial public release

- **AI-powered imprint detection** - finds *Impressum* links even when traditional parsing fails
- **Intelligent scraping engine** - automatically switches between a lightweight fast mode and a full browser mode depending on the website's complexity
- **Comprehensive email validation** - syntax, MX records, disposable filter, role-based detection, alias resolution, typo suggestions and live status tracking
- **Per-field privacy toggles** - disable any output field you don't need (e.g. `disableEmail`, `disableVatId`)
- **Pay-per-event pricing** - only pay for processed websites and (optionally) validated emails

## Features

🤖 **AI-Powered Link Detection:** Uses AI to find imprint page links when traditional parsing fails

🧠 **Smart Contact Extraction:** Extracts comprehensive contact and company information

🇩🇪 **German Website Optimization:** Specifically optimized for German website structures and imprint pages

🛡️ **Robust Error Handling:** Built-in retry mechanisms and comprehensive error handling

📊 **Detailed Output:** Structured data with contact person, company details, and legal information

🌐 **Proxy Support:** Optional proxy configuration for enhanced reliability

### Advanced Email Validation

When enabled, the Actor performs comprehensive email validation using multiple verification methods:

- **Syntax validation** - Ensures proper email format
- **Domain existence check** - Verifies the domain is active and reachable
- **MX record validation** - Confirms the domain can receive emails
- **Disposable email detection** - Filters out temporary/disposable email addresses
- **Role-based email detection** - Identifies generic addresses (info@, admin@, etc.)
- **Email alias detection** - Detects aliases for major providers (Gmail, Yahoo, Outlook/Hotmail)
- **Typo suggestions** - Provides corrections for common email typos
- **Real-time monitoring** - Live validation status tracking

This ensures you only get high-quality, deliverable email addresses for your lead generation campaigns.

## Pricing

| Cost item | Rate |
| --- | --- |
| Successful data extraction | $3.00 / 1,000 results |
| Website processing fee | $0.60 / 1,000 websites |
| Email validation service | $2.50 / 1,000 validations |
| Actor start | $0.04 (infrequent) |
| Apify platform compute (RAM/time) | Billed by Apify platform pricing |

> **Cost per lead: ~$0.004** - stays constant regardless of run size.

Email validation is billed separately at **$0.0025** per validated address when `validateEmail` is enabled.

### Cost Examples

**Scenario A: 100 URLs, ~90 successful imprints**

- Actor start: $0.04
- 100 websites processed: $0.06
- 90 successful results: $0.27
- **Total: $0.37**

**Scenario B: 500 URLs, ~430 successful imprints**

- Actor start: $0.04
- 500 websites processed: $0.30
- 430 successful results: $1.29
- **Total: ~$1.63**

## Input

The Actor accepts the following input parameters (see the **Input** tab in the Apify Console for the full, interactive schema):

| Parameter | Type | Required | Default | Description |
| --- | --- | --- | --- | --- |
| `targetUrls` | array | yes | — | Array of `{ "url": "..." }` objects (same shape for Console, API, and MCP). Invalid URLs are skipped and reported as input warnings. |
| `skipResultsWithoutEmail` | boolean | no | `false` | When enabled, results without an email address are not written to the dataset. |
| `maxRetries` | integer | no | `3` | Maximum retry attempts for failed requests (0–10). |
| `timeout` | integer | no | `5` | Per-request timeout in seconds (5–60). |
| `validateEmail` | boolean | no | `false` | Enable email validation; extra usage fees apply when on. |
| `proxyConfiguration` | object | no | — | Apify Proxy or custom proxy URLs (`useApifyProxy`, optional `proxyUrls`, `groups`, `countryCode`). |
| `performanceMax` | boolean | no | `false` | Higher parallelism; use only with at least 2 GB Actor memory. |
| `disableImprintUrl` | boolean | no | `false` | Omit `imprint_url` and `imprint_status` from each row. |
| `disableContactPerson` | boolean | no | `false` | Omit `contact_person` from each row. |
| `disableCompanyName` | boolean | no | `false` | Omit `company_name` from each row. |
| `disableCompanyAddress` | boolean | no | `false` | Omit `company_address` from each row. |
| `disablePhoneNumber` | boolean | no | `false` | Omit `phone_number` from each row. |
| `disableEmail` | boolean | no | `false` | Omit `email` and `email_status` from each row. |
| `disableRegisterNumber` | boolean | no | `false` | Omit `register_number` from each row. |
| `disableVatId` | boolean | no | `false` | Omit `vat_id` from each row. |
| `useHeadlessBrowser` | boolean | no | `false` | Not shown in Console. If true, force browser-based scraping for all URLs. |
| `enableAxiosRetry` | boolean | no | `true` | Not shown in Console. If true, axios-first scraping with browser fallback. |
| `retryOptions` | object | no | — | Not shown in Console. Retry trigger criteria for axios-first mode (`requireEmail`, `requireContactPerson`, `requireAnyField`, `minFieldsRequired`). |

### Input Example

```
{
  "targetUrls": [
    {"url": "https://example.de"},
    {"url": "https://another-site.de"}
  ],
  "skipResultsWithoutEmail": false,
  "maxRetries": 1,
  "timeout": 5,
  "validateEmail": true,
  "proxyConfiguration": {
    "useApifyProxy": false
  }
}
```

## API and MCP usage

Runs write dataset rows for each **valid input URL** that reaches processing. Every row includes `target_url` for deterministic input-output mapping. The Actor does not write a separate key-value `OUTPUT` record. Fetch rows from the default dataset after the run succeeds (or use the synchronous endpoint below).

**REST (sync, returns dataset items):** replace `YOUR_USERNAME`, `YOUR_API_TOKEN`, and use the same JSON body as in Input Example.

```
curl "https://api.apify.com/v2/acts/YOUR_USERNAME~german-imprint-scraper-v1beta/run-sync-get-dataset-items?token=YOUR_API_TOKEN" \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{"targetUrls":[{"url":"https://www.winning-solutions.de"}],"validateEmail":false}'
```

**JavaScript (`apify-client`):**

```
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const input = {
  targetUrls: [{ url: 'https://www.winning-solutions.de' }],
  validateEmail: false,
};
const run = await client.actor('YOUR_USERNAME~german-imprint-scraper-v1beta').call(input);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

**Apify MCP server (AI agents):** configure your MCP client with URL `https://mcp.apify.com?tools=YOUR_USERNAME~german-imprint-scraper-v1beta` (you can combine multiple tools per [Apify MCP docs](https://docs.apify.com/platform/integrations/mcp)). Pass the API token via your client (for example an `Authorization: Bearer ...` header), not inside the Actor input JSON.

## Output Structure

The Actor returns structured data for each processed URL. The table below lists the main fields. Optional dataset views in the Apify Console may show a subset or flattened columns. When **disable** options are enabled, the corresponding keys are omitted from each row.

| Field | Type | Description | Example Value |
| --- | --- | --- | --- |
| `target_url` | string | Original input URL that produced this row | `"https://example.de"` |
| `imprint_url` | string | Found impressum page URL, `null` when not found or an error occurred | `"https://example.de/impressum"` |
| `imprint_status` | string | Result of imprint URL discovery: `FOUND`, `NOT_FOUND`, `FETCH_ERROR`, `URL_ERROR`, `ERROR`, or `UNKNOWN` | `"FOUND"` |
| `contact_person.first_name` | string | First name of the contact person | `"Max"` |
| `contact_person.last_name` | string | Last name of the contact person | `"Mustermann"` |
| `contact_person.salutation` | string | Salutation (Herr/Frau/Dr.) | `"Herr"` |
| `company_name` | string | Full official company name | `"Example GmbH"` |
| `company_address.street` | string | Street name | `"Musterstraße"` |
| `company_address.house_number` | string | House number | `"123"` |
| `company_address.postalcode` | string | Postal code | `"12345"` |
| `company_address.city` | string | City name | `"Musterstadt"` |
| `phone_number` | string | Contact phone number | `"+49 123 456789"` |
| `email` | string | Contact email address | `"info@example.de"` |
| `email_status` | string | With validation: `DELIVERABLE`, `UNDELIVERABLE`, `UNKNOWN`, or `MISSING_EMAIL` if no email was found | `"DELIVERABLE"` |
| `register_number` | string | Commercial register number / Handelsregisternummer | `"HRB 12345"` |
| `vat_id` | string | VAT ID number / Umsatzsteuer-Id | `"DE123456789"` |
| `retryTriggered` | boolean | Whether retry was triggered during scraping | `false` |
| `retryReasons` | array | Array of reasons why retry was triggered (optional) | `["email is empty"]` |
| `_metadata.websiteProcessed` | boolean | Whether the website was successfully processed | `true` |
| `_metadata.resultCharged` | boolean | Whether this result was charged | `true` |
| `_metadata.emailValidated` | boolean | Whether email validation was performed | `true` |
| `_metadata.limitReached` | boolean | Whether usage limit was reached | `false` |
| `_metadata.error` | string | Present when the row records a top-level run failure | *(varies)* |
| `_metadata.errorContext` | mixed | Extra debugging context when `error` is set | *(varies)* |

### Output Example

```
{
  "target_url": "https://example.de",
  "imprint_url": "https://example.de/impressum",
  "imprint_status": "FOUND",
  "contact_person": {
    "first_name": "Max",
    "last_name": "Mustermann",
    "salutation": "Herr"
  },
  "company_name": "Example GmbH",
  "company_address": {
    "street": "Musterstraße",
    "house_number": "123",
    "postalcode": "12345",
    "city": "Musterstadt"
  },
  "phone_number": "+49 123 456789",
  "email": "info@example.de",
  "email_status": "DELIVERABLE",
  "register_number": "HRB 12345",
  "vat_id": "DE123456789",
  "retryTriggered": false,
  "retryReasons": [],
  "_metadata": {
    "websiteProcessed": true,
    "resultCharged": true,
    "emailValidated": true,
    "limitReached": false
  }
}
```