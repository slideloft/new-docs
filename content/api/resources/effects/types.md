---
title: Effect Types
order: 10
---

# types

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

There are eight groups of effect types. Each effect type has its own set of attributes.

## Account Effects

 - TYPE - skip - OPERATION\(S\) - Account Created - skip - create\_account - Account Removed - skip - merge\_account - Account Credited - skip - create\_account, payment, path\_payment, merge\_account - Account Debited - skip - create\_account, payment, path\_payment, merge\_account - Account Thresholds Updated - skip - set\_options - Account Home Domain Updated - skip - set\_options - Account Flags Updated - skip - set\_options - Account Inflation Destination Updated - skip - set\_options

## Signer Effects

 - TYPE - skip - OPERATION\(S\) - Signer Created - skip - set\_options - Signer Removed - skip - set\_options - Signer Updated - skip - set\_options

## Trustline Effects

 - TYPE - skip - OPERATION\(S\) - Trustline Created - skip - change\_trust - Trustline Removed - skip - change\_trust - Trustline Updated - skip - change\_trust, allow\_trust - Trustline Authorized - skip - allow\_trust - Trustline Deauthorized - skip - allow\_trust

## Trading Effects

 - TYPE - skip - OPERATION\(S\) - Offer Created - skip - manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer - Offer Removed - skip - manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment - Offer Updated - skip - manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment - Trade - skip - manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment

## Data Effects

 - TYPE - skip - OPERATION\(S\) - Data Created - skip - manage\_data - Data Removed - skip - manage\_data - Data Updated - skip - manage\_data

## Claimable Balance Effects

 - TYPE - skip - OPERATION\(S\) - Claimable Balance Created - skip - create\_claimable\_balance - Claimable Balance Claimant Created - skip - create\_claimable\_balance - Claimable Balance Claimed - skip - claim\_claimable\_balance

## Sponsorship Effects

 - TYPE - skip - OPERATION\(S\) - Account Sponsorship Created - skip - create\_account - Account Sponsorship Updated - skip - revoke\_sponsorship - Account Sponsorship Removed - skip - revoke\_sponsorship - Trustline Sponsorship Created - skip - change\_trust - Trustline Sponsorship Updated - skip - revoke\_sponsorship - Trustline Sponsorship Removed - skip - revoke\_sponsorship - Account Data Sponsorship Created - skip - manage\_data - Account Data Sponsorship Updated - skip - revoke\_sponsorship - Account Data Sponsorship Removed - skip - revoke\_sponsorship - Claimable Balance Sponsorship Created - skip - create\_claimable\_balance - Claimable Balance Sponsorship Updated - skip - revoke\_sponsorship - Claimable Balance Sponsorship Removed - skip - revoke\_sponsorship - Account Signer Sponsorship Created - skip - set\_options - Account Signer Sponsorship Updated - skip - revoke\_sponsorship - Account Signer Sponsorship Removed - skip - revoke\_sponsorship

## Miscellaneous Effects

 - TYPE - skip - OPERATION\(S\) - Sequence Bumped - skip - bump\_sequence

