---
title: Manage Data Object
order: 120
---

# Manage Data

Set, modify, or delete a data entry \(name/value pair\) for an account.

See the [`Manage Data` errors](../../../errors/result-codes/operation-specific/manage-data.md).

 - ATTRIBUTE - 

* name `string`

  The key for this data entry. It can be up to 64 bytes long. If this is a new `Name`, it will add the given name/value pair to the account. If this `Name` is already present, then the associated value will be modified.

* value `string`

  If present, then this value will be set in the DataEntry. It can be up to 64 bytes long. If not present, then the existing `Name` will be deleted.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/121957408846438401"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/1e1b8f628c338a0306cbcb512bd89473a0c6b25df67ad77cfc1478437a575665"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/121957408846438401/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121957408846438401"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121957408846438401"
    }
  },
  "id": "121957408846438401",
  "paging_token": "121957408846438401",
  "transaction_successful": true,
  "source_account": "GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2",
  "type": "manage_data",
  "type_i": 10,
  "created_at": "2020-02-25T17:47:32Z",
  "transaction_hash": "1e1b8f628c338a0306cbcb512bd89473a0c6b25df67ad77cfc1478437a575665",
  "name": "config.memo_required",
  "value": "MQ=="
}
```

