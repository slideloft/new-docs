---
title: Effect Types
order: 10
---

# Types

There are eight groups of effect types. Each effect type has its own set of attributes.

## Account Effects

 - TYPE  OPERATION\(S\) - 

* Account Created

  create\_account

* Account Removed

  merge\_account

* Account Credited

  create\_account, payment, path\_payment, merge\_account

* Account Debited

  create\_account, payment, path\_payment, merge\_account

* Account Thresholds Updated

  set\_options

* Account Home Domain Updated

  set\_options

* Account Flags Updated

  set\_options

* Account Inflation Destination Updated

  set\_options

#### Signer Effects

* Signer Created

  set\_options

* Signer Removed

  set\_options

* Signer Updated

  set\_options

#### Trustline Effects

* Trustline Created

  change\_trust

* Trustline Removed

  change\_trust

* Trustline Updated

  change\_trust, allow\_trust

* Trustline Authorized

  allow\_trust

* Trustline Deauthorized

  allow\_trust

#### Trading Effects

* Offer Created

  manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer

* Offer Removed

  manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment

* Offer Updated

  manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment

* Trade

  manage\_buy\_offer, manage\_sell\_offer, create\_passive\_sell\_offer, path\_payment

#### Data Effects

* Data Created

  manage\_data

* Data Removed

  manage\_data

* Data Updated

  manage\_data

#### Claimable Balance Effects

* Claimable Balance Created

  create\_claimable\_balance

* Claimable Balance Claimant Created

  create\_claimable\_balance

* Claimable Balance Claimed

  claim\_claimable\_balance

#### Sponsorship Effects

* Account Sponsorship Created

  create\_account

* Account Sponsorship Updated

  revoke\_sponsorship

* Account Sponsorship Removed

  revoke\_sponsorship

* Trustline Sponsorship Created

  change\_trust

* Trustline Sponsorship Updated

  revoke\_sponsorship

* Trustline Sponsorship Removed

  revoke\_sponsorship

* Account Data Sponsorship Created

  manage\_data

* Account Data Sponsorship Updated

  revoke\_sponsorship

* Account Data Sponsorship Removed

  revoke\_sponsorship

* Claimable Balance Sponsorship Created

  create\_claimable\_balance

* Claimable Balance Sponsorship Updated

  revoke\_sponsorship

* Claimable Balance Sponsorship Removed

  revoke\_sponsorship

* Account Signer Sponsorship Created

  set\_options

* Account Signer Sponsorship Updated

  revoke\_sponsorship

* Account Signer Sponsorship Removed

  revoke\_sponsorship

#### Miscellaneous Effects

* Sequence Bumped

  bump\_sequence

