---
title: Retrieve an Account's Offers
order: 70
---

# Offers

This endpoint represents all offers a given account has currently open and can be used in streaming mode.

Streaming mode allows you to listen for new offers for this account as they are added to the Stellar ledger. If called in streaming mode, Horizon will start at the earliest known offer unless a `cursor` is set, in which case it will start from that `cursor`. By setting the `cursor` value to `now`, you can stream offers created since your request time.

 - ARGUMENT - 

* account\_id `required`

  This account’s public key encoded in a base32 string representation.

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
  .offers()
  .forAccount("GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K")
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
curl "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=\u0026limit=10\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164943216\u0026limit=10\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164555927\u0026limit=10\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/offers/164555927"
          },
          "offer_maker": {
            "href": "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
          }
        },
        "id": 164555927,
        "paging_token": "164555927",
        "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K",
        "selling": {
          "asset_type": "native"
        },
        "buying": {
          "asset_type": "credit_alphanum4",
          "asset_code": "BB1",
          "asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN"
        },
        "amount": "214.9999939",
        "price_r": {
          "n": 10000000,
          "d": 86000001
        },
        "price": "0.1162791",
        "last_modified_ledger": 28383147,
        "last_modified_time": "2020-02-24T22:58:38Z"
      },
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/offers/164943216"
          },
          "offer_maker": {
            "href": "https://expansion-testnet.bantu.network/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"
          }
        },
        "id": 164943216,
        "paging_token": "164943216",
        "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K",
        "selling": {
          "asset_type": "credit_alphanum4",
          "asset_code": "BB1",
          "asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN"
        },
        "buying": {
          "asset_type": "native"
        },
        "amount": "24.9999990",
        "price_r": {
          "n": 32224991,
          "d": 2500000
        },
        "price": "12.8899964",
        "last_modified_ledger": 28394149,
        "last_modified_time": "2020-02-25T15:49:57Z"
      }
    ]
  }
}
```

```bash
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var callback = function (resp) {
  console.log(resp);
};

var es = server
  .offers()
  .forAccount("GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K")
  .cursor("now")
  .stream({ onmessage: callback });
```

