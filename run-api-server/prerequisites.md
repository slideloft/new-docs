---
title: Prerequisites
order: 10
---

# prerequisites



Currently, Expansion is dependent on a Bantu Core server. While we are working to reduce that dependence, at the moment it still needs access to both the SQL database and the HTTP API published by Bantu Core. See [Run a Core Node](../run-core-node/index.md) to learn how to set up and administer a Bantu Core node.

Expansion is also dependent upon a postgres server, which it uses to store processed Core data for ease of use. Expansion requires postgres version &gt;= 9.5.

In addition to the two prerequisites above, you may optionally install a redis server to be used for rate limiting requests.

