---
id: elastic-search
title: Elasticsearch
---

## Overview

An Elrond node can enable the indexing within an Elasticsearch instance. Indexed data will serve as historical data source
that can be used as it is for searching purposes or to serve a front-end application.

:::tip
Due to the possible high data volume, it's not recommended to use validators as nodes to index in Elasticsearch from.
Our implementation uses a concept of a queue and makes sure that everything is being processed. Consensus and synchronization mechanisms can have delays because of the indexing.
:::

## Setup

In order to set up an observer that indexes in Elasticsearch, one has to update the `external.toml` file from the node's 
configuration directory. A minimum configuration would have `Enabled` set to `true` and the rest of the fields updated 
accordingly (`URL`, `Username`, `Password`). 

Alternatively, one can choose to use also Kibana for visualizing Elastic Data. Kikana's path must be `_plugin/kibana/api`.

Also, one can specify to only index data for a given set of indexes. The list of indexes enabled is to be found at the 
`EnabledIndexes` section.

### Proxy support

There are some endpoints in elrond-proxy that rely on an Elasticsearch instance. They can be found [here](/sdk-and-tools/proxy#dependency-on-elastic-search).

## Multi-shards

In order to have the history of the entire network, one has to enable elastic indexing for a node in each shard (0, 1, 2 and metachain).
Some features that ensure data validity rely on the fact that a node of each shard indexes in the database. For example, the status
of a cross-shard transaction is decided on the destination shard.

## Elasticsearch cluster system requirements

The Elasticsearch cluster can be installed on multiple machines (we recommend a setup with more nodes in a cluster) or on a single one.

In case of a single machine, our recommendation is as follows:

- 12 x CPU
- 32 GB RAM
- Disk space that can grow up to 3 TB
- 100 Mbit/s always-on Internet connection

## Clone an Elasticsearch cluster

In order to have all the information about the Elrond chain in an Elasticsearch cluster (from genessis to current time) one has to copy all the data with a specific tool from an Elasticsearch cluster to another.
To get more information how to do this use the documentation from this [repository](https://github.com/ElrondNetwork/elrond-tools-go/tree/main/elasticreindexer).

