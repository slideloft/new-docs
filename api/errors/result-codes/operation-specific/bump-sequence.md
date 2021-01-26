---
title: Bump Sequence Result Codes
order: 130
---

# bump-sequence

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Bump Sequence` operation.

Learn more about the [`Bump Sequence` operation](../../../../docs/start/list-of-operations.md#bump-sequence).

 - OpSuccess - BUMP\_SEQUENCE\_SUCCESS - Sequence number has been bumped. - op\_bad\_seq - BUMP\_SEQUENCE\_BAD\_SEQ - The specified bumpTo sequence number is not a valid sequence number. It must be between 0 and INT64\_MAX \(9223372036854775807 or 0x7fffffffffffffff\).

