---
title: Rate Limiting
order: 40
---

# Rate Limiting

Horizon rate limits on a per-IP-address basis. By default, a client is limited to 3600 requests per hour - one request per second on average.

While streaming, each update of the stream counts as a request and against a client’s allotted rate limit.

