---
title: Retrieve a Transaction's Operations
order: 30
---

# Operations

This endpoint returns successful operations for a specific transaction.

 ARGUMENTS

* transaction\_hashrequired

  A hex-encoded SHA-256 hash of this transaction’s XDR-encoded form.

* cursoroptional

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* orderoptional

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limitoptional

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

* include\_failedoptional

  Set to true to include failed operations in results. Options include `true` and `false`.

* joinoptional

  Set to `transactions` to include the transactions which created each of the operations in the response

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .operations()
  .forTransaction(
    "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
  )
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
curl "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=\u0026limit=10\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=120133379185221636\u0026limit=10\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a/operations?cursor=120133379185221633\u0026limit=10\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221633"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221633/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120133379185221633"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120133379185221633"
          }
        },
        "id": "120133379185221633",
        "paging_token": "120133379185221633",
        "transaction_successful": true,
        "source_account": "GDJX67SFY2N73H72TWMKKBQP5UPBNKBNUMNE2IGFKNES43S4327X6DHG",
        "type": "manage_buy_offer",
        "type_i": 12,
        "created_at": "2020-01-28T21:14:59Z",
        "transaction_hash": "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
        "amount": "0.0000000",
        "price": "0.0001000",
        "price_r": {
          "n": 1,
          "d": 10000
        },
        "buying_asset_type": "native",
        "selling_asset_type": "credit_alphanum4",
        "selling_asset_code": "ETH",
        "selling_asset_issuer": "GBDEVU63Y6NTHJQQZIKVTC23NWLQVP3WJ2RI2OTSJTNYOIGICST6DUXR",
        "offer_id": 149983118
      },
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221634"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221634/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120133379185221634"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120133379185221634"
          }
        },
        "id": "120133379185221634",
        "paging_token": "120133379185221634",
        "transaction_successful": true,
        "source_account": "GDJX67SFY2N73H72TWMKKBQP5UPBNKBNUMNE2IGFKNES43S4327X6DHG",
        "type": "manage_buy_offer",
        "type_i": 12,
        "created_at": "2020-01-28T21:14:59Z",
        "transaction_hash": "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
        "amount": "0.0000000",
        "price": "0.0001000",
        "price_r": {
          "n": 1,
          "d": 10000
        },
        "buying_asset_type": "native",
        "selling_asset_type": "credit_alphanum4",
        "selling_asset_code": "ETH",
        "selling_asset_issuer": "GBDEVU63Y6NTHJQQZIKVTC23NWLQVP3WJ2RI2OTSJTNYOIGICST6DUXR",
        "offer_id": 149983119
      },
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221635"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221635/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120133379185221635"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120133379185221635"
          }
        },
        "id": "120133379185221635",
        "paging_token": "120133379185221635",
        "transaction_successful": true,
        "source_account": "GDJX67SFY2N73H72TWMKKBQP5UPBNKBNUMNE2IGFKNES43S4327X6DHG",
        "type": "manage_offer",
        "type_i": 3,
        "created_at": "2020-01-28T21:14:59Z",
        "transaction_hash": "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
        "amount": "98.5005752",
        "price": "0.0003494",
        "price_r": {
          "n": 17471,
          "d": 50000000
        },
        "buying_asset_type": "credit_alphanum4",
        "buying_asset_code": "ETH",
        "buying_asset_issuer": "GBDEVU63Y6NTHJQQZIKVTC23NWLQVP3WJ2RI2OTSJTNYOIGICST6DUXR",
        "selling_asset_type": "native",
        "offer_id": 0
      },
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221636"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/120133379185221636/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120133379185221636"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120133379185221636"
          }
        },
        "id": "120133379185221636",
        "paging_token": "120133379185221636",
        "transaction_successful": true,
        "source_account": "GDJX67SFY2N73H72TWMKKBQP5UPBNKBNUMNE2IGFKNES43S4327X6DHG",
        "type": "manage_buy_offer",
        "type_i": 12,
        "created_at": "2020-01-28T21:14:59Z",
        "transaction_hash": "6b983a4e0dc3c04f4bd6b9037c55f70a09c434dfd01492be1077cf7ea68c2e4a",
        "amount": "291.8057980",
        "price": "0.0002565",
        "price_r": {
          "n": 250039,
          "d": 975000000
        },
        "buying_asset_type": "native",
        "selling_asset_type": "credit_alphanum4",
        "selling_asset_code": "ETH",
        "selling_asset_issuer": "GBDEVU63Y6NTHJQQZIKVTC23NWLQVP3WJ2RI2OTSJTNYOIGICST6DUXR",
        "offer_id": 0
      }
    ]
  }
}
```

