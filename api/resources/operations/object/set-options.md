---
title: Set Options Object
order: 80
---

# Set Options

Sets an account's flags, inflation destination, signers, and home domain.

See the [`Set Options` errors](../../../errors/result-codes/operation-specific/set-options.md).

 - ATTRIBUTE - 



* signer\_key `string`

  The public key of the new signer.

* signer\_weight `number`

  The weight of the new signer. Can range from `1` to `255`.

* master\_key\_weight `number`

  The weight of the master key. Can range from `1` to `255`.

* low\_threshold `number`

  The sum weight for the low threshold.

* med\_threshold `number`

  The sum weight for the medium threshold.

* high\_threshold `number`

  The sum weight for the high threshold.

* home\_domain `string`

  The home domain used for stellar.toml file discovery.

* set\_flags `array`

  The array of numeric values of flags that has been set in this operation. Options include `1` for `AUTH_REQUIRED_FLAG`, `2` for `AUTH_REVOCABLE_FLAG`, and `4` for `AUTH_IMMUTABLE_FLAG`.

* set\_flags\_s `array`

  The array of string values of flags that has been set in this operation. Options include `AUTH_REQUIRED_FLAG`, `AUTH_REVOCABLE_FLAG`, and `AUTH_IMMUTABLE_FLAG`.

* clear\_flags `array`

  The array of numeric values of flags that has been cleared in this operation. Options include `1` for `AUTH_REQUIRED_FLAG`, `2` for `AUTH_REVOCABLE_FLAG`, and `4` for `AUTH_IMMUTABLE_FLAG`.

* clear\_flags\_s `array`

  The array of string values of flags that has been cleared in this operation. Options include `AUTH_REQUIRED_FLAG`, `AUTH_REVOCABLE_FLAG`, and `AUTH_IMMUTABLE_FLAG`.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/102125410241826819"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/e020277cf755a1c29234d34f123f546a2c4805d7b4ca9303e253667b0ff4d846"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/102125410241826819/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=102125410241826819"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=102125410241826819"
    }
  },
  "id": "102125410241826819",
  "paging_token": "102125410241826819",
  "transaction_successful": true,
  "source_account": "GABMKJM6I25XI4K7U6XWMULOUQIQ27BCTMLS6BYYSOWKTBUXVRJSXHYQ",
  "type": "set_options",
  "type_i": 5,
  "created_at": "2019-05-08T21:20:34Z",
  "transaction_hash": "e020277cf755a1c29234d34f123f546a2c4805d7b4ca9303e253667b0ff4d846",
  "home_domain": "www.stellar.org"
}
```

