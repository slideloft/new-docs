---
title: List Strict Receive Payment Paths
order: 20
---

# Strict Receive

The strict receive payment path endpoint lists the paths a payment can take based on the amount of an asset you want the recipient to receive. The destination asset amount stays constant, and the type and amount of an asset sent vary based on offers in the order books.

For this search, Horizon loads a list of assets available to the sender \(based on `source_account` or `source_assets`\) and displays the possible paths from the different source assets to the destination asset. Only paths that satisfy the `destination_amount` are returned.

 - ARGUMENT - 

* source\_account `optional`

  The Stellar address of the sender. Any returned path must start with an asset that the sender holds. Using either `source_account` or `source_assets` as an argument is required for strict receive path payments.

* source\_assets `optional`

  A comma-separated list of assets available to the sender. Any returned path must start with an asset in this list. Each asset is formatted as `CODE:ISSUER_ACCOUNT`. For example: `USD:GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX`. Using either `source_account` or `source_assets` as an argument is required for strict receive path payments.

* destination\_asset\_type `required`

  The type for the destination asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* destination\_asset\_issuer `optional`

  The Stellar address of the issuer of the destination asset. Required if the `destination_asset_type` is not `native`.

* destination\_asset\_code `optional`

  The code for the destination asset. Required if the `destination_asset_type` is not `native`.

* destination\_amount `required`

  The amount of the destination asset that should be received.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .strictReceivePaths(
    [
      new StellarSdk.Asset(
        "CNY",
        "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
      ),
    ],
    new StellarSdk.Asset(
      "BB1",
      "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
    ),
    "5",
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
curl "https://expansion-testnet.bantu.network/paths/strict-receive?source_assets=CNY:GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX&destination_asset_type=credit_alphanum4&destination_asset_code=BB1&destination_asset_issuer=GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN&destination_amount=5"
```
{% endtab %}
{% endtabs %}

{% code title="Example Response" %}
```bash
{
  "_embedded": {
    "records": [
      {
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "CNY",
        "source_asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "source_amount": "28.9871131",
        "destination_asset_type": "credit_alphanum4",
        "destination_asset_code": "BB1",
        "destination_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
        "destination_amount": "5.0000000",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "XCN",
            "asset_issuer": "GCNY5OXYSY4FKHOPT2SPOQZAOEIGXB5LBYW3HVU3OWSTQITS65M5RCNY"
          },
          {
            "asset_type": "native"
          }
        ]
      },
      {
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "CNY",
        "source_asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "source_amount": "29.0722784",
        "destination_asset_type": "credit_alphanum4",
        "destination_asset_code": "BB1",
        "destination_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
        "destination_amount": "5.0000000",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "ULT",
            "asset_issuer": "GC76RMFNNXBFDSJRBXCABWLHXDK4ITVQSMI56DC2ZJVC3YOLLPCKKULT"
          },
          {
            "asset_type": "native"
          }
        ]
      },
      {
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "CNY",
        "source_asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "source_amount": "29.4000002",
        "destination_asset_type": "credit_alphanum4",
        "destination_asset_code": "BB1",
        "destination_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
        "destination_amount": "5.0000000",
        "path": [
          {
            "asset_type": "native"
          }
        ]
      },
      {
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "CNY",
        "source_asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "source_amount": "31.8955888",
        "destination_asset_type": "credit_alphanum4",
        "destination_asset_code": "BB1",
        "destination_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
        "destination_amount": "5.0000000",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "USD",
            "asset_issuer": "GBUYUAI75XXWDZEKLY66CFYKQPET5JR4EENXZBUZ3YXZ7DS56Z4OKOFU"
          },
          {
            "asset_type": "native"
          }
        ]
      },
      {
        "source_asset_type": "credit_alphanum4",
        "source_asset_code": "CNY",
        "source_asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "source_amount": "34.7086084",
        "destination_asset_type": "credit_alphanum4",
        "destination_asset_code": "BB1",
        "destination_asset_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
        "destination_amount": "5.0000000",
        "path": [
          {
            "asset_type": "credit_alphanum4",
            "asset_code": "USD",
            "asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
          },
          {
            "asset_type": "native"
          }
        ]
      }
    ]
  }
}
```
{% endcode %}

{% code title="JavaScript Streaming Example" %}
```bash
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var callback = function (resp) {
  console.log(resp);
};

var es = server
  .strictReceivePaths(
    [
      new StellarSdk.Asset(
        "CNY",
        "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
      ),
    ],
    new StellarSdk.Asset(
      "BB1",
      "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN",
    ),
    "5",
  )
  .cursor("now")
  .stream({ onmessage: callback });
```
{% endcode %}

