# Expense Management Platform

> Part of the [worlds-biggest-software-project](https://github.com/worlds-biggest-software-project) initiative.
>
> An AI-native, open-source expense management platform that pairs multi-modal receipt capture with natural-language policy enforcement and synthetic-fraud defence — without locking customers into a proprietary corporate card.

This project is a card-agnostic expense management platform for finance teams who want modern AI capabilities without surrendering their banking relationship. It targets the gap between legacy enterprise suites (SAP Concur, Emburse) and US-centric card-revenue platforms (Ramp, Brex), and aims to give SMB and mid-market companies — particularly outside the US — a serious open-source alternative.

---

## Why Expense Management Platform?

- **Incumbents tie expense intelligence to their card.** Ramp and Brex (now Capital One) deliver real-time policy enforcement only when customers adopt their corporate card; companies that cannot or will not switch card programmes are excluded from the AI-driven tier of the market.
- **Legacy suites are AI-bolt-on, not AI-native.** SAP Concur leads on global compliance but runs a 1990s-era architecture with bolted-on AI, dated UX, and policy configuration that requires IT involvement; user satisfaction lags newer competitors.
- **Synthetic receipt fraud is a 2025-era threat with no open-source defence.** The March 2025 OpenAI image-generation upgrade made high-quality fake receipts trivial to produce; current OCR-only validation is vulnerable, and no open-source platform addresses this gap.
- **Existing OSS options are functionally thin.** ERPNext Expense Claims and Odoo Community offer no receipt OCR, no AI policy enforcement, no real-time card feeds, and no mobile-first capture — they are accounting modules, not expense platforms.
- **Europe and the SMB segment are underserved.** Pleo addresses European SMBs but lacks enterprise policy depth; no GDPR-aware, VAT-reclaim-capable open-source alternative exists for EU companies.

---

## Key Features

### Receipt Capture and Data Extraction

- Mobile receipt capture with AI-powered OCR extraction of merchant, amount, date, currency, and VAT
- Multi-modal AI processing capable of handling damaged, handwritten, low-light, and non-standard receipt images
- Email-inbox forwarding with automatic receipt-to-transaction pairing
- Multi-currency expense handling using ISO 4217 currency codes
- Automatic VAT field extraction for EU expense reporting

### Policy Enforcement and Compliance

- Configurable policy rules engine: per-category limits, merchant category restrictions, and per-diem rates
- Natural-language policy rule engine that interprets plain-English policy statements via an LLM and enforces them without IT configuration
- Real-time point-of-purchase policy enforcement with immediate employee and manager notification
- Per diem / GSA rate integration for US government contractors
- VAT reclaim tracking aligned with EU Directive 2008/9/EC and the 13th Directive
- IRS Accountable Plan compliance reporting

### Fraud Detection and Audit

- Synthetic receipt fraud detection combining image metadata analysis (EXIF), merchant network verification, and geographic plausibility checks
- Behavioural anomaly scoring against each employee's historical merchant-category patterns
- Cross-employee pattern detection for collusion and duplicate-submission fraud
- Per-expense audit trail covering submission, review, and payment
- AI-driven flagging of high-risk expenses prior to approval

### Card and Banking Integration

- Card-agnostic transaction feeds via Open Banking APIs (Plaid, FDX, PSD2)
- Automatic receipt-to-transaction matching for any Visa or Mastercard feed
- Pluggable card adapters so customers retain their existing banking relationships
- Real-time spend feed with AI-categorised GL coding pushed automatically to the connected ERP

### Reimbursement, Spend Intelligence, and ERP Sync

- Employee reimbursement via ACH with payroll integration
- ERP synchronisation for GL posting (ERPNext, QuickBooks, Xero, NetSuite, Sage Intacct)
- HRIS integrations for card provisioning linked to onboarding (Gusto, Rippling, BambooHR)
- Duplicate subscription detection and preferred-vendor savings recommendations
- Natural-language spend queries for ad-hoc analysis without custom reporting

---

## AI-Native Advantage

Unlike incumbents that bolt AI onto rule-based architectures, this platform is structured around AI from the data layer up. Multi-modal vision-and-text models extract accurate data from receipts that defeat template OCR; an LLM-based policy engine accepts plain-English rules and enforces them at the point of swipe rather than at reimbursement; and a layered fraud-defence model — combining EXIF metadata analysis, merchant verification, and behavioural anomaly scoring — addresses the synthetic-receipt threat that emerged after the March 2025 generative-image upgrade. Spend intelligence is proactive rather than reactive: redundant subscriptions, sub-optimal vendors, and budget overruns are surfaced from real-time spend data before they compound.

---

## Tech Stack & Deployment

The platform is designed to be self-hostable for companies that need data residency or GDPR-aligned deployment, with a managed-cloud option for SMBs. Card and bank connectivity is built on Open Banking standards (Plaid and FDX in the US, PSD2 in the EU) so customers are not forced onto a proprietary card. ERP and HRIS connectivity is delivered through pre-built connectors for QuickBooks, Xero, NetSuite, Sage Intacct, ERPNext, Gusto, Rippling, and BambooHR, with a REST API for custom integrations. Compliance scope includes IRS Accountable Plan rules, EU VAT reclaim directives, GDPR, CCPA, and PCI DSS for card-data handling.

---

## Market Context

The global expense management software market is estimated at $8.48B–$9.29B in 2026 and projected to reach $12.86B–$15.86B by 2030–2032 at a 9.25%–11.1% CAGR (Mordor Intelligence; Fortune Business Insights). Commercial pricing ranges from $5/user/month (Expensify) to an estimated $8–$15/user/month for SAP Concur enterprise deployments, while Ramp and pre-acquisition Brex monetise via card interchange. Primary buyers are finance managers and controllers at 50–500-employee companies, CFOs at enterprises focused on fraud reduction and audit completeness, and procurement leads consolidating cards, expenses, and AP. Capital One's $5.15B acquisition of Brex (January 2026) and Ramp's $32B valuation indicate strong mainstream financial-institution interest in AI-driven corporate spend.

---

## Project Status

> This project is in the **research and specification phase**.  
> Contributions, feedback, and domain expertise are welcome.

---

## Contributing

We welcome contributions from developers, domain experts, and potential users.
See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

**Important:** All contributions must be your own original work or clearly attributed
open-source material with a compatible licence. Copyright infringement and licence
violations will not be tolerated and will result in immediate removal of the offending
contribution. If you are unsure whether a piece of code, text, or other material is
safe to contribute, open an issue and ask before submitting.

---

## Licence

Licence to be determined. The research notes flag GPL-3.0 (ERPNext) and LGPL-3.0 (Odoo Community) as relevant precedents in the open-source expense space; final licence selection will balance contributor reach against derivative-work obligations. See [discussion](#) for context.
