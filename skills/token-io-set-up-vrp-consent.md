---
name: token-io-set-up-vrp-consent
description: >-
  Set up a Variable Recurring Payments consent with a payer's bank through Token.io, initiate
  payments under it, and revoke it. Use for subscription, top-up and sweeping flows where the payer
  authorises once and you charge repeatedly.
api: Token.io's Open Banking API for TPPs
base_url: https://api.token.io
spec: openapi/token-io-variable-recurring-payments-api-openapi.yml
operations:
  - GetBanksv2
  - CreateVrpConsent
  - GetVrpConsent
  - GetVrpConsentPayments
  - ConfirmFunds
  - RevokeVrpConsent
generated: '2026-09-17'
method: generated
source: >-
  openapi/token-io-variable-recurring-payments-api-openapi.yml,
  https://docs.token.io/products/tpp/vrp/vrp-intro,
  https://docs.token.io/products/tpp/vrp/vrp-consent-revocation,
  conventions/token-io-conventions.yml
---

# Set up and use a VRP consent

VRP is the one Token.io flow where the payer's authorisation outlives the session. The consent is
the asset; payments are cheap once it exists, and mishandling the consent is the expensive mistake.

## Steps

1. **Check the bank supports it.** `GetBanksv2` (`GET /v2/banks`) exposes
   `supportsVariableRecurringPayment`. A bank without it will fail the consent, not the payment.
2. **Create the consent.** `CreateVrpConsent` (`POST /vrp-consents`) with the initiation block —
   the debtor, the creditor, and the limits the payer is agreeing to. The response carries the
   consent id (prefixed `vc:`).
3. **Send the payer to authorise.** The consent is authorised at the bank, through Hosted Pages or
   your own redirect. Subscribe to `VRP_CONSENT_STATUS_CHANGED` before you start so you learn when
   it reaches `AUTHORIZED`.
4. **Check funds before charging, where the bank supports it.** `ConfirmFunds`
   (`GET /vrps/{id}/confirm-funds`).
5. **Initiate payments under the consent** and follow each with `VRP_STATUS_CHANGED`. List what has
   been charged with `GetVrpConsentPayments` (`GET /vrp-consents/{id}/payments`).
6. **Revoke when the payer asks.** `RevokeVrpConsent` (`DELETE /vrp-consents/{id}`). Token.io
   relays the revocation to the bank and the status becomes `REVOKED` on success. Tell the payer
   only after the status confirms it — revocation is a bank round trip, not a local flag.

## Presence matters

The `customer-initiated` header declares whether the payer is present for a given VRP payment. It
is not cosmetic: it is how the bank distinguishes a payer-present charge from a sweeping or
unattended one, and it changes what the bank will permit. If it is absent, the customer is assumed
**not** present.

## Statuses

Consent statuses run to `AUTHORIZED` and `REVOKED`; payment statuses under a consent use the same
`INITIATION_*` vocabulary as a single payment, with the raw bank status in `bankVrpStatus`. See
`errors/token-io-decline-codes.yml`.

## Reversal

Revocation stops future payments. It does not reverse payments already made — those need
`InitiateRefund` (`POST /refunds`), and no time window is published for it.
