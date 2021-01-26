---
title: Key Management Basics
order: 30
---

# key-management

Step one for any app is to sort out user onboarding. Since a Stellar wallet is an interface that gives a user access to an account stored on the ledger, and since that access is controlled by the account's secret key, the first thing you have to decide is how to handle a user's secret key, and how to append the Stellar account it unlocks to a user object.

The most important question: who will “own” the account? There are three possible answers:

1. You, the service provider, store the secret key and delegate usage rights to the user. This is a “custodial” service.
2. They, the user, will store their own account credentials and permission your app to send requests or delegate transaction signing. This is a “non-custodial” service.
3. A mixture of the two via multisig. This is especially useful for maintaining non-custodial status while still allowing for account recovery.

Be very careful taking a custodial approach or using any mixture where you are storing user secrets. It’s easy to get wrong, and the consequences can be devastating. For our purposes, we will assume choice \#2. This tutorial will show you how to build a non-custodial service.

The non-custodial option poses some very real usability issues: your user has to securely store their own account credentials and safely navigate transaction signing on their end. There are ways to make that process more user-friendly, one of which is to create a keystore file guarded by a passphrase, and that's the approach we'll take in this tutorial.

Creating a keystore file and storing it locally in the browser allows a user to import or export it into other systems, and works pretty well as long as the user's passphrase is secure enough. We don't recommend this approach for high-security production applications, but it's the best way to get started, and for this tutorial, which lays out the foundation for a basic Stellar wallet, it’ll work just fine.

## Third-party Key Management Applications

There are also several apps and services that specialize in adding additional security layers to users' accounts. Check them out if you're interested:

* [Albedo](https://albedo.link/)
* [StellarAuth](https://stellarauth.com/)
* [Stellar Authenticator](https://stellar-authenticator.org/)
* [Ledger](https://www.ledger.com/)
* [Trezor](https://trezor.io/)
* [StellarGuard](https://stellarguard.me/)
* [LobstrVault](https://vault.lobstr.co/)

