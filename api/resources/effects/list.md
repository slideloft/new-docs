---
title: List All Effects
order: 20
---

# List

This endpoint lists all effects and can be used in [streaming](../../introduction/streaming.md) mode. Streaming mode allows you to listen for new effects as they are added to the Stellar ledger. If called in streaming mode, Horizon will start at the earliest known effect unless a `cursor` is set, in which case it will start from that `cursor`. By setting the cursor value to `now`, you can stream effects created since your request time.

 - ARGUMENT - 

* cursor `optional`

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* order `optional`

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limit `optional`

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .effects()
  .call()
  .then(function (effectResults) {
    //page 1
    console.log(effectResults.records);
  })
  .catch(function (err) {
    console.log(err);
  });
```
{% endtab %}

{% tab title="cURL" %}
```javascript
curl "https://expansion-testnet.bantu.network/effects"
```
{% endtab %}
{% endtabs %}

```javascript
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/effects?cursor=\u0026limit=3\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/effects?cursor=12884905985-3\u0026limit=3\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/effects?cursor=12884905985-1\u0026limit=3\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/12884905985"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=12884905985-1"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=12884905985-1"
          }
        },
        "id": "0000000012884905985-0000000001",
        "paging_token": "12884905985-1",
        "account": "GALPCCZN4YXA3YMJHKL6CVIECKPLJJCTVMSNYWBTKJW4K5HQLYLDMZTB",
        "type": "account_created",
        "type_i": 0,
        "created_at": "2015-09-30T17:15:54Z",
        "starting_balance": "20.0000000"
      },
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/12884905985"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=12884905985-2"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=12884905985-2"
          }
        },
        "id": "0000000012884905985-0000000002",
        "paging_token": "12884905985-2",
        "account": "GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN7",
        "type": "account_debited",
        "type_i": 3,
        "created_at": "2015-09-30T17:15:54Z",
        "asset_type": "native",
        "amount": "20.0000000"
      },
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/12884905985"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=12884905985-3"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=12884905985-3"
          }
        },
        "id": "0000000012884905985-0000000003",
        "paging_token": "12884905985-3",
        "account": "GALPCCZN4YXA3YMJHKL6CVIECKPLJJCTVMSNYWBTKJW4K5HQLYLDMZTB",
        "type": "signer_created",
        "type_i": 10,
        "created_at": "2015-09-30T17:15:54Z",
        "weight": 1,
        "public_key": "GALPCCZN4YXA3YMJHKL6CVIECKPLJJCTVMSNYWBTKJW4K5HQLYLDMZTB",
        "key": ""
      }
    ]
  }
}
```

```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://horizon-testnet.stellar.org");

var effectHandler = function (effectResponse) {
  console.log(effectResponse);
};

var es = server.effects().cursor("now").stream({
  onmessage: effectHandler,
});
```

