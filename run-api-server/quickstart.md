---
title: Expansion Quickstart
order: 5
---

# quickstart

This document describes how to quickly set up a **test** Bantu Core + Expansion node, that you can play around with to get a feel for how a bantu node operates. **This configuration is not secure!** It is **not** intended as a guide for production administration.

For detailed information about running Expansion and Bantu Core safely in production see the [Run and API Server](index.md) and [Run a Core Node](../run-core-node/index.md).

If you're ready to roll up your sleeves and dig into the code, check out the [Developer Guide](https://github.com/bantu/go/blob/master/services/Expansion/internal/docs/developing.md).

## Install and run the Quickstart Docker Image

The fastest way to get up and running is using the [bantu Quickstart Docker Image](https://github.com/bantu/docker-bantu-core-Expansion). This is a Docker container that provides both `bantu-core` and `Expansion`, pre-configured for testing.

1. Install [Docker](https://www.docker.com/get-started).
2. Verify your Docker installation works: `docker run hello-world`
3. Create a local directory that the container can use to record state. This is helpful because it can take a few minutes to sync a new `bantu-core` with enough data for testing, and because it allows you to inspect and modify the configuration if needed. Here, we create a directory called `bantu` to use as the persistent volume: `cd $HOME; mkdir bantu`
4. Download and run the bantu Quickstart container, replacing `USER` with your username:

```bash
docker run --rm -it -p "8000:8000" -p "11626:11626" -p "11625:11625" -p"8002:5432" -v $HOME/bantu:/opt/bantu --name bantu bantu/quickstart --testnet
```

You can check out Bantu Core status by browsing to [http://localhost:11626](http://localhost:11626).

You can check out your Expansion instance by browsing to [http://localhost:8000](http://localhost:8000).

You can tail logs within the container to see what's going on behind the scenes:

```bash
docker exec -it bantu /bin/bash
supervisorctl tail -f bantu-core
supervisorctl tail -f expansion stderr
```

On a modern laptop this test setup takes about 15 minutes to synchronise with the last couple of days of testnet ledgers. At that point Expansion will be available for querying.

See the [Quickstart Docker Image](https://github.com/bantu/docker-bantu-core-Expansion) documentation for more details, and alternative ways to run the container.

You can test your Expansion instance with a query like: [http://localhost:8000/transactions?cursor=&limit=10&order=asc](http://localhost:8000/transactions?cursor=&limit=10&order=asc). Use the [bantu Laboratory](https://laboratory.bantu.network/) to craft other queries to try out, and read about the available endpoints and see examples in the [Expansion API reference](../api/introduction/index.md).

