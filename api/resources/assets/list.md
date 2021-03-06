---
title: List All Assets
order: 20
---

# List

This endpoint lists all assets.

 - ARGUMENT - 

* asset\_code `optional`

  The code of the asset you would like to filter by.

* asset\_issuer `optional`

  The Stellar address of the issuer for the asset you would like to filter by.

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
  .assets()
  .forCode("CNY")
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
curl "https://expansion-testnet.bantu.network/assets?asset_code=CNY&limit=3"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/assets?asset_code=CNY\u0026cursor=\u0026limit=3\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/assets?asset_code=CNY\u0026cursor=CNY_GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH_credit_alphanum4\u0026limit=3\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/assets?asset_code=CNY\u0026cursor=CNY_GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3_credit_alphanum4\u0026limit=3\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "toml": {
            "href": "https://stellar.chenyuzhifu.com/.well-known/stellar.toml"
          }
        },
        "asset_type": "credit_alphanum4",
        "asset_code": "CNY",
        "asset_issuer": "GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3",
        "paging_token": "CNY_GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3_credit_alphanum4",
        "amount": "997268.0000000",
        "num_accounts": 23,
        "flags": {
          "auth_required": false,
          "auth_revocable": false,
          "auth_immutable": false
        }
      },
      {
        "_links": {
          "toml": {
            "href": "https://ripplefox.com/.well-known/stellar.toml"
          }
        },
        "asset_type": "credit_alphanum4",
        "asset_code": "CNY",
        "asset_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX",
        "paging_token": "CNY_GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX_credit_alphanum4",
        "amount": "18318343.2623217",
        "num_accounts": 5514,
        "flags": {
          "auth_required": false,
          "auth_revocable": false,
          "auth_immutable": false
        }
      },
      {
        "_links": {
          "toml": {
            "href": "https://naobtc.com/.well-known/stellar.toml"
          }
        },
        "asset_type": "credit_alphanum4",
        "asset_code": "CNY",
        "asset_issuer": "GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH",
        "paging_token": "CNY_GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH_credit_alphanum4",
        "amount": "0.0000000",
        "num_accounts": 1,
        "flags": {
          "auth_required": false,
          "auth_revocable": false,
          "auth_immutable": false
        }
      }
    ]
  }
}
```

```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var callback = function (resp) {
  console.log(resp);
};

var es = server
  .assets()
  .forCode("CNY")
  .cursor("now")
  .stream({ onmessage: callback });
```

