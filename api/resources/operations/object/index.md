---
title: The Operation Object
order: 0
---

# Index

Each of Bantu’s operations have unique response shapes. Below are the attributes that are common across individual operation objects.

See the [generic Operation errors](../../../errors/result-codes/operations.md).

**ATTRIBUTE**

* id `number`

  The operation’s ID number.

* paging\_token `string`

  A cursor value for use in [pagination](https://developers.stellar.org/api/introduction/pagination/).

* type\_i `number`

  A number indicating the operation type.

* type `string`

  The name of the operation type.

* transaction\_hash `string`

  A unique identifier for the transaction this operation belongs to.

* transaction\_successful `boolean`

  Indicates if this operation was part of a successful transaction.

* source\_account `string`

  The account that originates the operation.

* created\_at `string`

  The date this operation was created.

```bash
{
  "_links": {
    "effects": {
      "href": "/operations/402494270214144/effects/{?cursor,limit,order}",
      "templated": true
    },
    "precedes": {
      "href": "/operations?cursor=402494270214144&order=asc"
    },
    "self": {
      "href": "/operations/402494270214144"
    },
    "succeeds": {
      "href": "/operations?cursor=402494270214144&order=desc"
    },
    "transactions": {
      "href": "/transactions/402494270214144"
    }
  },
  "id": 402494270214144,
  "paging_token": "402494270214144",
  "type_i": 0,
  "type": "create_account"
}
```

