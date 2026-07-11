# OPEN RAMBO Issuing API

Official integration resources for platforms that need virtual-card product discovery, issuance, funding, card controls, and issuer-side transaction records.

## Resources

- [Issuing API overview](https://openrambo.com/issuing-api?utm_source=github&utm_medium=repository&utm_campaign=issuing_api)
- [OpenAPI 3.1 specification](https://openrambo.com/developers/openapi.yaml?utm_source=github&utm_medium=repository&utm_campaign=issuing_api)
- [Postman collection](https://openrambo.com/developers/openrambo-issuing.postman_collection.json?utm_source=github&utm_medium=repository&utm_campaign=issuing_api)
- [API launch-readiness guide](https://openrambo.com/insights/api-launch-readiness-for-api-platforms/?utm_source=github&utm_medium=repository&utm_campaign=issuing_api)
- [Demo / pitch video](media/openrambo-demo-pitch-2026-07-11.mp4)

## Tutorials

- [How to separate platform wallet funding from virtual card spending](docs/tutorials/wallet-card-ledger-separation.md)
- [Building an issuing API flow with idempotency and webhook safety](docs/tutorials/issuing-api-idempotency-webhooks.md)
- [Why advertising teams should use one controlled card per ad account](docs/tutorials/advertising-card-budget-controls.md)
- [Virtual card fee analysis: what to price before launch](docs/tutorials/virtual-card-fee-analysis.md)
- [Reconciliation basics for authorizations, settlements, and refunds](docs/tutorials/card-authorization-settlement-refund-reconciliation.md)
- [USDT funding workflow for a card platform](docs/tutorials/usdt-funding-workflow.md)
- [Choosing a virtual card provider for SaaS subscriptions](docs/tutorials/virtual-card-provider-for-saas-subscriptions.md)
- [Designing a card dashboard that builds user trust](docs/tutorials/card-user-dashboard-trust.md)
- [How to expose card issuing as an API without confusing users](docs/tutorials/card-issuing-api-without-user-confusion.md)

## Base URL

```text
https://openrambo.com/api/issuing/v1
```

Authenticate with a scoped `X-API-Key`. Mutating requests also require a unique `Idempotency-Key` of no more than 120 characters.

## Quick start

```bash
curl https://openrambo.com/api/issuing/v1/products \
  -H "X-API-Key: YOUR_API_KEY"
```

Create a card only after selecting a currently available product returned by `GET /products`:

```bash
curl -X POST https://openrambo.com/api/issuing/v1/cards \
  -H "X-API-Key: YOUR_API_KEY" \
  -H "Idempotency-Key: create-card-UNIQUE_ID" \
  -H "Content-Type: application/json" \
  -d '{"productId":"PRODUCT_ID","firstRechargeAmount":10}'
```

## Operational boundaries

- Product availability, opening fees, and minimum funding are returned by the live product catalog.
- Merchant acceptance is not guaranteed and remains subject to program, geography, merchant, and risk controls.
- Platform-wallet entries and issuer-side card transactions are separate ledgers.
- Do not log complete card credentials, API keys, or sensitive cardholder data.
- Retry only documented transient failures and reuse the same idempotency key for the same operation.

## Access

Partner access is provisioned after business and integration review. Contact [pengrambo3@gmail.com](mailto:pengrambo3@gmail.com) or use the support channels on [OPEN RAMBO](https://openrambo.com/?utm_source=github&utm_medium=repository&utm_campaign=issuing_api).
