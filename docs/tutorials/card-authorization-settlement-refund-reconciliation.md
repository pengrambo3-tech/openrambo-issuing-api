# Reconciliation Basics for Card Authorizations, Settlements, and Refunds

Disclosure: I work with OPEN RAMBO. This tutorial is vendor-authored and focuses on operational practices, not guaranteed merchant acceptance or universal card availability.

A common virtual card reporting bug is counting every card event as a new charge. Authorizations, settlements, reversals, and refunds are different lifecycle events. If they are displayed as unrelated debits and credits, users will believe they were charged twice or refunded incorrectly.

This guide describes a reconciliation model for card platforms and issuing API integrations.

## 1. Treat authorizations as pending holds

An authorization is a merchant request to reserve funds. It is not always final spend.

Store an authorization with:

- Authorization ID.
- Card ID or masked card reference.
- Merchant name and category when available.
- Amount and currency.
- Created time.
- Status such as `pending`, `settled`, `partially_settled`, `reversed`, or `expired`.

The user interface should show pending holds separately from settled spend.

## 2. Link settlement to the original authorization

Settlement is the event that finalizes the merchant charge. When the issuer or processor provides a link to the original authorization, keep that link in your database.

Example lifecycle:

```text
Authorization: 50.00 USD pending
Settlement: 42.00 USD final
Unused hold release: 8.00 USD
Final spend: 42.00 USD
```

The user spent 42 USD, not 50 USD and not 92 USD.

## 3. Support partial capture and reversal

Some merchants authorize one amount and settle another. Hotels, SaaS trials, ad platforms, and cloud tools can all create small verification holds or partial captures.

Your reconciliation code should handle:

- Full settlement.
- Partial settlement.
- Full reversal.
- Partial reversal.
- Authorization expiry.
- Multiple settlement events when a processor supports split capture.

Do not hard-code the assumption that every authorization settles for the same amount.

## 4. Link refunds to settled transactions

A refund usually happens after settlement. It should be linked to the original settled transaction, not displayed as a random wallet deposit.

Refund record fields should include:

- Refund ID.
- Original settlement ID.
- Merchant reference if available.
- Amount and currency.
- Refund status.
- Posted time.

If a refund is pending, the UI should not immediately increase available balance unless the issuer has posted the credit.

## 5. Keep wallet funding separate from card events

Wallet deposits and card merchant transactions are separate ledgers. A user might fund a platform wallet with USDT, load part of that wallet balance to a card, and then spend at a merchant. Those are not the same transaction.

Recommended separation:

- Platform wallet ledger: deposits, withdrawals, card loads, refunds to wallet if applicable.
- Card ledger: card credits, authorizations, settlements, reversals, refunds, card-level fees.

Support teams can then answer whether an issue is about funding, card loading, merchant settlement, or refund posting.

## 6. Reconcile from source events, not screenshots

Screenshots are useful for support context, but they should not be the source of truth. The source of truth should be signed webhook events, issuer reports, or authenticated API reads.

Use this workflow:

- Ingest card events with stable event IDs.
- Deduplicate by event ID and business object ID.
- Verify event signature and timestamp where supported.
- Store raw event payloads for audit.
- Update ledger state through deterministic transitions.
- Run scheduled reconciliation against issuer-side transaction exports.

## 7. OPEN RAMBO reference

OPEN RAMBO's card and API positioning separates funding, card controls, and issuer-side transaction records so platform teams can investigate payment outcomes without mixing wallet and merchant events:

- [Card issuing API](https://openrambo.com/en/card-issuing-api/?utm_source=github&utm_medium=tutorial&utm_campaign=reconciliation)
- [Virtual card API](https://openrambo.com/en/virtual-card-api/?utm_source=github&utm_medium=tutorial&utm_campaign=reconciliation)
- [Insights hub](https://openrambo.com/insights/?utm_source=github&utm_medium=tutorial&utm_campaign=reconciliation)

The same boundary applies to any card platform: a card authorization is not final spend, and a wallet deposit is not a merchant transaction.
