---
title: The Order Book Object
order: 10
---

# object

When Horizon returns information about an order book, it uses the following format:

 - ATTRIBUTE - 

* bids `object`

  The prices and amounts for the buyside of the asset pair.Hide child attributes

  * price\_robject

    A precise representation of the bid price of the asset pair.Hide child attributes

    * nnumber

      The numerator.

    * dnumber

      The denominator.

  * price `string`

    The bid price of the base asset denominated in the counter asset. A number representing the decimal form of `price_r`.

  * amount `string`

    The amount of counter asset that the account making this offer is willing to buy at this price.

* asks `object`

  The prices and amounts for the sellside of the asset pair.Hide child attributes

  * price\_robject

    A precise representation of the ask price of the asset pair.Hide child attributes

    * nnumber

      The numerator.

    * dnumber

      The denominator.

  * price `string`

    The ask price of the base asset denominated in the counter asset. A number representing the decimal form of `price_r`.

  * amount `string`

    The amount of counter asset that the account making this offer is willing to sell at this price.

* base `object`

  Details about the base asset. Hide child attributes

  * asset\_type `string`

    The type for the base asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

  * asset\_code `string`

    The code for the base asset.

  * asset\_issuer `string`

    The Stellar address of the base asset’s issuer.

* counter `object`

  Details about the counter asset. Hide child attributes

  * asset\_type `string`

    The type for the counter asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

  * asset\_code `string`

    The code for the counter asset.

  * asset\_issuer `string`

    The Stellar address of the counter asset’s issuer.

```bash
{
  "bids": [
    {
      "price_r": {
        "n": 6014600,
        "d": 102275119
      },
      "price": "0.0588080",
      "amount": "0.1722469"
    },
    {
      "price_r": {
        "n": 1250000,
        "d": 21831117
      },
      "price": "0.0572577",
      "amount": "0.2991796"
    }
  ],
  "asks": [
    {
      "price_r": {
        "n": 118163,
        "d": 2000000
      },
      "price": "0.0590815",
      "amount": "8057.2710223"
    },
    {
      "price_r": {
        "n": 60627,
        "d": 1000000
      },
      "price": "0.0606270",
      "amount": "10000.0000000"
    }
  ],
  "base": {
    "asset_type": "native"
  },
  "counter": {
    "asset_type": "credit_alphanum4",
    "asset_code": "USD",
    "asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
  }
}
```

