# Standards & API Reference

> Project: Expense Management Platform · Generated: 2026-05-06

## Industry Standards & Specifications

### ISO Standards

**ISO 4217 — Codes for the Representation of Currencies and Funds**
- URL: https://www.iso.org/iso-4217-currency-codes.html
- Three-letter alphabetic currency codes (e.g., USD, EUR, GBP) and three-digit numeric equivalents. Any multi-currency expense platform must implement ISO 4217 to unambiguously represent amounts, exchange rate calculations, and VAT entries across jurisdictions.

**ISO 20022 — Financial Services Messaging Standard**
- URL: https://www.swift.com/standards/iso-20022
- XML-based universal financial messaging standard covering payments, remittances, and reporting. The US Fedwire Funds Service migrated to ISO 20022 in July 2025; Swift adopted MX message types in November 2025. Relevant to expense platforms for ACH reimbursement payloads (pain.001 credit transfer, pain.002 payment status) and remittance data. Nacha's ISO 20022-to-ACH Mapping Guide (https://www.nacha.org/content/iso-20022-ach-mapping-guide) provides translation guidance between ISO 20022 messages and ACH transactions.

**ISO 18245 — Merchant Category Codes (MCC)**
- URL: https://www.iso.org/standard/33365.html
- Defines the structure and meaning of four-digit merchant category codes used by Visa, Mastercard, Amex, and Discover. Expense platforms use MCCs to automatically categorise card transactions (e.g., 5812 = Eating Places/Restaurants, 3000–3299 = Airlines, 7011 = Hotels). Policy engines can restrict spend by MCC (e.g., no purchases at MCC 5813 Bars/Taverns without approval). Card networks publish their own MCC reference lists; the Stripe MCC guide (https://stripe.com/guides/merchant-category-codes) provides a practical consolidated lookup.

---

### W3C & IETF Standards

**RFC 6749 — The OAuth 2.0 Authorization Framework**
- URL: https://datatracker.ietf.org/doc/html/rfc6749
- The foundational authorization framework for delegated API access. All major expense management APIs (Ramp, Brex, Pleo, SAP Concur, Spendesk, Navan) use OAuth 2.0 to issue access tokens for third-party integrations. Required for any expense platform exposing a developer API or consuming bank and card feeds.

**RFC 7636 — Proof Key for Code Exchange (PKCE) for OAuth 2.0**
- URL: https://datatracker.ietf.org/doc/html/rfc7636
- Extends the OAuth 2.0 Authorization Code flow to prevent authorization code interception attacks. Mandatory for public clients (mobile and SPA expense apps) accessing expense and bank feed APIs.

**RFC 8414 — OAuth 2.0 Authorization Server Metadata**
- URL: https://datatracker.ietf.org/doc/html/rfc8414
- Enables discovery of authorization server endpoints. Required for interoperable OAuth implementations across ERP and bank integrations.

**OpenID Connect Core 1.0**
- URL: https://openid.net/specs/openid-connect-core-1_0.html
- Identity layer on top of OAuth 2.0; enables SSO for expense platform user authentication. All enterprise expense platforms support OIDC for integration with Okta, Azure AD, and Google Workspace identity providers.

**RFC 7231 — HTTP/1.1 Semantics and Content**
- URL: https://datatracker.ietf.org/doc/html/rfc7231
- Baseline HTTP semantics governing all REST API interactions. Expense management REST APIs follow HTTP verb conventions (GET for retrieval, POST for submission, PATCH for updates).

**RFC 8288 — Web Linking (Link Header)**
- URL: https://datatracker.ietf.org/doc/html/rfc8288
- Defines the Link header for pagination in REST APIs. Relevant for expense transaction feeds and reporting endpoints returning large result sets.

---

### Data Model & API Specifications

**OpenAPI Specification (OAS) 3.1**
- URL: https://spec.openapis.org/oas/v3.1.0
- The de facto standard for describing REST APIs using JSON or YAML schemas. Ramp, Brex, Pleo, and Spendesk publish OpenAPI specifications for their developer portals. An open-source expense platform should publish an OAS 3.1 specification to enable SDK auto-generation and third-party integration. SAP Concur publishes OpenAPI (Swagger) documentation at https://api.sap.com/products/SAPConcur/apis/REST.

**JSON Schema (Draft 2020-12)**
- URL: https://json-schema.org/specification
- Standard for defining the structure of JSON documents. Used for validating expense submission payloads, receipt metadata schemas, and webhook event bodies in expense APIs.

**FDX API — Financial Data Exchange**
- URL: https://financialdataexchange.org/
- The CFPB-recognised open banking standard-setting body for the US (recognised January 2025 under the Personal Financial Data Rights rule). FDX API v6.4/v6.5 enables standardised access to account information, transaction data, and payment information. Over 130 million consumer accounts now connected via FDX API (2026); large institutions must be CFPB-compliant by April 2026. Mastercard publishes an FDX Developer Hub at https://developer.mastercard.com/fdx-dev-hub/documentation. Critical for card transaction feed integration without proprietary card adoption.

**UK Open Banking Standard (Read/Write API v4.0)**
- URL: https://standards.openbanking.org.uk/
- Detailed API specifications for UK banks compliant with PSD2 and the FCA's Open Banking regime. Security profiles aligned with FAPI 1.0 Advanced. Relevant for any expense platform serving UK/EU markets and ingesting corporate bank transaction feeds.

**Nacha ACH Operating Rules**
- URL: https://www.nacha.org/content/standards
- Governs ACH credit transfer for employee expense reimbursements in the US. Expense reimbursement disbursement via ACH must comply with Nacha rules on entry types (PPD for individual employees, CCD for business-to-business). Updated ISO 20022-to-ACH mapping published by Nacha enables structured remittance data alongside reimbursement payments.

---

### Security & Authentication Standards

**PCI DSS v4.0 — Payment Card Industry Data Security Standard**
- URL: https://www.pcisecuritystandards.org/
- Applies to expense platforms that store, process, or transmit corporate card transaction data. PCI DSS v4.0 (effective April 2024, full compliance required March 2025) introduces enhanced API security requirements including: requirement 6.2 for bespoke code review, requirement 11.6 for detection of unauthorized changes to payment pages, and requirement 12.3.2 for targeted risk analysis. Expense platforms using Plaid or FDX card feeds without storing card numbers may qualify for reduced scope under SAQ-A.

**Financial-grade API (FAPI) 1.0 Advanced — OpenID Foundation**
- URL: https://openid.net/specs/openid-financial-api-part-2-1_0.html
- Security profile for OAuth 2.0 designed for high-value financial API scenarios. Requires: PAR (Pushed Authorisation Requests, RFC 9126), mTLS sender-constrained access tokens, and JAR (JWT-Secured Authorisation Requests, RFC 9101). The UK Open Banking Standard and PSD2 require FAPI 1.0 Advanced for Account Information Service Providers. Relevant for expense platforms consuming regulated bank feeds in the UK and EU.

**FAPI 2.0 Security Profile**
- URL: https://openid.net/specs/fapi-security-profile-2_0.html
- Next-generation financial API security profile simplifying FAPI 1.0 while maintaining security guarantees; FAPI 2.0 Attacker Model replaces implicit flow entirely. Emerging standard for new financial API implementations; relevant for greenfield expense platforms targeting EU/UK regulated markets.

**OWASP API Security Top 10 (2023 edition)**
- URL: https://owasp.org/API-Security/
- The primary reference for API security risk assessment in financial applications. APIs are the primary attack vector in 83% of cloud-native application breaches (Gartner, 2025). For expense management APIs the highest-risk categories are: API1 (Broken Object Level Authorization — employees accessing other employees' expense data), API2 (Broken Authentication — token compromise enabling fraudulent reimbursement submissions), and API4 (Unrestricted Resource Consumption — bulk receipt uploads or reporting queries). OWASP Top 10:2025 (https://owasp.org/Top10/2025/) covers web application risks applicable to expense management dashboards.

**NIST SP 800-63B — Digital Identity Guidelines (Authentication)**
- URL: https://pages.nist.gov/800-63-3/sp800-63b.html
- US government standard for digital identity and authentication assurance levels. Relevant to enterprise expense platforms integrated with US federal contractor IRS Accountable Plan compliance requirements, and for any platform storing employee financial data.

---

### Regulatory Frameworks

**IRS Accountable Plan Rules (IRC §62(a)(2)(A), IRS Publication 463)**
- URL: https://www.irs.gov/publications/p463
- US tax law governing tax-free reimbursement of employee business expenses. Three requirements: business connection, substantiation within 60 days, and return of excess reimbursements within 120 days. Reimbursements at or below GSA per diem rates are automatically tax-free under IRS Revenue Procedure 2019-48 (updated annually via Notice 2024-68 for FY2026). Expense platforms must enforce these rules to enable customers to claim reimbursements as non-taxable.

**GSA Per Diem Rates API**
- URL: https://open.gsa.gov/api/perdiem/
- US General Services Administration open API returning per diem rates as JSON by city, state, or ZIP code. FY2026 standard CONUS rate: $178/day ($110 lodging + $68 M&IE). Expense platforms should integrate this API for automatic per diem limit enforcement rather than maintaining static rate tables. Free, no authentication required.

**EU VAT Directive 2006/112/EC and Refund Directives**
- URL: https://ec.europa.eu/taxation_customs/business/vat/eu-vat-rules-topic/vat-refunds_en
- EU Directive 2008/9/EC governs VAT refund claims for EU-established businesses incurring VAT in other EU member states; the EU 13th Directive covers non-EU businesses. Expense platforms targeting European markets must capture VAT amounts, rates, and jurisdiction codes for each expense to support VAT reclaim workflows. VAT rates vary by country and product category; the European Commission's VIES (VAT Information Exchange System) API at https://ec.europa.eu/taxation_customs/vies/ supports VAT number validation.

**GDPR — General Data Protection Regulation (EU) 2016/679**
- URL: https://gdpr.eu/
- Applies to all expense data for EU-resident employees regardless of where the platform is hosted. Expense platforms hold sensitive personal data: employee names, locations, merchant names, travel patterns, and spending behaviour. Compliance requirements: legal basis for processing (legitimate interest or employment contract), data minimisation, right to erasure, and data residency controls. GDPR fines now exceed €7.1 billion cumulative; maximum per-violation penalty is €20M or 4% of global annual turnover.

**CCPA / CPRA — California Consumer Privacy Act**
- URL: https://oag.ca.gov/privacy/ccpa
- Applies to expense platforms serving California employees at companies meeting CCPA size thresholds. By 2025, 21 US states have enacted comprehensive consumer data privacy laws with similar scope. Expense platforms must support data subject access requests (DSAR) for employee spending data and provide opt-out of data sale (if applicable).

**PSD2 — EU Payment Services Directive 2 (Directive 2015/2366/EU)**
- URL: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32015L2366
- Requires banks to provide API access to account data for authorised Third Party Providers (TPPs). Account Information Service Providers (AISPs) can retrieve transaction data with explicit customer consent. Expense platforms operating as AISPs in the EU can ingest corporate card and bank account transaction data via PSD2 APIs, enabling automatic receipt matching without proprietary card adoption.

---

## Similar Products — Developer Documentation & APIs

### SAP Concur

- **Description:** Enterprise travel and expense management platform with dominant Fortune 500 market share. REST API covers expense reports, receipts, travel requests, and user provisioning.
- **API Documentation:** https://developer.concur.com/ (Developer Center with OpenAPI/Swagger specs)
- **API Reference (SAP API Hub):** https://api.sap.com/package/ConcurExpense
- **SDKs/Libraries:** No official SDK; community libraries available; OpenAPI spec enables SDK generation
- **Developer Guide:** https://developers.sap.com/tutorials/data-to-value-conn-concur-part01.html
- **Standards:** REST/JSON, OAuth 2.0 for authentication, OpenAPI (Swagger) spec published
- **Authentication:** OAuth 2.0 (client credentials and authorization code flows)
- **Notes:** Expense Reports v3, Receipts v4, Request v4, User Provisioning v4 are current; older v1/v3 endpoints are being deprecated (User V1 Form Fields decommissioned June 2026). Bulk User v3.1 API decommissioned January 2025.

---

### Ramp

- **Description:** Corporate card and spend management platform with real-time AI policy enforcement and savings intelligence. Developer API provides scoped access to transactions, cards, users, reimbursements, and accounting exports.
- **API Documentation:** https://docs.ramp.com/
- **API Reference (Reimbursements):** https://docs.ramp.com/developer-api/v1/api/reimbursements
- **SDKs/Libraries:** No official SDK; OpenAPI spec available; sandbox environment pre-populated with sample data
- **Developer Guide:** https://docs.ramp.com/ (includes guides index, API reference, webhook reference, GraphQL playground, and OAuth playground)
- **Standards:** REST/JSON, GraphQL, OpenAPI 3.x spec, webhooks for real-time transaction events
- **Authentication:** OAuth 2.0 (client credentials); developer sandbox requires separate credentials
- **Notes:** Technology Partner Programme at https://ramp.com/technology-partnerships. Webhook events cover transactions, receipts, and reimbursements. US-centric card product limits international integration scope.

---

### Brex (Capital One)

- **Description:** Corporate card and expense platform acquired by Capital One (completed April 2026) for $5.15B. API provides access to card transactions, expenses, receipts, reimbursements, and accounting exports. New AI-native Accounting API announced for automated ERP integration.
- **API Documentation:** https://developer.brex.com/
- **Developer Guide:** https://truto.one/blog/how-to-integrate-the-brex-api-with-your-accounting-stack-2026-engineering-guide/ (2026 engineering integration guide)
- **SDKs/Libraries:** API documentation at developer.brex.com; SDK availability TBD post-acquisition
- **Standards:** REST/JSON; separate Transactions API and Expenses API (merged for full GL coding workflow)
- **Authentication:** OAuth 2.0
- **Notes:** Expenses API provides metadata (memos, category tags, linked receipts, approval statuses); Transactions API provides financial data (amount, date). Post-acquisition product direction under Capital One review; API continuity expected but pricing/access may change.

---

### Expensify

- **Description:** SMB/mid-market expense platform with SmartScan OCR and Concierge AI. Integration Server API supports large-scale account provisioning and expense report export/import. New Expensify (App) has a separate API.
- **API Documentation (Integration Server):** https://integrations.expensify.com/Integration-Server/doc/
- **API Documentation (New Expensify App):** https://mintlify.com/Expensify/App/developers/api/endpoints
- **Web Services API:** https://www.expensify.com/api-services.html (query and manipulate Expensify; JSON responses)
- **SDKs/Libraries:** No official SDK; GitHub integrations repository at https://github.com/Expensify/Integrations
- **Standards:** REST/JSON; partner credential system (partnerUserID + partnerUserSecret)
- **Authentication:** API key pair (partnerUserID and partnerUserSecret); generate at https://www.expensify.com/tools/integrations/
- **Notes:** Expensify API is not accepting new applications as of 2026 (enterprise customers only). Data returned in JSON. Use cases: programmatic expense report download, receipt submission, account provisioning for new hires.

---

### Pleo

- **Description:** European SMB corporate card and expense management platform. REST API with OpenAPI specification covers expenses, receipts, cards, and transactions. Developer portal includes sandbox, webhooks, OAuth playground, and Postman/Insomnia collections.
- **API Documentation:** https://developers.pleo.io/docs/pleo-introduction
- **API Reference:** https://developers.pleo.io/reference/getexpense
- **SDKs/Libraries:** SDK support in 7 languages (per developer portal); Postman and Insomnia collections provided
- **Standards:** REST/JSON, OpenAPI specification, webhooks
- **Authentication:** OAuth 2.0 and API Keys
- **Notes:** EU/EEA-focused; multi-currency support across EU member states. GET /expenses and GET /expense/{id}/receipt are core endpoints. Community-designed approach with ungated API spec and developer portal.

---

### Spendesk

- **Description:** European spend management platform combining corporate cards, invoices, and expense claims. Community-designed public API in beta; covers card issuance, transaction retrieval, expense claims, vendor management, accounting exports, and webhooks.
- **API Documentation:** https://developer.spendesk.com/
- **Quickstart Guide:** https://developer.spendesk.com/public/docs/quickstart
- **Standards:** REST/JSON, OpenAPI-compatible documentation; TLS encryption for all API traffic
- **Authentication:** OAuth 2.0 or API Keys; role-based access controls
- **Notes:** API is currently in beta; production access requires contact with Spendesk customer service. CFO-focused spend visibility platform; API enables embedding spend management into ERP, billing, and procurement workflows.

---

### Navan (formerly TripActions)

- **Description:** Integrated travel booking and expense management platform. REST API covers user management, travel data export, and expense transactions. API requires admin-level access credentials and special enablement from Navan support for expense-specific endpoints.
- **API Documentation:** https://app.navan.com/app/helpcenter/articles/travel/admin/other-integrations/navan-tmc-api-integration-documentation
- **Integrations Overview:** https://navan.com/integrations
- **Standards:** REST/JSON; OAuth 2.0 Bearer token authentication
- **Authentication:** OAuth 2.0 via POST /auth/v1/token (client credentials grant)
- **Notes:** GET /travel/v1/users supports cursor pagination; POST /travel/v1/users for provisioning. Expense Transaction API requires separate permission enablement. Navan Connect (250+ bank card enrolment without card switching) has no public API documentation.

---

### Plaid

- **Description:** Open banking connectivity platform enabling access to bank and card transaction data for 12,000+ financial institutions. Core use case for expense management: card transaction feed ingestion for automatic receipt matching and account reconciliation.
- **API Documentation:** https://plaid.com/docs/
- **Transactions API:** https://plaid.com/docs/api/products/transactions/
- **Transactions Introduction:** https://plaid.com/docs/transactions/
- **SDKs/Libraries:** Official libraries for Node.js, Python, Ruby, Java, Go (https://plaid.com/docs/libraries/)
- **Standards:** REST/JSON; webhooks (SYNC_UPDATES_AVAILABLE event type); /transactions/sync for incremental updates
- **Authentication:** OAuth 2.0 (Plaid Link for end-user consent); client_id + secret for server-to-server calls
- **Notes:** Up to 24 months of transaction history; 90%+ categorisation accuracy with enriched merchant names and MCC codes. PSD2-compliant for UK/EU via Plaid's open banking integrations. CFPB CPFR compliance (Personal Financial Data Rights, October 2024) aligns Plaid with FDX standard.

---

### ERPNext / Frappe Framework

- **Description:** Open-source ERP with GPL-3.0 Expense Claims module. Frappe Framework exposes all DocTypes (including Expense Claim) via a generic REST API; supports webhooks for outgoing events.
- **API Documentation:** https://docs.frappe.io/framework/user/en/api
- **Expense Claims Documentation:** https://docs.frappe.io/erpnext/v13/user/manual/en/human-resources/expense-claim
- **Unofficial API Docs:** https://github.com/alyf-de/frappe_api-docs
- **SDKs/Libraries:** No official SDK; REST API accessible from any HTTP client; Python and JavaScript client libraries available in community
- **Standards:** REST/JSON; generic CRUD endpoints for all DocTypes; event streaming for sync
- **Authentication:** API Key + API Secret (token-based)
- **Notes:** GPL-3.0 licence requires distributed derivatives to also be GPL-3.0. No native receipt OCR, card feed integration, or AI policy enforcement. REST API is feature-complete for expense claim CRUD but lacks dedicated endpoints for receipt matching or spend analytics. Suitable as integration target (ERP sync) for an AI-native expense platform.

---

## Notes

**Emerging Standards:**

- **FDX v6.5** (2025–2026): The FDX API is expanding data clusters to cover tax reporting and insurance data, broadening its relevance beyond traditional banking into the full expense and reimbursement lifecycle. Large US financial institutions face CFPB compliance deadlines by April 2026, which will significantly increase FDX API availability and adoption.

- **FAPI 2.0**: While FAPI 1.0 Advanced is the current deployed standard for regulated financial APIs in the UK and EU, FAPI 2.0 is being adopted by new implementations. Greenfield expense platforms should implement FAPI 2.0 from the outset to avoid needing to migrate.

- **ISO 20022 Remittance Data**: Full ISO 20022 adoption in Fedwire (July 2025) and Swift (November 2025) enables richer remittance data to accompany ACH reimbursements, supporting automated matching of disbursement to expense report at the employee's bank.

- **AI Receipt Fraud Detection Standards**: No formal standard yet exists for detecting AI-generated synthetic receipts. This is an actively evolving area; OWASP has not yet published guidance specific to AI-generated document fraud. An open-source expense platform could pioneer a reference implementation and propose standardisation through OWASP or ACFE (Association of Certified Fraud Examiners).

- **Merchant Category Code (MCC) Standard API**: While ISO 18245 defines MCCs, there is no single authoritative free API for MCC lookups. Card networks (Visa, Mastercard) publish reference lists but not as open APIs. Expense platforms typically maintain an internal MCC mapping table or use enrichment services (Plaid, Stripe Radar) that return MCC data with transaction objects.
