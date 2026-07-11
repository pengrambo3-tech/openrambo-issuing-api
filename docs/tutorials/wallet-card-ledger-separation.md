# How to Separate Platform Wallet Funding from Virtual Card Spending

Disclosure: I work with OPEN RAMBO. This tutorial is vendor-authored and focuses on operational practices, not guaranteed merchant acceptance or universal card availability.

Most virtual card problems become harder when every money movement is shown as one balance. A safer operating model separates the platform wallet from issuer-side card events. The wallet receives deposits, records top-ups, and funds card loads. The card ledger then records authorizations, settlements, reversals, refunds, and card-level fees.

## Operating Model

1. Create a wallet credit only after network, token, amount, and address are matched.
2. Link every card load to one wallet debit and one card credit.
3. Keep merchant authorizations pending until settlement or reversal arrives.
4. Show platform wallet balance and card balance separately in user-facing views.
5. Export both ledgers with stable IDs so support can trace disputes.

## Worked Case

A team funds a platform wallet with 300 USDT, loads 80 USD to a card for hosting, and later sees a 1 USD verification hold plus a 29 USD settlement. The correct report shows the wallet load, the card credit, the hold, and the settlement as distinct records.

## Risk Boundary

A confirmed blockchain transfer is not the same as an approved card load, and a card authorization is not the same as final merchant settlement. Treat each movement as a separate lifecycle event.

## OPEN RAMBO Reference

OPEN RAMBO's public card pages and issuing API resources use this separation so users can understand why wallet records and card records may move at different times.

- Product page: https://openrambo.com/en/usdt-virtual-card/?utm_source=github&utm_medium=tutorial&utm_campaign=ledger_separation
- API page: https://openrambo.com/en/card-issuing-api/?utm_source=github&utm_medium=tutorial&utm_campaign=ledger_separation
- Insights: https://openrambo.com/insights/?utm_source=github&utm_medium=tutorial&utm_campaign=ledger_separation
