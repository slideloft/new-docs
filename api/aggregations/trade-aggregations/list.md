---
title: List Trade Aggregations
order: 20
---

# List

This endpoint displays trade data based on filters set in the arguments.

This is done by dividing a given time range into segments and aggregating statistics, for a given asset pair \(base, counter\) over each of these segments.

The duration of the segments is specified with the `resolution` parameter. The start and end of the time range are given by `startTime` and `endTime` respectively, which are both rounded to the nearest multiple of `resolution` since epoch.

The individual segments are also aligned with multiples of `resolution` since epoch. If you want to change this alignment, the segments can be `offset` by specifying the offset parameter.

 - ARGUMENT - 

* start\_time `long`

  The lower time boundary represented as milliseconds since epoch.

* end\_time `long`

  The upper time boundary represented as milliseconds since epoch.

* resolution `long`

  The segment duration represented as milliseconds. Supported values are 1 minute \(60000\), 5 minutes \(300000\), 15 minutes \(900000\), 1 hour \(3600000\), 1 day \(86400000\) and 1 week \(604800000\).

* offset `long`

  Segments can be offset using this parameter. Expressed in milliseconds. Can only be used if the resolution is greater than 1 hour. Value must be in whole hours, less than the provided resolution, and less than 24 hours.

* base\_asset\_type `required`

  The type for the base asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* base\_asset\_issuer `optional`

  The Stellar address of the base asset’s issuer. Required if the `base_asset_type` is not `native`.

* base\_asset\_code `optional`

  The code for the base asset. Required if the `base_asset_type` is not `native`.

* counter\_asset\_type `required`

  The type for the counter asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* counter\_asset\_issuer `optional`

  The Stellar address of the counter asset’s issuer. Required if the `counter_asset_type` is not `native`.

* counter\_asset\_code `optional`

  The code for the counter asset. Required if the `counter_asset_type` is not `native`.

* order `optional`

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limit `optional`

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var base = new StellarSdk.Asset.native();
var counter = new StellarSdk.Asset(
  "EURT",
  "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S",
);
var startTime = 1582156800000;
var endTime = 1582178400000;
var resolution = 3600000;
var offset = 0;

server
  .tradeAggregation(base, counter, startTime, endTime, resolution, offset)
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
curl "https://expansion-testnet.bantu.network/trade_aggregations?base_asset_type=native&counter_asset_code=EURT&counter_asset_issuer=GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S&counter_asset_type=credit_alphanum4&resolution=3600000&start_time=1582156800000&end_time=1582178400000"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/trade_aggregations?base_asset_type=native\u0026counter_asset_code=EURT\u0026counter_asset_issuer=GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S\u0026counter_asset_type=credit_alphanum4\u0026resolution=3600000\u0026start_time=1582156800000\u0026end_time=1582178400001"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/trade_aggregations?base_asset_type=native\u0026counter_asset_code=EURT\u0026counter_asset_issuer=GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S\u0026counter_asset_type=credit_alphanum4\u0026end_time=1582178400001\u0026resolution=3600000\u0026start_time=1582171200000"
    },
    "prev": {
      "href": ""
    }
  },
  "_embedded": {
    "records": [
      {
        "timestamp": 1582164000000,
        "trade_count": 3,
        "base_volume": "399.3873200",
        "counter_volume": "25.5368082",
        "avg": "0.0639400",
        "high": "0.0652169",
        "high_r": {
          "N": 652169,
          "D": 10000000
        },
        "low": "0.0638338",
        "low_r": {
          "N": 8107550,
          "D": 127010393
        },
        "open": "0.0652169",
        "open_r": {
          "N": 652169,
          "D": 10000000
        },
        "close": "0.0638338",
        "close_r": {
          "N": 8107550,
          "D": 127010393
        }
      },
      {
        "timestamp": 1582167600000,
        "trade_count": 1,
        "base_volume": "149.8415320",
        "counter_volume": "9.7149804",
        "avg": "0.0648350",
        "high": "0.0648350",
        "high_r": {
          "N": 5000000,
          "D": 77118803
        },
        "low": "0.0648350",
        "low_r": {
          "N": 5000000,
          "D": 77118803
        },
        "open": "0.0648350",
        "open_r": {
          "N": 5000000,
          "D": 77118803
        },
        "close": "0.0648350",
        "close_r": {
          "N": 5000000,
          "D": 77118803
        }
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

var base = new StellarSdk.Asset.native();
var counter = new StellarSdk.Asset(
  "EURT",
  "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S",
);
var startTime = 1582156800000;
var endTime = 1582178400000;
var resolution = 3600000;
var offset = 0;

var es = server
  .tradeAggregation(base, counter, startTime, endTime, resolution, offset)
  .cursor("now")
  .stream({ onmessage: callback });
```

