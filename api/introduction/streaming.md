---
title: Streaming
order: 30
---

# streaming

import { MethodTable } from "components/MethodTable";

Horizon provides a streaming mechanism for receiving events in near real time. Instead of repeatedly sending requests to Horizon for batch updates, a connection is established between a client and Horizon with updates to an endpoint response streaming as new ledgers close and updates occur.

This reduces requests that return no data and allows near instantaneous updates client-side.

All attributes for the endpoints that allow streaming are the same as regular responses. A caller can initiate streaming by setting ‘Accept: text/event-stream’ in the HTTP header when making the request. Study an example of using streaming in the [Follow Received Payments tutorial](../../tutorials/follow-received-payments.md).

 

Endpoints with Streaming

| [Ledgers](https://developers.stellar.org/api/resources/ledgers/) |
| :--- |
| [Transactions](https://developers.stellar.org/api/resources/transactions/) |
| [Operations](https://developers.stellar.org/api/resources/operations/) |
| [Payments](https://developers.stellar.org/api/resources/operations/object/payment/) |
| [Effects](https://developers.stellar.org/api/resources/effects/) |
| [Accounts](https://developers.stellar.org/api/resources/accounts/) |
| [Offers](https://developers.stellar.org/api/resources/offers/) |
| [Trades](https://developers.stellar.org/api/resources/trades/) |
| [Order Books](https://developers.stellar.org/api/aggregations/order-books/) |

