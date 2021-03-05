---
title: Prerequisites
order: 20
---

# prerequisites

You can install Bantu Core a [number of different ways](installation.md), and once you do, you can [configure](configuring.md) it to participate in the network on several [different levels](index.md#types-of-nodes): it can be a Watcher, a Basic Validator, or a Full Validator. No matter how you install Bantu Core or what kind of node you run, however, you need to set up to connect to the peer-to-peer network, store the state of the ledger in a SQL [database](configuring.md#database), and most likely connect to [expansion](../api/introduction/index.md), the Bantu API.

## Computer Requirements

We recently asked Bantu Core operators about their setups, and should have some updated information soon based on their responses. So stay tuned. In early 2018, Stellar Core with PostgreSQL running on the same machine worked well on a [m5.large](https://aws.amazon.com/ec2/instance-types/m5/) in AWS \(dual-core 2.5 GHz Intel Xeon, 8 GB RAM\). Storage-wise, 20 GB was enough in 2018, but the ledger has grown a lot since then, and most people seem to have at least 1TB on hand.

If you are running Bantu Core in conjunction with expansion, you will need to ensure that your setup is also equipped to handle expansion's [compute requirements](../run-api-server/prerequisites.md) as well.

Bantu Core is designed to run on relatively modest hardware so that a whole range of individuals and organizations can participate in the network, and basic nodes should be able to function pretty well without tremendous overhead. That said, the more you ask of your node, the greater the requirements.

## Network access

Bantu Core interacts with the peer-to-peer network to keep a distributed ledger in sync, which means that your node needs to make certain [TCP ports](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_ports) available for inbound and outbound communication.

* **Inbound**: a Bantu Core node needs to allow all ips to connect to its `PEER_PORT` over TCP. You can specify a port when you [configure Bantu Core](configuring.md), but most people use the default, which is **11625**.
* **Outbound**: a Bantu Core needs to connect to other nodes via thier `PEER_PORT`s TCP. But most use the default port, which is, again, **11625**.

## Internal System Access

Bantu Core also needs to connect to certain internal systems, though exactly how varies based on your setup.

* **Outbound**:
  * Bantu Core requires access to a postgreSQL database. If that databse resides on a different machine on your network, you'll need to allow that connection. You specify the databse when you configure Bantu Core.
  * You can block all other connections.
* **Inbound**: Bantu Core exposes an _unauthenticated_ HTTP endpoint on its `HTTP_PORT`. You can specify a port when you [configure Stellar Core](configuring.md), but most people use the default, which is **11626**.
  * The `HTTP_PORT` is used by expansion to submit transactions, so may have to be exposed to the rest of your internal ips
  * It's also used to query Stellar Core [info](commands.md) and provide [metrics](monitoring.md)
  * And to perform administrative commands such as [scheduling upgrades](network-upgrades.md) and changing log levels
  * For more on that, see [commands](commands.md)

Note: if you need to expose your HTTP endpoint to other hosts in your local network,we recommended using an intermediate reverse proxy server to implement authentication. Don't expose the HTTP endpoint to the raw and cruel open internet.

