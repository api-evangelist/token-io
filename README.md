# token-io (token-io)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Token.io is an Open Banking infrastructure provider offering A2A (Account-to-Account) payments and account information services across Europe. Founded in 2016 and FCA-authorised since 2018, Token.io was the first payment initiation service provider to conduct an end-to-end PSD2-compliant Open Banking transaction. The Token.io platform connects developers and TPPs to over 4,000 banks via a single standardised API supporting Payment Initiation Services (PIS), Account Information Services (AIS), Variable Recurring Payments (VRP), refunds, payouts, settlement accounts, account verification, and Pay-by-Link checkout. Used by merchants, PSPs, fintechs, PFM apps, and platform businesses to replace card-rail payments and aggregate multibank data.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/token-io/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/token-io/refs/heads/main/apis.yml)

## Scope

- **Position:** Consuming

## Timestamps

- **Created:** 2026-05-25T00:00:00.000Z
- **Modified:** 2026-05-25

## APIs

### Token.io Open Banking API

Token.io's Open Banking API for Third Party Providers (TPPs). Enables authorized access to authenticated users' account information, initiation and tracking of single immediate and future-dated payments, variable recurring payments (VRP) for long-held consents, settlement-account based payments and refunds, payouts, account verification, and Pay-by-Link checkout flows. Supports Banks v1/v2, Sub-TPP management, webhooks, JWT-based authentication, and reporting across 4,000+ connected banks in Europe.

- **Human URL:** [https://docs.token.io/products/tpp/api/reference](https://docs.token.io/products/tpp/api/reference)
- **Base URL:** `https://api.token.io`

#### Tags

- Open Banking
- Payments
- Account Information
- AIS
- PIS
- VRP
- PSD2

#### Properties

- [Documentation](https://docs.token.io/products/tpp/api/reference)
- [Reference](https://reference.token.io/)
- [Getting Started](https://docs.token.io/products/tpp)
- [Open A P I Source](https://docs.token.io/_bundle/products/tpp/api/reference/index.yaml)
- [OpenAPI](openapi/token-io-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [JSON Schema](json-schema/token-io-payment-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/token-io-vrp-consent-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/token-io-account-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/token-io-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)

### Token.io JavaScript SDK

Official Token.io JavaScript SDK for Node.js and browser environments interacting with the Token System and Open Banking API.

- **Human URL:** [https://github.com/tokenio/sdk-js](https://github.com/tokenio/sdk-js)

#### Tags

- SDK
- JavaScript
- Node.js
- Browser

#### Properties

- [Source Code](https://github.com/tokenio/sdk-js)
- [SDK](https://github.com/tokenio/sdk-js)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Token.io PHP SDK

Official Token.io PHP SDK for interacting with the Token System and Open Banking API.

- **Human URL:** [https://github.com/tokenio/sdk-php](https://github.com/tokenio/sdk-php)

#### Tags

- SDK
- PHP

#### Properties

- [Source Code](https://github.com/tokenio/sdk-php)
- [SDK](https://github.com/tokenio/sdk-php)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Token.io C# SDK

Official Token.io C# / .NET SDK for the Open Banking API.

- **Human URL:** [https://github.com/tokenio/sdk-csharp](https://github.com/tokenio/sdk-csharp)

#### Tags

- SDK
- C#
- .NET

#### Properties

- [Source Code](https://github.com/tokenio/sdk-csharp)
- [SDK](https://github.com/tokenio/sdk-csharp)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Token.io Objective-C SDK

Official Token.io Objective-C SDK for iOS.

- **Human URL:** [https://github.com/tokenio/sdk-objc](https://github.com/tokenio/sdk-objc)

#### Tags

- SDK
- Objective-C
- iOS

#### Properties

- [Source Code](https://github.com/tokenio/sdk-objc)
- [SDK](https://github.com/tokenio/sdk-objc)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Token.io iOS Webview SDK

iOS webview SDK for embedding Token.io Hosted Payments pages in native iOS apps.

- **Human URL:** [https://github.com/tokenio/tokenio-ios-webview-sdk](https://github.com/tokenio/tokenio-ios-webview-sdk)

#### Tags

- SDK
- iOS
- Swift
- Webview
- Hosted Payments

#### Properties

- [Source Code](https://github.com/tokenio/tokenio-ios-webview-sdk)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Token.io Android Webview SDK

Android webview SDK for embedding Token.io Hosted Payments pages in native Android apps.

- **Human URL:** [https://github.com/tokenio/tokenio-android-webview-sdk](https://github.com/tokenio/tokenio-android-webview-sdk)

#### Tags

- SDK
- Android
- Kotlin
- Webview
- Hosted Payments

#### Properties

- [Source Code](https://github.com/tokenio/tokenio-android-webview-sdk)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Merchant Sample (Java)

Java merchant checkout sample illustrating Token.io payment initiation flows.

- **Human URL:** [https://github.com/tokenio/merchant-sample-java](https://github.com/tokenio/merchant-sample-java)

#### Tags

- Sample
- Java
- Merchant

#### Properties

- [Source Code](https://github.com/tokenio/merchant-sample-java)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Merchant Sample (JavaScript)

Simple JavaScript merchant checkout example for Token.io.

- **Human URL:** [https://github.com/tokenio/merchant-sample-js](https://github.com/tokenio/merchant-sample-js)

#### Tags

- Sample
- JavaScript
- Merchant

#### Properties

- [Source Code](https://github.com/tokenio/merchant-sample-js)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Bank Sample (Java)

Sample implementation of the Token Bank Integration API in Java.

- **Human URL:** [https://github.com/tokenio/bank-sample-java](https://github.com/tokenio/bank-sample-java)

#### Tags

- Sample
- Java
- Bank Integration

#### Properties

- [Source Code](https://github.com/tokenio/bank-sample-java)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Personal Finance Management Sample (Java)

Simple personal finance app illustrating Token.io's Access Tokens for AIS use cases.

- **Human URL:** [https://github.com/tokenio/pfm-sample-java](https://github.com/tokenio/pfm-sample-java)

#### Tags

- Sample
- Java
- PFM
- Access Tokens

#### Properties

- [Source Code](https://github.com/tokenio/pfm-sample-java)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Merchant Integration Workshop

Hands-on workshop for integrating a merchant with Token Checkout.

- **Human URL:** [https://github.com/tokenio/merchant-integration-workshop](https://github.com/tokenio/merchant-integration-workshop)

#### Tags

- Tutorial
- Workshop
- Merchant

#### Properties

- [Source Code](https://github.com/tokenio/merchant-integration-workshop)
- [Postman Collection](collections/token-io.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/token-io.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Portal](https://token.io)
- [Documentation](https://docs.token.io)
- [Getting Started](https://docs.token.io/products/tpp)
- [Reference](https://reference.token.io/)
- [Support](https://support.token.io)
- [Sandbox](https://dashboard.sandbox.token.io/signin)
- [GitHub Organization](https://github.com/tokenio)
- [Pricing](https://token.io/contact/pricing)
- [News](https://token.io/news)
- [Blog](https://token.io/blog)
- [F A Q](https://token.io/faq)
- [License](https://www.openbanking.org.uk/regulated-providers/token/)
- [Plans](plans/token-io-plans-pricing.yml)
- [Rate Limits](rate-limits/token-io-rate-limits.yml)
- [Fin Ops](finops/token-io-finops.yml)
- [Features](undefined)
- [Use Cases](undefined)

## Maintainers

**FN:** Kin Lane
**Email:** info@apievangelist.com
**URL:** https://apievangelist.com
