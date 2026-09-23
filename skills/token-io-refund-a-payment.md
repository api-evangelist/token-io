---
name: token-io-refund-a-payment
description: >-
  Return money for a completed Token.io payment — full or partial — and follow the refund to a final
  status. Use when a consumer returns goods or a merchant needs to reverse a settled A2A payment.
api: Token.io's Open Banking API for TPPs
base_url: https://api.token.io
spec: openapi/token-io-refunds-api-openapi.yml
operations:
  - InitiateRefund
  - GetRefund
  - GetRefunds
  - GetTransferRefunds
generated: '2026-09-17'
method: generated
source: >-
  openapi/token-io-refunds-api-openapi.yml,
  https://docs.token.io/products/tpp/settlement-accounts/refunds,
  errors/token-io-decline-codes.yml, conventions/token-io-conventions.yml
---

# Refund a Token.io payment

An A2A refund is a fresh payment in the opposite direction, funded from a settlement account. It is
not a card reversal, so nothing is "voided" — money moves again.

## Before you start

- The original payment must be identifiable: you need its `id`.
- Refunds are funded from a settlement account. If you do not pass payer details, Token.io retrieves
  them from the original payment.
- If you are an unregulated TPP operating under Token.io's licence, `initiation.onBehalfOfId` is
  **always** required on the refund request.

## Steps

1. **Initiate.** `InitiateRefund` (`POST /refunds`) with the original payment `id`, the `amount`,
   a `description`, and optionally `accountId` for the settlement account to debit.
2. **Read the initial status.** `INITIATION_PENDING` means Token.io accepted and validated it.
   `INITIATION_PROCESSING` means the bank has it.
3. **Follow it to a final status.** Subscribe to `REFUND_STATUS_CHANGED` (one webhook configuration
   per member — see `asyncapi/token-io-webhooks.yml`). If webhooks are not configured or not
   arriving, poll `GetRefund` (`GET /refunds/{id}`); the docs recommend every 120 minutes while the
   refund is `INITIATION_PROCESSING`.
4. **Reconcile.** `GetRefunds` (`GET /refunds`) lists refunds; `GetTransferRefunds`
   (`GET /transfers/{id}/refunds`) lists them for a Payments v1 transfer.

## Rules Token.io enforces for you

- **Partial refunds are supported**, and Token.io will not let the cumulative refunded amount exceed
  the original payment. You do not have to track the remaining balance yourself, but you should
  expect a rejection if you try to exceed it.
- **When your own account is the settlement account**, put the merchant name in the `refId`
  remittance reference so the payer can recognise the credit on their statement.

## What the docs do not say

No refund deadline is published. There is no "within N days" rule anywhere in the refunds
documentation, and none should be asserted to a user. If a refund window matters commercially,
it is a contract question, not an API one.

## Final statuses

`INITIATION_COMPLETED` is success. `INITIATION_REJECTED` came back from the bank.
`INITIATION_FAILED` includes the case where the status polling period was exhausted — treat that as
unknown and reconcile, not as a confirmed failure.

## Idempotency

There is none. `POST /refunds` has no idempotency key. On a timeout, poll `GetRefunds` filtered to
the original payment before resending — a blind retry can issue a second refund.
