---
title: Retrieve an Offer
order: 20
---

# Single

The single offer endpoint provides information on a specific offer.

 - ARGUMENT - 

* offer\_id `required`

  A unique identifier for this offer.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .offers()
  .offer("165563085")
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
curl "https://expansion-testnet.bantu.network/offers/165563085"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/offers/165563085"
    },
    "offer_maker": {
      "href": "https://expansion-testnet.bantu.network/accounts/GCM4PT6XDZBWOOENDS6FOU22GJQLJPV2GC7VRVII4TFGZBA3ZXNM55SV"
    }
  },
  "id": 165563085,
  "paging_token": "165563085",
  "seller": "GCM4PT6XDZBWOOENDS6FOU22GJQLJPV2GC7VRVII4TFGZBA3ZXNM55SV",
  "selling": {
    "asset_type": "credit_alphanum4",
    "asset_code": "USD",
    "asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
  },
  "buying": {
    "asset_type": "native"
  },
  "amount": "26.1075388",
  "price_r": {
    "n": 1449156725,
    "d": 84642346
  },
  "price": "17.1209423",
  "last_modified_ledger": 28412042,
  "last_modified_time": null
}
```

