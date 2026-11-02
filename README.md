# Ethereum Classic public RPC

Public JSON-RPC endpoints for Ethereum Classic and its Mordor test network, being
stood up as an extension of the public goods the network already starts from: a
load-balancing gateway in front of the bootnodes
[Core-Geth](https://github.com/ethereumclassic/core-geth) ships. The gateway's
configuration and its admission list belong in this repository, so that more than one
maintainer can rebuild or move the service and anyone can read how it is run. This
work is maintained in the [`ethereumclassic`](https://github.com/ethereumclassic)
GitHub organization by Ethereum Classic's core developers and open community
contributions.

> [!IMPORTANT]
> **Until these endpoints answer, use ChainList.** It lists the public endpoints
> operators publish for [Ethereum Classic](https://chainlist.org/chain/61) and
> [Mordor](https://chainlist.org/chain/63). The ETC Cooperative is winding down, and
> the services it maintained are moving to the `ethereumclassic` GitHub organization:
> the Core-Geth client, the peer discovery lists, the bootnodes and public JSON-RPC.
> These endpoints are being stood up to replace the ones that depended on the
> Cooperative, such as `etc.rivet.link`, which went offline in late August 2026, and
> `rpc.mordor.etccooperative.org`, on the Cooperative's own domain. Before you move a
> node, a pool or an application to a new source of software or data, confirm which
> organization publishes it.
> [The ETC Cooperative transition](https://docs.coregeth.com/etc-cooperative-transition/#public-json-rpc)
> says when this recommendation changes, and lists where the Cooperative's other
> services continue.

## The endpoints

| Network | Chain ID | Endpoint |
|---|---|---|
| Ethereum Classic | 61 | `https://rpc.ethereumclassic.net` |
| Mordor | 63 | `https://rpc-mordor.ethereumclassic.net` |

**They extend the public goods already maintained here.** The
[bootnodes](https://docs.coregeth.com/guides/bootnodes-and-discovery/) the Core-Geth
`v1.13` line ships are run by its maintainers, new nodes bootstrap through them, and
they seed the crawl behind the
[peer discovery lists](https://github.com/ethereumclassic/discv4-dns-lists). The
gateway is to sit in front of those same nodes and balance requests across them, so
that public traffic reaches them through its rate limits and never directly. How the
hosts are deployed belongs in
[`ethereumclassic/nodes`](https://github.com/ethereumclassic/nodes).

**They are run from this organization on purpose.** An endpoint a wallet, an explorer
or a payment processor depends on should not disappear because one company's contract
ended, which is what happened to `etc.rivet.link`. Only endpoints inside the
`ethereumclassic` public-good framework are admitted, and the admission list is
committed here as they are, where anyone can check it.

## Quick start

Once an endpoint answers, point a wallet or an application at it with the chain ID
above. To check one from a terminal:

```sh
curl -s -X POST -H 'Content-Type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}' \
  https://rpc.ethereumclassic.net
```

The result is `"0x3d"` on Ethereum Classic and `"0x3f"` on Mordor.

### Run your own node

**A public endpoint is someone else's node.** It sees every request you send it, and
it can rate limit you, fall behind or stop. Anything you depend on should run against
a node you control. These endpoints are being stood up for anyone to use, and a wallet
product can use them too, but it should run its own node, so that the product's
reliability stays in its own hands. Every product that does also lightens the load on
these public goods.

**If you want to run your own, here is how.** Running `geth` is running a complete
Ethereum Classic node: it finds peers, syncs the chain, validates every block it
receives, and serves the result to whatever you point at it. Run the `v1.13` line:
[Downloads](https://coregeth.com/downloads/) has the archive for every platform with
its checksum beside it, and the commands to install and start it. Then start with the
page for what you run.

| You are | Start with |
|---|---|
| Running a node for yourself or a wallet | [Installation](https://docs.coregeth.com/getting-started/installation/), then [Running a node](https://docs.coregeth.com/getting-started/run-a-node/) |
| An exchange or custodian | [Production operations](https://docs.coregeth.com/guides/production-operations/) |
| A solo miner | [Mining](https://docs.coregeth.com/guides/mining/) |
| A mining pool operator | [Mining pool node](https://docs.coregeth.com/guides/mining-pool-node/) |
| An RPC provider | [Public RPC endpoint](https://docs.coregeth.com/guides/public-rpc-endpoint/) |
| Building a wallet or another application on Ethereum Classic | [Endpoints for your own project](https://docs.coregeth.com/guides/developer-endpoints/), then [Public RPC endpoint](https://docs.coregeth.com/guides/public-rpc-endpoint/) if your users reach the node directly |
| An explorer, indexer or analytics service | [Archive node](https://docs.coregeth.com/guides/archive-node/) |
| Testing on Mordor | [Run a Mordor node](https://docs.coregeth.com/getting-started/run-mordor-node/) |

[Choose your role](https://docs.coregeth.com/guides/) has every role, including private
networks and building the client. The Ethereum Classic Core Developers run a
[Discord](https://coregeth.com/discord) for questions about running a node, an upgrade,
or anything in the documentation.

> [!WARNING]
> **Every node still on a `v1.12` release should move to the `v1.13` line.** Your chain
> data carries over, and the upgrade costs about twenty minutes of downtime.
> [Downloads](https://coregeth.com/downloads/) has the commands and checksums, and the
> [migration guide](https://docs.coregeth.com/tutorials/v1.13.0-migration/) has a path
> for each platform. [Node operators: start here](https://docs.coregeth.com/operators/)
> has the steps an upgrade cannot do for you: rotating the P2P node key, required if
> your node ran the `v1.12` line; tracking releases at `ethereumclassic/core-geth`,
> since anything still watching `etclabscore/core-geth` will not see a new release; and
> deciding the MESS setting. [Security](https://coregeth.com/security/) has what the
> network is running, and every audit.

## Documentation

| Page | What it covers |
|---|---|
| [The ETC Cooperative transition](https://docs.coregeth.com/etc-cooperative-transition/#public-json-rpc) | What these endpoints replace, and why they are run from this organization |
| [Node operators: start here](https://docs.coregeth.com/operators/) | The short path for node, pool, exchange and RPC operators: what to do now, and what to read in what order |
| [Migration guide](https://docs.coregeth.com/tutorials/v1.13.0-migration/) | What changes on upgrade from `v1.12`, per platform, and the steps a node needs |
| [Choose your role](https://docs.coregeth.com/guides/) | The starting page for each kind of node, from a personal node to a mining pool |
| [Public RPC endpoint](https://docs.coregeth.com/guides/public-rpc-endpoint/) | Serving JSON-RPC from your own node, and what has to sit in front of it |
| [Bootnodes and peer discovery](https://docs.coregeth.com/guides/bootnodes-and-discovery/) | How a node finds its first peers, and how the peer discovery lists are built |
| [Support this work](docs/support.md) | Who maintains and funds these endpoints, and how to sponsor them |

## Status

The endpoints are being stood up, and the gateway configuration and admission list
land in this repository as they are. Until the endpoints answer, ChainList is the
recommendation. This section and
[the transition page](https://docs.coregeth.com/etc-cooperative-transition/#public-json-rpc)
say so when that changes.

## Security

**To report a security issue privately**, email <security@ethereumclassic.net>.
[`SECURITY.md`](SECURITY.md) has the details. Security issues are never reported
as public issues.

## Support this work

These endpoints are a public good. The work is done in the `ethereumclassic` GitHub
organization by Ethereum Classic's core developers and open community contributions,
together with the [Ethereum Classic DAO](https://ethereumclassicdao.org), the standing
legal entity that maintains and funds it as the funder of last resort. The repositories
stay in that organization no matter who maintains or funds them. Earlier, the work
passed from one organization to the next as each closed or left: ETCDEV, ETC Labs and
the ETC Cooperative. With the ETC Cooperative's dissolution, Ethereum Classic
stakeholders such as mining pools, exchanges and service providers should use
<security@ethereumclassic.net> as their point of contact.

If you are a stakeholder of Ethereum Classic, you rely on this infrastructure. Ethereum
Classic has no protocol-layer funding mechanism for its critical infrastructure or its
core developers, so no part of the network's fee or issuance revenue pays for this
work. A funder of last resort keeps the work alive. It does not make the work
sustainable, and what the work needs is steady funding from the operations that depend
on it. Please consider sponsoring it. [Support this work](docs/support.md) lists who
has funded it, explains how sponsors are credited, and gives the routes: an invoiced
maintenance agreement for organizations, or a direct transfer to an address provided on
request.

## License

Not settled yet. This repository's license follows what its source dependencies
require, and no `LICENSE` file is in the tree until they are known.
