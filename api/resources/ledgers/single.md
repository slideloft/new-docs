---
title: Retrieve a Ledger
order: 20
---

# Single

The single ledger endpoint provides information on a specific ledger.



* sequencerequired

  The sequence number of a specific ledger.

* cursoroptional

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* orderoptional

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limitoptional

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

* include\_failedoptional

  Set to true to include failed transactions in results. Options include `true` and `false`.



{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .ledgers()
  .ledger("69858")
  .call()
  .then(function (resp) {
    console.log(resp);
  })
  .catch(function (err) {
    console.error(err);
  });
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl "https://expansion-testnet.bantu.network/ledgers/69859"
```
{% endtab %}
{% endtabs %}

```bash
"_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27146933"
    },
    "transactions": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27146933/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27146933/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27146933/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27146933/effects{?cursor,limit,order}",
      "templated": true
    }
  },
  "id": "e1218a337cecda05526fba902c61d3d7130baa58d8db41f544bf563f779b6329",
  "paging_token": "116595189421703168",
  "hash": "e1218a337cecda05526fba902c61d3d7130baa58d8db41f544bf563f779b6329",
  "prev_hash": "9eac16fecd885147067b58b7684f60d216f931b813f651265bbc97de4cea313d",
  "sequence": 27146933,
  "successful_transaction_count": 26,
  "failed_transaction_count": 9,
  "operation_count": 67,
  "closed_at": "2019-12-06T22:39:32Z",
  "total_coins": "105443902087.3472865",
  "fee_pool": "1807264.7509661",
  "base_fee_in_stroops": 100,
  "base_reserve_in_stroops": 5000000,
  "max_tx_set_size": 1000,
  "protocol_version": 12,
  "header_xdr": "AAAADJ6sFv7NiFFHBntYt2hPYNIW+TG4E/ZRJlu8l95M6jE9bsvzId+Gtul2mNMW4UZQ+KqSb/nbN8F1CTxAfQsyUy8AAAAAXerYpAAAAAAAAAAAXQNpS8daKGZUeY5quYUcIiJZBMB7LiLsZJsEx9qw79fx99Bu/lk+sIePNUNcuOC2euthzfhLuWJ1nZBuoQFDjgGeOrUOoh6z7HlbYQAAEG/dvCadAAABFgAAAAAIOwAqAAAAZABMS0AAAAPooSNtHXJNJKKWlBtgkAM1LBxzlzYjIlS0xwpjP+uCi76fQj59wgTy0+xtx7O1qTb+W6zcI2zWZnrUU/8v8RZHFBfoo20QYKh95+wWr348yZAexZpdrjhyCxbChxlVTZOX6nZfIgcYBMnZRkOTCLdPO76yeqpDhqu9KrPe3YPTO3wAAAAA"
}
```

