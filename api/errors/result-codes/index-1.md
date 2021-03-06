---
title: Result Codes
order: 0
---

# Index

import { MethodTable } from "components/MethodTable";

Result Codes describe why a transaction or operation failed in Stellar Core and are communicated in the “extras” field of a Horizon response when the “Transaction Failed” Status Code is returned.

In the “extras” field, the errors returned are referred to as “Result Codes” and are Horizon’s abstraction of “Stellar Protocol Codes”, which are more specific codes available in the XDR. Result Codes are Horizon’s way of normalizing Stellar Protocol Codes.

There are three types of Result Codes: [Transaction Result Codes](transactions.md), [Operation Result Codes](operations.md), and [Operation-Specific Result Codes](operation-specific/index.md).



Result Code Types

| [Transaction Result Codes](https://developers.stellar.org/api/errors/result-codes/transactions/) | Generic errors about transaction failures. |
| :--- | :--- |
| [Operation Result Codes](https://developers.stellar.org/api/errors/result-codes/operations/) | Generic errors about operation failures. |
| [Operation-Specific Result Codes](https://developers.stellar.org/api/errors/result-codes/operation-specific/) | Errors specific to each operation type. |

