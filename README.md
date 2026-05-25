# Token.io (token-io)
Token.io is an Open Banking infrastructure provider offering A2A (Account-to-Account) payments and account information services across Europe. Founded in 2016 and FCA-authorised since 2018, Token.io was the first payment initiation service provider to conduct an end-to-end PSD2-compliant Open Banking transaction. The Token.io platform connects developers and TPPs to over 4,000 banks via a single standardised API supporting Payment Initiation Services (PIS), Account Information Services (AIS), Variable Recurring Payments (VRP), refunds, payouts, settlement accounts, account verification, and Pay-by-Link checkout.

**URL:** [Visit APIs.json](https://raw.githubusercontent.com/api-evangelist/token-io/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

- Open Banking, Payments, AIS, PIS, VRP, PSD2, A2A Payments, Pay by Bank, Financial Services

## Timestamps

- **Created:** 2026-05-25
- **Modified:** 2026-05-25

## Products

| Product | Description |
|---|---|
| Payments v2 | Single immediate and future-dated A2A payment initiation |
| Variable Recurring Payments (VRP) | Sweeping and commercial (non-sweeping) recurring payment mandates |
| Data (AIS) | Account information — balances, transactions, standing orders |
| Pay by Link | Reusable payment URLs with amount and usage limits |
| Account on File | Tokenized bank account references for repeat payments |
| Refunds | Refund initiation tied to original payment transactions |
| Payouts | Outbound transfer execution and monitoring |
| Settlement Accounts | Virtual accounts and settlement rules |
| Account Verification | Name / account-holder confirmation checks |
| Banks v1 & v2 | Discovery of 4,000+ connected banks across Europe |
| Sub-TPPs | Sub-TPP entity management for reseller / platform models |
| Webhooks | Event notifications for payments, VRP, AIS lifecycle |
| Reports | Bank status monitoring across AIS and PIS |

## APIs

### Token.io Open Banking API
Token.io's Open Banking API for Third Party Providers (TPPs) — covers Payment Initiation Services (PIS), Account Information Services (AIS), Variable Recurring Payments (VRP), refunds, payouts, settlement accounts, account verification, Pay-by-Link, and bank discovery across 4,000+ European banks. JWT-authenticated production API at `https://api.token.io` with sandbox access via `dashboard.sandbox.token.io`.

**Human URL:** [https://docs.token.io/products/tpp/api/reference](https://docs.token.io/products/tpp/api/reference)
**Base URL:** `https://api.token.io`

- [Documentation](https://docs.token.io/products/tpp/api/reference)
- [API Reference](https://reference.token.io/)
- [Getting Started](https://docs.token.io/products/tpp)
- [OpenAPI Source](https://docs.token.io/_bundle/products/tpp/api/reference/index.yaml)
- [OpenAPI (local)](openapi/token-io-openapi.yml)
- [JSON Schema — Payment](json-schema/token-io-payment-schema.json)
- [JSON Schema — VRP Consent](json-schema/token-io-vrp-consent-schema.json)
- [JSON Schema — Account](json-schema/token-io-account-schema.json)
- [JSON-LD Context](json-ld/token-io-context.jsonld)

## Naftiko Capabilities

| Capability | Surface |
|---|---|
| [Payments v2](capabilities/payments-v2.yaml) | Initiate, list, and retrieve single immediate / future-dated payments |
| [Variable Recurring Payments](capabilities/variable-recurring-payments.yaml) | Create VRP consents, initiate VRP payments |
| [Data (AIS) — Accounts](capabilities/data-accounts.yaml) | Accounts, balances, transactions, standing orders |
| [Banks](capabilities/banks.yaml) | Bank discovery and country list |
| [Refunds](capabilities/refunds.yaml) | Refund initiation and tracking |
| [Payouts](capabilities/payouts.yaml) | Payout initiation and monitoring |
| [Settlement Accounts](capabilities/settlement-accounts.yaml) | Virtual account management |
| [Webhooks](capabilities/webhooks.yaml) | Webhook configuration |
| [Pay by Link](capabilities/pay-by-link.yaml) | Reusable payment links |

## SDKs and Samples

| Repo | Language | Purpose |
|---|---|---|
| [sdk-js](https://github.com/tokenio/sdk-js) | JavaScript / Node | Token System and Open Banking client |
| [sdk-php](https://github.com/tokenio/sdk-php) | PHP | Token System client |
| [sdk-csharp](https://github.com/tokenio/sdk-csharp) | C# / .NET | Token System client |
| [sdk-objc](https://github.com/tokenio/sdk-objc) | Objective-C | iOS native client |
| [tokenio-ios-webview-sdk](https://github.com/tokenio/tokenio-ios-webview-sdk) | Swift | iOS Hosted Payments webview |
| [tokenio-android-webview-sdk](https://github.com/tokenio/tokenio-android-webview-sdk) | Kotlin | Android Hosted Payments webview |
| [merchant-sample-java](https://github.com/tokenio/merchant-sample-java) | Java | Merchant checkout sample |
| [merchant-sample-js](https://github.com/tokenio/merchant-sample-js) | JavaScript | Merchant checkout sample |
| [bank-sample-java](https://github.com/tokenio/bank-sample-java) | Java | Bank Integration API sample |
| [pfm-sample-java](https://github.com/tokenio/pfm-sample-java) | Java | Personal finance / Access Tokens sample |
| [merchant-integration-workshop](https://github.com/tokenio/merchant-integration-workshop) | HTML | Hands-on integration workshop |

## Commercial

- [Plans / Pricing (API Commons Plans 0.1)](plans/token-io-plans-pricing.yml)
- [Rate Limits (API Commons Rate Limits 0.1)](rate-limits/token-io-rate-limits.yml)
- [FinOps (FOCUS 1.3)](finops/token-io-finops.yml)

## Compliance and Licensing

- FCA-authorised UK Payment Initiation Service Provider (PISP) and Account Information Service Provider (AISP) since 2018
- PSD2-compliant
- Listed on the [UK Open Banking regulated providers register](https://www.openbanking.org.uk/regulated-providers/token/)

## Common Links

- [Portal](https://token.io)
- [Documentation](https://docs.token.io)
- [Getting Started](https://docs.token.io/products/tpp)
- [API Reference](https://reference.token.io/)
- [Sandbox Dashboard](https://dashboard.sandbox.token.io/signin)
- [Support](https://support.token.io)
- [GitHub Organization](https://github.com/tokenio)
- [Pricing](https://token.io/contact/pricing)
- [News](https://token.io/news)
- [Blog](https://token.io/blog)
- [FAQ](https://token.io/faq)
