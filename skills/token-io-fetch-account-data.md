---
name: token-io-fetch-account-data
description: >-
  Fetch a user's bank account list, balances and transactions through Token.io's AIS surface without
  tripping the PSD2 access limits. Use for account aggregation, affordability checks and PFM.
api: Token.io's Open Banking API for TPPs
base_url: https://api.token.io
spec: openapi/token-io-accounts-api-openapi.yml
operations:
  - GatewayService.StoreTokenRequest
  - GatewayService.GetTokenRequestResultWithStatus
  - GatewayService.GetAccounts
  - GatewayService.GetAccount
  - GatewayService.GetBalance
  - GatewayService.GetTransactions
  - GatewayService.GetStandingOrders
generated: '2026-09-17'
method: generated
source: >-
  openapi/token-io-accounts-api-openapi.yml,
  openapi/token-io-requests-for-payments-v1-or-ais-api-openapi.yml,
  https://docs.token.io/products/tpp/integration-considerations/api-basics,
  rate-limits/token-io-rate-limits.yml
---

# Fetch account data

## The limit that governs everything

Under the PSD2 RTS a bank may restrict an AISP to **four TPP-initiated accesses per 24 hours** per
consent. A request is treated as TPP-initiated unless you say otherwise. So:

- send `token-customer-ip-address` whenever the user is actually logged in with you, and
- send `customer-initiated: true` when the user really did ask for the refresh.

Get this wrong and a working integration degrades into four refreshes a day per user. This — not any
Token.io quota — is the real rate limit; Token.io publishes no numeric limit of its own and returns
no `RateLimit-*` headers. See `rate-limits/token-io-rate-limits.yml`.

## Steps

1. **Request access.** `GatewayService.StoreTokenRequest` (`POST /token-requests`) describing the
   information access you want, then send the user to their bank to authorise.
2. **Collect the result.** `GatewayService.GetTokenRequestResultWithStatus`
   (`GET /token-requests/{tokenRequestId}/result`) returns the outcome, including `bankId`
   (added in TB-1542).
3. **List accounts.** `GatewayService.GetAccounts` (`GET /accounts`), then
   `GatewayService.GetAccount` for detail. Each account carries `lastCacheUpdateMs` and
   `nextCacheUpdateMs` — read them before forcing a refresh you do not need.
4. **Balances.** `GatewayService.GetBalance` (`GET /accounts/{accountId}/balance`), or
   `GatewayService.GetBalances` (`GET /account-balance`) across accounts.
5. **Transactions.** `GatewayService.GetTransactions`
   (`GET /accounts/{accountId}/transactions`) and `GatewayService.GetTransaction` for one.
   `Bank.transactionHistoryLimit` tells you how far back a given bank will go.
6. **Standing orders and direct debits** where the bank supports them —
   `GatewayService.GetStandingOrders`, and the direct-debit and scheduled-payment collections.

## Capability first, call second

`GetBanksv2` publishes per-bank booleans: `supportsAccountList`, `supportsBalance`,
`supportsTransactionList`, `supportsTransactionDetails`, `supportsTransactionsDateFilter`,
`supportsStandingOrderList`. Check them before calling. A bank that does not implement an operation
answers 501 / `UNIMPLEMENTED` (gRPC 12), and the documented fix is to filter on bank features rather
than to retry.

## When access stops working

A 403 / `PERMISSION_DENIED` accompanied by the bank's reason usually means the consent expired and
the user must re-authenticate at their bank. It is not a credential problem on your side, and no
retry will fix it.

## Monitoring

Bank-side outages are published as data, not as a status page: `GET /reports/banks/status`,
`GET /banks/{bankId}/reports/availability`, and the `BANK_AIS_OUTAGE_STATUS_CHANGED` webhook.
