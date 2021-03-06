---
title: Errors
order: 0
---

# Index

After processing a request, Horizon returns a success or error response to the client. A success response will return a Status Code of 200, and an error response will return a Status Code in the range of 4XX - 5XX along with additional information about why the request could not complete successfully.

There are two categories of errors: [HTTP Status Codes](http-status-codes/index.md) and [Result Codes](result-codes/index-1.md). Result Codes only follow a Transaction Failed \(400\) HTTP Status Code.



Error Categories

| [HTTP Status Codes](https://developers.stellar.org/api/errors/http-status-codes/) | Errors that occur at the Horizon Server level. |
| :--- | :--- |
| [Result Codes](https://developers.stellar.org/api/errors/result-codes/) | Errors that occur at the Stellar Core level. |

