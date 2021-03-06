---
title: The Account Object
order: 10
---

# Object

When Horizon returns information about an account, it uses the following format:

 - ATTRIBUTE - 

* id `string`

  A unique identifier for this account.

* account\_id `string`

  This account’s public key encoded in a base32 string representation.

* sequence `number`

  This account’s current sequence number. For use when submitting this account’s next transaction.

* subentry\_count `number`

  The number of subentries on this account.

* home\_domain `string`

  The domain that hosts this account’s `stellar.toml` file.

* last\_modified\_ledger `number`

  The ID of the last ledger that included changes to this account.

* num\_sponsoring `number`

  The number of reserves sponsored by this account.

* num\_sponsored `number`

  The number of reserves sponsored for this account.

* sponsor `string (optional)`

  The account ID of the sponsor who is paying the reserves for this account.

* thresholds `object`

  Operations have varying levels of access. This field specifies thresholds for different access levels, as well as the weight of the master key. Hide child attributes

  * low\_threshold `number`

    The weight required for a valid transaction including the Allow Trust and Bump Sequence operations.

  * med\_threshold `number`

    The weight required for a valid transaction including the Create Account, Payment, Path Payment, Manage Buy Offer, Manage Sell Offer, Create Passive Sell Offer, Change Trust, Inflation, and Manage Data operations.

  * high\_threshold `number`

    The weight required for a valid transaction including the Account Merge and Set Options operations.

* flags `object`

  Flags denote the enabling/disabling of certain asset issuer privileges. Hide child attributes

  * auth\_immutable `boolean`

    If set to `true`, none of the following flags can be changed.

  * auth\_required boolean

    If set to `true`, anyone who wants to hold an asset issued by this account must first be approved by this account.

  * auth\_revocable `boolean`

    If set to `true`, this account can freeze the balance of a holder of an asset issued by this account.

* balances `object`

  The assets this account holds.Hide child attributes

  * balance `string`

    The number of units of an asset held by this account.

  * buying\_liabilities `string`

    The sum of all buy offers owned by this account for this asset.

  * selling\_liabilities `string`

    The sum of all sell offers owned by this account for this asset.

  * limit `number (optional)`

    The maximum amount of this asset that this account is willing to accept. Specified when opening a trustline.

  * asset\_type `string`

    Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

  * asset\_code `string (optional)`

    The code for this asset.

  * asset\_issuer `string (optional)`

    The Stellar address of this asset’s issuer.

  * sponsor `string (optional)`

    The account ID of the sponsor who is paying the reserves for this trustline.

* signers `array of objects`

  The public keys and associated weights that can be used to authorize transactions for this account. Used for multi-sig.Hide child attributes

  * public\_key `string`

    **REMOVED in 0.17.0: USE `key` INSTEAD.**

  * weight `number`

    The numerical weight of a signer. Used to determine if a transaction meets the `threshold` requirements.

  * sponsor `string (optional)`

    The account ID of the sponsor who is paying the reserves for this signer.

  * key `string`

    A hash of characters dependent on the signer type.

  * type `string`

    The type of hash for this signer.Hide child attributes

    * ed25519\_public\_key

      A normal Stellar public key.

    * sha256\_hash

      The SHA256 hash of some arbitrary `x`. Adding a signature of this type allows anyone who knows x to sign a transaction from this account. _Note: Once this transaction is broadcast, x will be known publicly._

    * preauth\_tx

      The hash of a pre-authorized transaction. This signer is automatically removed from the account when a matching transaction is properly applied.

* data `object`

  An array of account data fields.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U"
    },
    "transactions": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/effects{?cursor,limit,order}",
      "templated": true
    },
    "offers": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/offers{?cursor,limit,order}",
      "templated": true
    },
    "trades": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/trades{?cursor,limit,order}",
      "templated": true
    },
    "data": {
      "href": "https://expansion-testnet.bantu.network/accounts/GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U/data/{key}",
      "templated": true
    }
  },
  "id": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "account_id": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "sequence": "24739097524306468",
  "subentry_count": 3,
  "inflation_destination": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
  "home_domain": "tempo.eu.com",
  "last_modified_ledger": 23569316,
  "num_sponsoring": 0,
  "num_sponsored": 0,
  "thresholds": {
    "low_threshold": 5,
    "med_threshold": 0,
    "high_threshold": 0
  },
  "flags": {
    "auth_required": false,
    "auth_revocable": true,
    "auth_immutable": false
  },
  "balances": [
    {
      "balance": "1.0000005",
      "limit": "922337203685.4775807",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "last_modified_ledger": 22651481,
      "is_authorized": true,
      "asset_type": "credit_alphanum4",
      "asset_code": "EURT",
      "asset_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S"
    },
    {
      "balance": "0.0000000",
      "limit": "922337203685.4775807",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "last_modified_ledger": 7877447,
      "is_authorized": false,
      "asset_type": "credit_alphanum4",
      "asset_code": "PHP",
      "asset_issuer": "GBUQWP3BOUZX34TOND2QV7QQ7K7VJTG6VSE7WMLBTMDJLLAW7YKGU6EP"
    },
    {
      "balance": "0.0000000",
      "limit": "922337203685.4775807",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "last_modified_ledger": 20213845,
      "is_authorized": true,
      "asset_type": "credit_alphanum4",
      "asset_code": "NGN",
      "asset_issuer": "GCC4YLCR7DDWFCIPTROQM7EB2QMFD35XRWEQVIQYJQHVW6VE5MJZXIGW"
    },
    {
      "balance": "198.8944970",
      "buying_liabilities": "0.0000000",
      "selling_liabilities": "0.0000000",
      "asset_type": "native"
    }
  ],
  "signers": [
    {
      "weight": 10,
      "key": "GDI73WJ4SX7LOG3XZDJC3KCK6ED6E5NBYK2JUBQSPBCNNWEG3ZN7T75U",
      "type": "ed25519_public_key"
    }
  ],
  "data": {},
  "paging_token": ""
}
```

