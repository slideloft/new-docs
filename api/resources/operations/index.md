---
title: Operations
order: 0
---

# index

import { EndpointsTable } from "components/EndpointsTable";

Operations are objects that represent a desired change to the ledger: payments, offers to exchange currency, changes made to account options, etc. Operations are submitted to the Stellar network grouped in a Transaction.

Each of Stellar’s operations have a unique operation object.

 \| \| \| \| --- \| -------------------------------------------------- \| \| GET \| \[/operations/:operation\_id\]\(./single.mdx\) \| \| GET \| \[/operations/:operation\_id/effects\]\(./effects.mdx\) \| \| GET \| \[/operations\]\(./list.mdx\) \| \| GET \| \[/payments\]\(./list-payments.mdx\) \|

