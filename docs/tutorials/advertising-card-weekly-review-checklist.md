# Advertising Card Weekly Review Checklist: Owners, Holds, Refunds, and Limits

Disclosure: I work with OPEN RAMBO. This tutorial is vendor-authored and focuses on operational practices, not guaranteed merchant acceptance or universal card availability.

Advertising cards become harder to manage when the team waits for a month-end surprise instead of reviewing the account every week. A short weekly review can catch stale active cards, orphaned owners, unexplained holds, silent limit drift, and refunds that no longer map back to the original campaign.

## What to review every week

1. List every active advertising card, its owner, the related client or campaign, and the current card status.
2. Compare the approved weekly budget window with the actually loaded balance on each card.
3. Separate pending verification holds from settled ad charges before calculating spend.
4. Check whether any limit changed during the week and record who changed it and why.
5. Match refunds and reversals back to the original settled transaction instead of treating them as new wallet funding.
6. Flag cards with no clear owner, no recent activity, or a billing profile that is no longer in use.

## Evidence that should exist

Every review should be able to answer these questions without guesswork:

- Which ad account or billing profile uses this card?
- Who is the current owner?
- What was the approved funding window?
- Which transactions are still pending?
- Which refunds are still unresolved?
- Did anyone raise the ceiling or top up the card outside the normal plan?

If those answers only exist in chat screenshots or memory, the review process is too weak.

## Worked example

An agency runs cards for three clients. One client card shows a USD 1 verification hold, a USD 247 settled threshold charge, and a USD 50 top-up that was made midweek after a failed payment. The weekly review should confirm whether the top-up was planned, whether the failed payment was caused by an actual balance gap or by a pending hold, and whether the current owner still manages that billing profile.

The correct outcome is not merely “the campaign kept running.” The correct outcome is that finance, ad ops, and support can all reconstruct the same sequence of events from the ledger.

## Weekly review output

A useful export or checklist should include:

- Active cards and owners
- Current loaded balance
- Pending holds
- Settled charges
- Refunds and reversals
- Limit changes
- Cards recommended for freeze or closure

This turns card review into a repeatable operating ritual instead of a reaction to the loudest client or the latest decline.

## Risk boundary

Weekly review does not guarantee merchant acceptance or prevent every failed payment. Its purpose is to reduce confusion, detect control drift early, and stop a small reconciliation issue from turning into a larger client dispute.

## OPEN RAMBO Reference

OPEN RAMBO keeps platform-wallet records and issuer-side card activity separate so teams can review funding, charges, and exceptions without flattening them into one number.

- Advertising card page: https://openrambo.com/en/virtual-card-for-advertising/?utm_source=github&utm_medium=tutorial&utm_campaign=advertising_weekly_review
- Advertising operations guide: https://openrambo.com/insights/card-operations-for-advertising/?utm_source=github&utm_medium=tutorial&utm_campaign=advertising_weekly_review
