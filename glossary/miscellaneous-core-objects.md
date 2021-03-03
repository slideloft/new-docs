---
title: Miscellaneous Stellar Core Objects
order: null
---

# Miscellaneous Core Objects

## LedgerKey

LedgerKey holds information to identify a specific ledgerEntry. It is a union that can be any one of the LedgerEntryTypes \(ACCOUNT, TRUSTLINE, OFFER, DATA, or CLAIMABLE\_BALANCE\). Search for LedgerKey in [stellar-ledger-entries.x](https://github.com/stellar/stellar-core/blob/master/src/xdr/Stellar-ledger-entries.x) for more information.

## OperationID

OperationID is a union with one possible type \(ENVELOPE\_TYPE\_OP\_ID\). It contains the transaction source account, sequence number, and the operation index of the CreateClaimableBalance operation in the transaction. Search for OperationID in [stellar-transactions.x](https://github.com/stellar/stellar-core/blob/master/src/xdr/Stellar-transaction.x) for more information.

## ClaimableBalanceID

ClaimableBalanceID is a union with one possible type \(CLAIMABLE\_BALANCE\_ID\_TYPE\_V0\). It contains a SHA-256 hash of the OperationID for Claimable Balances.

