---
title: Retrieve an Account's Data
order: 90
---

# Data

This endpoint represents a single data for a given account.

 - ARGUMENT - 

* account\_id `required`

  This account’s public key encoded in a base32 string representation.

* key `required`

  The key name for this data.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .loadAccount("GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2")
  .then(function (account) {
    return account.data({ key: "config.memo_required" });
  })
  .then(function (resp) {
    console.log(resp);
  })
  .catch(function (err) {
    console.error(err);
  });
```
{% endtab %}

{% tab title="cURL" %}
```javascript
curl "https://expansion-testnet.bantu.network/accounts/GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2/data/config.memo_required"
```
{% endtab %}
{% endtabs %}

```bash

{
  "value": "MQ=="
}
```

