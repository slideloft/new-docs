---
title: HTTP Status Codes
order: 0
---

# Index

import { MethodTable } from "components/MethodTable";

Some errors only occur at the Horizon level and are not thrown in Stellar Core. These are usually issues with how the transaction was formed or a conflict between the transaction’s composition and how the Horizon server is setup.

Stellar uses conventional HTTP response codes to indicate the success or failure of an API request. In general:

* Codes in the 2xx range indicate success.
* Codes in the 4xx range indicate an error that failed given the information provided
* Codes in the 5xx range indicate an error with the Horizon server.

There are two types of Status Codes: [Standard Status Codes](standard.md) and [Horizon-Specific Status Codes](https://github.com/slideloft/new-docs/tree/046158a008b14dc6d54bdd6f4c48e078c303a05e/content/api/errors/http-status-codes/horizon-specific.mdx).



HTTP Status Code Types

| [Standard Status Codes](https://developers.stellar.org/api/errors/http-status-codes/standard/) | Generic HTTP responses. |
| :--- | :--- |
| [Horizon-Specific Status Codes](https://developers.stellar.org/api/errors/http-status-codes/horizon-specific/) | Errors that are unique to Horizon. |

