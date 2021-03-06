---
title: Retrieve a Ledger's Operations
order: 40
---

# Operations

This endpoint returns successful operations in a specific ledger.

 \| \| \| \| --- \| --- \| \| GET \| /ledgers/:ledger\_sequence/operations?cursor={paging\_token}&order={asc,desc}&limit={1-200}&include\_failed{true,false}&join={transactions} \|



**ARGUMENTS**

* ledger\_sequencerequired

  The sequence number of a specific ledger.

* cursoroptional

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* orderoptional

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limitoptional

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

* include\_failedoptional

  Set to true to include failed operations in results. Options include `true` and `false`.

* joinoptional

  Set to `transactions` to include the transactions which created each of the operations in the response.

Example RequestcURLJavaScript

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .operations()
  .forLedger("27147222")
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
curl "https://expansion-testnet.bantu.network/ledgers/27147222/operations?limit=2"
```
{% endtab %}
{% endtabs %}

Example Response  


```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27147222/operations?cursor=\u0026limit=2\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27147222/operations?cursor=116596430667259905\u0026limit=2\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27147222/operations?cursor=116596430667255809\u0026limit=2\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/116596430667255809"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/3a644389bbec63dd2b107a03c16711563fc549daa7b7f56f951a2e470f81f2e0"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/116596430667255809/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=116596430667255809"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=116596430667255809"
          }
        },
        "id": "116596430667255809",
        "paging_token": "116596430667255809",
        "transaction_successful": true,
        "source_account": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH",
        "type": "payment",
        "type_i": 1,
        "created_at": "2019-12-06T23:05:38Z",
        "transaction_hash": "3a644389bbec63dd2b107a03c16711563fc549daa7b7f56f951a2e470f81f2e0",
        "asset_type": "credit_alphanum4",
        "asset_code": "NODL",
        "asset_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL",
        "from": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH",
        "to": "GAD35Y7AEQYS4WNZND5OV7HQ6ALBDDNTNFO2TN2CM4ERE7ZV4FJBNXZ6",
        "amount": "0.0000077"
      },
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/116596430667259905"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/83eabfa824b57436eda49bb9ac28675285f6d945325f69db41792078a83d3479"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/116596430667259905/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=116596430667259905"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=116596430667259905"
          }
        },
        "id": "116596430667259905",
        "paging_token": "116596430667259905",
        "transaction_successful": true,
        "source_account": "GBE63IHPHXHKQHIF7L5P5MGOV4MMDYE6RGZCJYWJPBRQZDJ5MOAPOX7A",
        "type": "manage_offer",
        "type_i": 3,
        "created_at": "2019-12-06T23:05:38Z",
        "transaction_hash": "83eabfa824b57436eda49bb9ac28675285f6d945325f69db41792078a83d3479",
        "amount": "0.0000023",
        "price": "0.0484621",
        "price_r": {
          "n": 484621,
          "d": 10000000
        },
        "buying_asset_type": "native",
        "selling_asset_type": "credit_alphanum4",
        "selling_asset_code": "RMT",
        "selling_asset_issuer": "GDEGOXPCHXWFYY234D2YZSPEJ24BX42ESJNVHY5H7TWWQSYRN5ZKZE3N",
        "offer_id": 0
      }
    ]
  }
}
```

