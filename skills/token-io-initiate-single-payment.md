---
name: token-io-initiate-single-payment
description: >-
  Initiate a single immediate account-to-account payment through Token.io, carry the payer through
  bank authentication, and resolve the payment to a final status. Use for Pay by Bank checkout on
  Payments v2.
api: Token.io's Open Banking API for TPPs
base_url: https://api.token.io
sandbox_url: https://api.sandbox.token.io
spec: openapi/token-io-payments-v2-api-openapi.yml
operations:
  - GetBanksv2
  - InitiatePayment
  - GetPayment
  - ProvideEmbeddedFields
  - GatewayService.SetWebhookConfig
generated: '2026-09-17'
method: generated
source: >-
  openapi/token-io-payments-v2-api-openapi.yml, openapi/token-io-banks-v2-api-openapi.yml,
  conventions/token-io-conventions.yml, errors/token-io-decline-codes.yml,
  sandbox/token-io-sandbox.yml
---

# Initiate a single immediate payment

A Token.io payment is not a charge you capture. It is an instruction the payer authorises at their
own bank, which means the flow is: pick the bank, create the payment, send the human to the bank,
then wait for a status you do not control.

## Before you start

- Authenticate with a detached JWT signed by a key enrolled against your member id. Set `exp` under
  ten minutes from now. HTTP Basic works only against `api.sandbox.token.io`.
- Send `token-customer-ip-address` and, when a human really did click the button,
  `customer-initiated: true`. Omitting them tells the bank this is TPP-initiated, which changes what
  the bank will allow.
- If you operate under Token.io's licence, `initiation.onBehalfOfId` / the sub-TPP id is mandatory
  (TB-1549). A payment without it is rejected.

## Steps

1. **Choose a bank the operation will actually work against.** `GetBanksv2` (`GET /v2/banks`)
   returns each bank with ~40 capability flags. Filter on the ones the flow needs — for example
   `supportsSendPayment`, `requiresOneStepPayment`, `supportsReturnRefundAccount` — rather than
   letting the payer pick a bank that will answer 501 (`UNIMPLEMENTED`, "not supported by the bank").
2. **Subscribe to status before you create anything.** `GatewayService.SetWebhookConfig`
   (`PUT /webhook/config`) with `type: ["PAYMENT_STATUS_CHANGED"]` and your URL. There is exactly
   one configuration per member and it is replaced, not merged, so read the existing one with
   `GatewayService.GetWebhookConfig` first and put back the union of the types you need.
3. **Create the payment.** `InitiatePayment` (`POST /v2/payments`) with the amount, currency,
   creditor, `localInstrument` and your own `refId`. The response carries the payment `id` (prefixed
   `pm2:`) and a status.
4. **Send the payer to the bank.** Use the returned authentication/redirect details, or the Hosted
   Pages surface — the modal, iframe or redirect described in
   `components/token-io-components.yml`. For embedded authentication, collect the bank's fields and
   post them back with `ProvideEmbeddedFields`
   (`POST /v2/payments/{paymentId}/embedded-auth`).
5. **Resolve the status.** Wait for `PAYMENT_STATUS_CHANGED`. If no webhook arrives, poll
   `GetPayment` (`GET /v2/payments/{paymentId}`) — do not resend the initiation.

## Reading the result

`status` is Token.io's view; `bankPaymentStatus` is the raw ISO 20022 code from the bank, passed
through unmapped. Both matter, and the mapping between them is bank-dependent.

- `INITIATION_COMPLETED` — accepted. Settlement of an instant payment lands within 30–45 minutes.
- `INITIATION_PROCESSING` — keep waiting; the bank has acknowledged it.
- `INITIATION_REJECTED_INSUFFICIENT_FUNDS` — payer-actionable. Offer another account.
- `INITIATION_DECLINED` — usually the payer cancelled or refused consent. Re-prompt; do not retry.
- `INITIATION_EXPIRED` — the bank never returned a final status (~30 minutes, or ~40 if the payer
  never completed the bank login). This is an unknown outcome, not a decline. Reconcile before
  charging again.

## The rule that matters most

**Token.io publishes no idempotency key.** There is no header and no documented de-duplication on
`POST /v2/payments`. A retry of a timed-out initiation is not protected against creating a second
payment. On any timeout, `DEADLINE_EXCEEDED` or 504, poll `GetPayment` or wait for the webhook —
never re-POST.

## Errors

Add `token-json-error: true` to get the JSON envelope
(`{error:{code,message,token_trace_id,error_origin}}`). On a 500, read the `token-external-error`
response header: `true` means the bank failed and a retry may help; absent means Token.io failed.
Keep the `tokenTraceId` from every response — it is what support will ask for. Full catalogue in
`errors/token-io-problem-types.yml`.

## Testing

Select the `mock-redirect` bank in sandbox and drive the outcome with the amount: `101` completes,
`108` gives insufficient funds, `104` and `112` decline, `105` stays processing. The full table is
in `sandbox/token-io-sandbox.yml`.

## Undoing it

There is no capture step to cancel after settlement. Before completion, `CancelPayment`
(`DELETE /v2/payments/{paymentId}`); after it, a refund is the only reversal —
`InitiateRefund` (`POST /refunds`), bounded by the original amount. **Token.io states no time
window for either.** Do not tell a user a refund deadline the docs do not give.
