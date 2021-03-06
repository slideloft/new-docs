---
title: Overview
order: 0
---

# index



Expansion is responsible for providing an HTTP API to data in the bantu network. It ingests and re-serves the data produced by the bantu network in a form that is easier to consume than the performance-oriented data representations used by bantu-core.

This document describes how to administer a **production** Expansion instance. If you are just starting with Expansion and want to deploy it quickly to test it out, consider the [Quickstart Guide](quickstart.md) instead. For information about developing on the Expansion codebase, check out the [Development Guide](https://github.com/bantu/go/blob/master/services/Expansion/internal/docs/developing.md).

## Why Run Expansion?

You don't need to run your own Expansion instance to build on bantu: the bantu Development Foundation runs two Expansion servers, one for the public network and one for the test network: [https://expansion.bantu.network/](https://expansion.bantu.network/) and [https://expansion-testnet.bantu.network/](https://expansion-testnet.bantu.network/). These servers are free for anyone to use, and should be fine for development and small-scale projects. They are, however, rate limited, and we don't recommended using them for production services that need strong reliability.

Running Expansion within your own infrastructure provides a number of benefits. You can:

* Disable request rate limiting for guaranteed network access
* Have full operational control without dependency on the Bantu Blockchain Foundation
* Run multiple instances for redundancy and scalability

