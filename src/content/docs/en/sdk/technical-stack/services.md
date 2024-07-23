---
section: sdk
date: Last Modified
title: "Scroll SDK Services"
lang: "en"
permalink: "sdk/technical-stack/services"
excerpt: "The various components running to support the Scroll SDK."
---

## Overview

Scroll SDK is composed of various services that work together to create a functional rollup. This article provides an overview of these services, their roles, and how they contribute to the overall architecture of Scroll SDK.

We'll start by listing the services required for a minimal deployment, followed by a detailed description of each service. This information will help you understand the components of Scroll SDK and make informed decisions about which services to enable or disable based on your specific needs.

This covers the full list of items in [values.yaml](https://github.com/scroll-tech/scroll-stack/blob/develop/charts/scroll-stack/values.yaml), which allows for enabling or disabling of specific services. New to Scroll’s Architecture? Check out [this article](/en/technology/chain/rollup/) for more info.

## Helm & Kubernetes

TODO: Here we describe the project setup, where configuration files are for each service, mention that they're auto-generated by the docker image mentioned in [Configuration](/en/sdk/technical-stack/configuration), and maybe a nice diagram showing how they relate to one another.

### Ingress DNS

The following services have ingresses setup by default, along with DNS names that make them accessible in local deployments if yours `etc/hosts` file is appropriately configured:

TODO: LIST THESE

## Minimal Deployment

| Service                 | Enabled |
| ----------------------- | ------- |
| l1-devnet               | ✅      |
| blockscout              | ✅      |
| bridge-history-api      | ✅      |
| bridge-history-fetcher  | ✅      |
| balance-checker         |         |
| chain-monitor           |         |
| contracts               | ✅      |
| coordinator-api         |         |
| coordinator-cron        |         |
| event-watcher           | ✅      |
| frontends               | ✅      |
| gas-oracle              | ✅      |
| grafana                 | ✅      |
| rollup-explorer-backend |         |
| rollup-node             | ✅      |
| l1-explorer             | ✅      |
| l2-sequencer            | ✅      |
| l2-rpc                  | ✅      |
| l2-bootnode             | ✅      |
| loki-stack              | ✅      |
| blockscout-sc-verifier  |         |
| rpc-gateway             | ✅      |
| postgresql              | ✅      |
| kube-prometheus-stack   | ✅      |

## Services Overview

#### Anvil (`l1-devnet`)

Anvil serves as the default local base chain for devnet deployments. It provides a simulated Ethereum environment for testing and development purposes.

#### Blockscout (`blockscout`)

Blockscout is a Block Explorer with an Indexer and WebUI configured specifically for the Scroll SDK chain. It allows users to view and interact with blockchain data in a user-friendly interface.

#### Bridge History API (`bridge-history-api`)

The Bridge History API is used by frontends for reporting a user's bridging history and generating withdrawal proofs for L2 → L1 bridge claims. It provides essential functionality for cross-chain operations.

#### Bridge History Fetcher (`bridge-history-fetcher`)

The Bridge History Fetcher is an indexer that continuously collects all user bridging transactions. It ensures that bridging data is up-to-date and readily available.

#### Balance Checker (`balance-checker`)

The Balance Checker is a simple service to track and monitor the balances of some operator accounts and contracts, such as fee vaults and commit senders.

#### Chain Monitor (`chain-monitor`)

The Chain Monitor is a security service that short-circuits batch finalization if certain invariants are not satisfied. While optional, it is recommended for enhanced security.

#### Contracts (`contracts`)

The Contracts service contains scripts to deploy necessary chain contracts (rollup and bridge) on both L1 and L2. It ensures that the required smart contracts are in place for the Scroll SDK to function properly.

#### Coordinator API (`coordinator-api`)

The Coordinator API allows Provers to register as being open for work and manages scheduling and storage of proofs. It requires significant RAM to run and is disabled by default.

#### Coordinator Cron (`coordinator-cron`)

The Coordinator Cron is a background job that monitors proving tasks for timeout and marks batches (aggregation tasks) as ready once all sub-proofs are ready.

#### Event Watcher (`event-watcher`)

The Event Watcher is an Indexer that monitors rollup events on L1. It keeps track of important events occurring on the base layer.

#### Frontends (`frontends`)

Frontends provide generic Web UIs for the Rollup Explorer, Bridge, and basic chain links for setting up your wallet. They offer user-friendly interfaces for interacting with the Scroll SDK.

#### Gas Oracle (`gas-oracle`)

The Gas Oracle is a backend service that relays up-to-date fee information between L1 and L2 by updating the gas oracle contract on both layers. It helps maintain accurate gas pricing across the network.

#### Grafana (`grafana`)

Grafana provides a Web UI for viewing metrics dashboards. It allows for visual monitoring and analysis of various system metrics.

#### Rollup Explorer Backend (`rollup-explorer-backend`)

The Rollup Explorer Backend is a service under testing and not recommended for use at this time.

#### Rollup Node (`rollup-node`)

The Rollup Node is a core component of the Scroll SDK architecture. It plays a crucial role in managing the rollup process.

#### L1 Explorer (`l1-explorer`)

The L1 Explorer provides a block explorer interface for the L1 devnet. It allows users to inspect transactions and blocks on the base layer.

#### L2 Sequencer (`l2-sequencer`)

The L2 Sequencer is responsible for producing blocks using Clique Proof of Authority (PoA) consensus. It maintains the order of transactions on the L2 chain.

#### L2 RPC (`l2-rpc`)

The L2 RPC node is set up to be exposed to external RPC API consumers. It allows interaction with the L2 chain through standard Ethereum JSON-RPC calls.

#### L2 Bootnode (`l2-bootnode`)

The L2 Bootnode is a dedicated node that helps synchronize additional follower nodes. It facilitates network discovery and connectivity.

#### Loki Stack (`loki-stack`)

The Loki Stack is a log aggregation system. It collects and manages logs from various services within the Scroll SDK ecosystem.

#### Blockscout Smart Contract Verifier (`blockscout-sc-verifier`)

The Blockscout Smart Contract Verifier is a service used by Blockscout for verifying that smart contract source code matches deployed bytecode. It is currently unsupported.

#### RPC Gateway (`rpc-gateway`)

The RPC Gateway is a simple RPC load balancer that distributes requests among multiple L2 geth RPC nodes. It helps manage incoming RPC traffic efficiently.

#### PostgreSQL Database (`postgresql`)

The PostgreSQL Database is used across services to coordinate data and tools. It provides a reliable and scalable database solution for the Scroll SDK.

#### Kube Prometheus Stack (`kube-prometheus-stack`)

The Kube Prometheus Stack is a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator. It provides comprehensive monitoring and alerting capabilities for the Kubernetes cluster running the Scroll SDK.

#### Database Configuration (`db`)

Allows configurations for a DB outside of the default postgres service included in the stack. This provides flexibility in database setup and management for various services within the Scroll SDK ecosystem.