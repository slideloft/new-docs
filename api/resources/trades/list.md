---
title: List All Trades
order: 20
---

# List

This endpoint lists all trades and can be used in [streaming](../../introduction/streaming.md) mode.

Streaming mode allows you to listen for new trades as they are added to the Stellar ledger. If called in streaming mode, Horizon will start at the earliest known trade unless a `cursor` is set, in which case it will start from that `cursor`. By setting the cursor value to `now`, you can stream trades created since your request time.

When filtering for a specific orderbook, you must use use all six of these arguments: `base_asset_type`, `base_asset_issuer`, `base_asset_code`, `counter_asset_type`, `counter_asset_issuer`, and `counter_asset_code`. If the base or counter asset is XLM, you only need to indicate the asset type as `native` and do not need to designate the code or the issuer.

 - ARGUMENT - 

* offer\_id `optional`

  The offer ID. Used to filter for trades originating from a specific offer.

* base\_asset\_type `optional`

  The type for the base asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* base\_asset\_issuer `optional`

  The Stellar address of the base asset’s issuer.

* base\_asset\_code `optional`

  The code for the base asset.

* counter\_asset\_type `optional`

  The type for the counter asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* counter\_asset\_issuer `optional`

  The Stellar address of the counter asset’s issuer.

* counter\_asset\_code `optional`

  The code for the counter asset.

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
  .trades()
  .forAssetPair(
    new StellarSdk.Asset(
      "USD",
      "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX",
    ),
    new StellarSdk.Asset.native(),
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
curl "https://expansion-testnet.bantu.network/trades?base_asset_type=credit_alphanum4&base_asset_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX&base_asset_code=USD&counter_asset_type=native&limit=3"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/trades?base_asset_code=USD\u0026base_asset_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026base_asset_type=credit_alphanum4\u0026counter_asset_type=native\u0026cursor=\u0026limit=3\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/trades?base_asset_code=USD\u0026base_asset_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026base_asset_type=credit_alphanum4\u0026counter_asset_type=native\u0026cursor=83056000260648961-0\u0026limit=3\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/trades?base_asset_code=USD\u0026base_asset_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026base_asset_type=credit_alphanum4\u0026counter_asset_type=native\u0026cursor=82854686553571330-0\u0026limit=3\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": ""
          },
          "base": {
            "href": "https://expansion-testnet.bantu.network/accounts/GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS"
          },
          "counter": {
            "href": "https://expansion-testnet.bantu.network/accounts/GBCHK52UXADCQCO7FBA5VBYPGCJFXHCNAVJTMUEKOCCNKJH5F35UZU5T"
          },
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/82854686553571330"
          }
        },
        "id": "82854686553571330-0",
        "paging_token": "82854686553571330-0",
        "ledger_close_time": "2018-08-05T00:55:34Z",
        "offer_id": "23074703",
        "base_offer_id": "23074703",
        "base_account": "GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS",
        "base_amount": "22.9174941",
        "base_asset_type": "credit_alphanum4",
        "base_asset_code": "USD",
        "base_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX",
        "counter_offer_id": "4694540704980959234",
        "counter_account": "GBCHK52UXADCQCO7FBA5VBYPGCJFXHCNAVJTMUEKOCCNKJH5F35UZU5T",
        "counter_amount": "97.9999800",
        "counter_asset_type": "native",
        "base_is_seller": true,
        "price": {
          "n": 106905209,
          "d": 25000000
        }
      },
      {
        "_links": {
          "self": {
            "href": ""
          },
          "base": {
            "href": "https://expansion-testnet.bantu.network/accounts/GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS"
          },
          "counter": {
            "href": "https://expansion-testnet.bantu.network/accounts/GDURV3I6U5OTUV75WWAG2HWZTQHNMCR3NR2P5GPKDCIS2AEWCFSOLVFU"
          },
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/83005225157287937"
          }
        },
        "id": "83005225157287937-0",
        "paging_token": "83005225157287937-0",
        "ledger_close_time": "2018-08-07T02:01:53Z",
        "offer_id": "23400441",
        "base_offer_id": "23400441",
        "base_account": "GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS",
        "base_amount": "1.0000000",
        "base_asset_type": "credit_alphanum4",
        "base_asset_code": "USD",
        "base_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX",
        "counter_offer_id": "4694691243584675841",
        "counter_account": "GDURV3I6U5OTUV75WWAG2HWZTQHNMCR3NR2P5GPKDCIS2AEWCFSOLVFU",
        "counter_amount": "4.3080953",
        "counter_asset_type": "native",
        "base_is_seller": true,
        "price": {
          "n": 430809521,
          "d": 100000000
        }
      },
      {
        "_links": {
          "self": {
            "href": ""
          },
          "base": {
            "href": "https://expansion-testnet.bantu.network/accounts/GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS"
          },
          "counter": {
            "href": "https://expansion-testnet.bantu.network/accounts/GBNDB4UHLDRBLR35JNU4ADYG3J5WA4LJZOPBXMNHZKTKSL37BDX4UBQY"
          },
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/83056000260648961"
          }
        },
        "id": "83056000260648961-0",
        "paging_token": "83056000260648961-0",
        "ledger_close_time": "2018-08-07T18:27:33Z",
        "offer_id": "23400441",
        "base_offer_id": "23400441",
        "base_account": "GD47M25MLSCSYP4SIVNQXVQ4KWNLVGXS4S2AXPTYEJK6OY4VALJWK4BS",
        "base_amount": "1.0000000",
        "base_asset_type": "credit_alphanum4",
        "base_asset_code": "USD",
        "base_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX",
        "counter_offer_id": "4694742018688036865",
        "counter_account": "GBNDB4UHLDRBLR35JNU4ADYG3J5WA4LJZOPBXMNHZKTKSL37BDX4UBQY",
        "counter_amount": "4.3080953",
        "counter_asset_type": "native",
        "base_is_seller": true,
        "price": {
          "n": 430809521,
          "d": 100000000
        }
      }
    ]
  }
}

```

```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var tradesHandler = function (resp) {
  console.log(resp);
};

var es = server
  .trades()
  .forAssetPair(
    new StellarSdk.Asset(
      "USD",
      "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX",
    ),
    new StellarSdk.Asset.native(),
  )
  .cursor("now")
  .stream({ onmessage: tradesHandler });
```

