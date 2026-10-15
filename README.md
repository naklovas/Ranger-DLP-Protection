<div align="center">

# 🛡️ Ranger DLP — Enterprise Data Guard

### *Paste with confidence. Your secrets stay yours.*

**A lightweight, zero-latency browser extension that stops sensitive data from leaking into AI assistants, chat tools, ticketing systems and web forms — before it ever leaves your clipboard.**

![Manifest V3](https://img.shields.io/badge/Manifest-V3-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)
![Rules](https://img.shields.io/badge/Detection_Rules-30-success?style=for-the-badge)
![Telemetry](https://img.shields.io/badge/Telemetry-Zero-critical?style=for-the-badge)
![Processing](https://img.shields.io/badge/Processing-100%25_Local-blueviolet?style=for-the-badge)

[Why Ranger DLP?](#-why-ranger-dlp) •
[How It Works](#%EF%B8%8F-how-it-works) •
[Protection Modes](#-dual-protection-modes) •
[30 Rules](#-the-30-rule-detection-matrix) •
[Use Cases](#-real-world-use-cases) •
[Privacy](#-privacy--security-by-design) •
[FAQ](#-faq)

</div>

---

## 🌍 The Problem

Every day, developers and IT teams paste thousands of lines of text into AI assistants, chat apps and support portals:

- a **stack trace** that happens to include a database connection string,
- a **`.env` or config file** with a live API key buried on line 87,
- a **customer log** containing an IBAN, a credit card number or a national ID,
- a **curl command** with a `Bearer` token still attached.

Nobody does it on purpose. It happens in a hurry, at 2 AM, during an incident. And once that text is submitted to a third-party service, **you can no longer take it back** — it may be logged, cached, retained or used for training.

**Ranger DLP is the safety net that catches those mistakes at the exact moment they happen: the paste.**

---

## 🚀 Why Ranger DLP?

| | |
|---|---|
| ⚡ **Zero-Latency Inspection** | Large error logs, multi-line stack traces and full JSON payloads are scanned in milliseconds, directly in the browser — no lag, no spinner, no interruption to your flow. |
| 🧠 **Built for the AI Era** | Designed around the way people really use ChatGPT, Claude, Gemini, Copilot and similar tools: big, messy, copy-pasted blocks of text. |
| 🎭 **Dual Protection Modes** | Choose between *smart masking* (keep working, secrets redacted) and *hard blocking* (stop the paste entirely). |
| 🔍 **30 Enterprise Rules** | Cloud credentials, tokens, private keys, financial data, PII and infrastructure details — covered out of the box. |
| 🔒 **100% Local & Private** | No servers, no accounts, no analytics. Everything runs inside your browser's memory and nothing is ever sent anywhere. |
| 🪶 **Lightweight** | No heavy dependencies, no background bloat. It stays out of your way until it is needed. |
| 🎛️ **Fully Configurable** | Enable or disable each rule individually and pick the protection mode that fits your team's policy. |

---

## ⚙️ How It Works

Ranger DLP sits quietly between your clipboard and the web page. When you **paste** or **drag & drop** text, the extension inspects it *before* the page receives it.

```mermaid
flowchart LR
    A[📋 You paste or drop text] --> B{🛡️ Ranger DLP<br/>local scan<br/>30 rules}
    B -- Clean --> C[✅ Text pasted as-is]
    B -- Sensitive data found --> D{Protection mode}
    D -- Mask --> E[🎭 Secrets redacted<br/>text pasted safely]
    D -- Block --> F[⛔ Paste cancelled<br/>user warned]
```

1. **Intercept** — The paste / drop event is captured before it reaches the website.
2. **Inspect** — The text is run through the 30-rule pattern engine, entirely in local memory.
3. **Act** — Depending on your settings, sensitive values are masked or the action is blocked.
4. **Forget** — Nothing is stored, logged or transmitted. The inspected text simply passes through.

---

## 🎭 Dual Protection Modes

### 1. Mask Data (`***`) — *Keep working, stay safe*

Sensitive values are automatically redacted while the **last 2 characters are preserved**, so you (and the AI) still have enough context to debug.

**Before:**

```text
ERROR 2026-10-15 02:14:07 Connection failed
  at db.connect(postgres://admin:S3cr3tP@ss@10.0.4.12:5432/prod)
  aws_access_key_id = AKIAIOSFODNN7EXAMPLE
  card_number = 4111 1111 1111 1111
```

**After Ranger DLP:**

```text
ERROR 2026-10-15 02:14:07 Connection failed
  at db.connect(*********************************************od)
  aws_access_key_id = ******************LE
  card_number = *****************11
```

The structure of the log stays intact — the stack trace, the error message, the line numbers — only the dangerous parts are gone.

### 2. Block Action — *Zero tolerance*

When sensitive data is detected, the paste or drop is **cancelled instantly** and you are warned. Ideal for high-security environments and for anyone who prefers to review and clean the text manually.

---

## 🔍 The 30-Rule Detection Matrix

Ranger DLP ships with **30 pre-configured enterprise rules**, grouped into five protection layers.

### ☁️ Layer 1 — Cloud & API Secrets

| # | Rule | What it catches |
|:-:|------|-----------------|
| 1 | **AWS Access Key ID** | `AKIA…` / `ASIA…` infrastructure credentials |
| 2 | **AWS Secret Access Key** | 40-character secret keys paired with access keys |
| 3 | **GitHub Tokens** | `ghp_`, `gho_`, `ghs_`, `github_pat_` personal and app tokens |
| 4 | **Google Cloud API Key** | `AIza…` service and API keys |
| 5 | **Slack Tokens** | `xoxb-`, `xoxp-`, `xoxa-` bot and user tokens |
| 6 | **Stripe Live Secret Key** | `sk_live_…` production payment keys |
| 7 | **Generic API Secrets** | `api_key`, `apikey`, `client_secret`, `secret_key` assignments |

### 🔑 Layer 2 — Authentication & Database Infrastructure

| # | Rule | What it catches |
|:-:|------|-----------------|
| 8 | **JSON Web Tokens (JWT)** | Session and access tokens starting with `eyJ…` |
| 9 | **Private Key Blocks** | `-----BEGIN (RSA / EC / OPENSSH) PRIVATE KEY-----` blocks |
| 10 | **Bearer / OAuth Tokens** | `Authorization: Bearer …` headers |
| 11 | **Hardcoded Passwords** | `password = "…"`, `passwd`, `pwd` assignments |
| 12 | **Database Connection Strings** | PostgreSQL, MySQL, MongoDB, Redis and MSSQL URIs with embedded credentials |

### 🪪 Layer 3 — Personal & Identity Data (PII)

| # | Rule | What it catches |
|:-:|------|-----------------|
| 13 | **National ID Number** | Citizen identification numbers (with checksum validation) |
| 14 | **Social Security Number (SSN)** | US-format social security numbers |
| 15 | **Passport Number** | International passport identifiers |
| 16 | **Medical Record Number (MRN)** | Healthcare record identifiers |
| 17 | **Date of Birth** | Birth dates in common formats |
| 18 | **Phone Number** | Mobile and landline numbers in international formats |
| 19 | **Corporate Tax ID (VAT / VKN)** | Company tax identification numbers |

### 💳 Layer 4 — Financial & Crypto Assets

| # | Rule | What it catches |
|:-:|------|-----------------|
| 20 | **Credit / Debit Cards** | 13–16 digit card numbers with Luhn validation |
| 21 | **IBAN** | International bank account numbers |
| 22 | **SWIFT / BIC Codes** | Interbank routing codes |
| 23 | **Bitcoin Wallets** | `bc1…`, `1…`, `3…` addresses |
| 24 | **Ethereum Wallets** | `0x…` 40-hex-character addresses |

### 🌐 Layer 5 — Network, Assets & Corporate Information

| # | Rule | What it catches |
|:-:|------|-----------------|
| 25 | **Private IPv4 Addresses** | Internal ranges `10.x`, `172.16–31.x`, `192.168.x` |
| 26 | **IPv6 Addresses** | Internal and link-local IPv6 addresses |
| 27 | **MAC Addresses** | Hardware network interface identifiers |
| 28 | **Vehicle Identification Number (VIN)** | 17-character vehicle chassis numbers |
| 29 | **License Plates** | Vehicle registration plates |
| 30 | **Confidentiality Markers** | Text labelled `CONFIDENTIAL`, `STRICTLY CONFIDENTIAL`, `INTERNAL ONLY` |

> 💡 Every rule can be toggled on or off individually from the extension settings, so you can tune detection to your organisation's policy and reduce noise.

---

## 🧑‍💻 Real-World Use Cases

### 🤖 Asking an AI to debug a production error
You copy 300 lines of logs into an AI assistant. Somewhere inside: a MongoDB URI with a password and a JWT. Ranger DLP masks both — the AI still sees the error, but not your credentials.

### 🎫 Opening a support ticket
A customer complaint includes their IBAN and phone number. You paste it into an external ticketing system — Ranger DLP redacts the personal data automatically.

### 💬 Sharing config in a chat channel
You drop a `docker-compose.yml` into a team chat to ask a quick question. The `STRIPE_SECRET_KEY` line never makes it through.

### 🏢 Enforcing company policy
Security teams can standardise on **Block** mode, so that production secrets simply cannot be pasted into unapproved web tools.

---

## 👥 Who Is It For?

- **Software developers** who use AI assistants daily for debugging and code review
- **DevOps / SRE engineers** handling logs, configs and infrastructure during incidents
- **IT & security teams** looking for a lightweight first line of defence against accidental leaks
- **Support & operations staff** working with customer data in web-based tools
- **Anyone** who has ever thought *"wait… did I just paste that?"*

---

## 🔒 Privacy & Security by Design

Ranger DLP is built on a simple principle: **a data protection tool must never become a data leak itself.**

- 🚫 **No data collection** — we do not collect, transmit, store or share clipboard contents, browsing history, personal data or telemetry.
- 💻 **100% client-side** — all inspection and masking happen locally, in browser memory.
- 🌐 **No external calls** — the extension does not contact any server.
- 🗄️ **Local settings only** — your preferences and rule configuration are kept on your own device via standard browser storage APIs.
- 🧹 **Nothing is retained** — inspected text is not saved or logged.

Read the full [Privacy Policy](PRIVACY.md).

> ⚖️ **Compliance note:** Ranger DLP helps teams follow good data-handling practice in the spirit of regulations such as **GDPR, KVKK, HIPAA and PCI-DSS** by reducing accidental exposure. It is a preventive tool, not a certification, and does not on its own make an organisation compliant.

---

## 🧭 Design Principles

1. **Privacy first** — if it needs a server, it does not belong in Ranger DLP.
2. **Never slow the user down** — protection must be invisible until it matters.
3. **Context over censorship** — mask just enough to protect, keep enough to stay useful.
4. **User in control** — every rule and every mode is the user's choice.

---

## ❓ FAQ

<details>
<summary><b>Does Ranger DLP read everything I type?</b></summary>

No. It only inspects text at the moment of a **paste** or **drag & drop** event, and only locally. Nothing is recorded or sent anywhere.
</details>

<details>
<summary><b>Does it work with ChatGPT, Claude, Gemini and other AI tools?</b></summary>

Yes. Ranger DLP works at the browser level, so it protects paste and drop actions on any website — AI assistants, chat apps, ticketing systems, forms and more.
</details>

<details>
<summary><b>Will it slow down my browser?</b></summary>

No. Inspection runs in milliseconds, even on large logs, and the extension does nothing until you paste or drop text.
</details>

<details>
<summary><b>Why keep the last 2 characters when masking?</b></summary>

So you can still tell values apart and keep debugging context (e.g. "the key ending in `LE` failed") without exposing the secret itself.
</details>

<details>
<summary><b>Can it catch 100% of sensitive data?</b></summary>

No pattern-based tool can guarantee that. Ranger DLP is a strong safety net for the most common and most dangerous leak types — it complements, but does not replace, good security habits and secret management.
</details>

---

## 🇹🇷 Türkçe Özet

**Ranger DLP**, yazılımcıların, IT ekiplerinin ve kurumsal kullanıcıların hata loglarını, yapılandırma dosyalarını ve büyük metin bloklarını yapay zekâ asistanlarına ya da başka web araçlarına yapıştırırken **hassas verileri yanlışlıkla sızdırmasını önleyen** bir tarayıcı eklentisidir.

- **30 hazır kural:** AWS / GitHub / Slack / Stripe anahtarları, JWT, özel anahtarlar, veritabanı bağlantı cümleleri, TC Kimlik No, IBAN, kredi kartı, vergi numarası, iç IP adresleri ve daha fazlası.
- **İki koruma modu:** *Maskeleme* (son 2 karakter korunarak `***` ile gizleme) veya *Engelleme* (yapıştırma işlemini tamamen durdurma).
- **%100 yerel çalışma:** Hiçbir veri hiçbir sunucuya gönderilmez; tüm analiz tarayıcı belleğinde, milisaniyeler içinde yapılır.

---

## 📄 License

Copyright © 2026 **Volkan Işıkhan**. All rights reserved.
See [LICENSE](LICENSE) for details.

<div align="center">

**🛡️ Ranger DLP — Enterprise-grade protection for the modern, AI-powered web.**

</div>
