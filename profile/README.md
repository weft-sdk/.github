<div align="center">

<img src="https://raw.githubusercontent.com/weft-sdk/.github/main/profile/logo.svg" alt="Weft" width="88" height="88">

# Weft

**One interface for every way services talk.**

Write your contracts once. Call `weft.http`, `weft.kafka` and the rest.<br>
Weft runs the real library underneath: Express, KafkaJS, net/http, franz-go.

<br>

[![npm](https://img.shields.io/npm/v/@weft-sdk/core?label=%40weft-sdk%2Fcore&labelColor=111111&color=7d92ff)](https://www.npmjs.com/org/weft-sdk)
[![Go module](https://img.shields.io/github/v/tag/weft-sdk/weft?filter=go%2Fv*&label=go%20module&labelColor=111111&color=7d92ff)](https://pkg.go.dev/github.com/weft-sdk/weft/go)
[![CI](https://img.shields.io/github/actions/workflow/status/weft-sdk/weft/conformance.yml?branch=main&label=conformance&labelColor=111111&color=7d92ff)](https://github.com/weft-sdk/weft/actions)
[![License](https://img.shields.io/github/license/weft-sdk/weft?labelColor=111111&color=7d92ff)](https://github.com/weft-sdk/weft/blob/main/LICENSE)

[**Repository**](https://github.com/weft-sdk/weft) &nbsp;·&nbsp;
[**Docs**](https://github.com/weft-sdk/weft/tree/main/docs) &nbsp;·&nbsp;
[**Contract language**](https://github.com/weft-sdk/weft/blob/main/docs/02-contract-language.md) &nbsp;·&nbsp;
[**Roadmap**](https://github.com/weft-sdk/weft/blob/main/docs/12-roadmap.md)

</div>

<br>

## What it looks like

A contract is a small language-neutral file. You write it once.

```weft
package orders @version("1.0.0")

type Order {
  id: uuid
  items: OrderItem[]
  total: Money
}

event order.placed: Order { key: id }

http /v1 {
  POST "/orders"      createOrder(body: CreateOrder) -> Order | OutOfStock
  GET  "/orders/{id}" getOrder(id: uuid) -> Order?
}
```

`weft gen` turns it into typed code. Then you call `weft.*`, and every route, event name and payload is checked by the compiler.

```ts
import { weft } from "./weft.gen"

weft.http.post("/orders", ({ body }) => placeOrder(body))      // body is a CreateOrder
weft.kafka.on("order.placed", (order) => notifyCustomer(order)) // order is an Order

await weft.kafka.publish("order.placed", order)                 // a wrong payload does not compile
await weft.start()                                              // and weft.stop() shuts down cleanly
```

The same contract gives a Go service the same types, so a Go service and a TypeScript service read each other's messages. A conformance suite checks that on every change, with a real Kafka broker.

<br>

## Get started

```sh
# the CLI
cargo install --git https://github.com/weft-sdk/weft weft-cli --locked

# in your project: pick your transports, write weft.yaml, install the packages, generate the code
weft init
```

`weft init` detects TypeScript (`package.json`) or Go (`go.mod`), installs the packages with your package manager, writes an example contract, and runs `weft gen`.

<br>

## What you get

| Feature | What it means |
| --- | --- |
| **One API** | `weft.http`, `weft.kafka` and the rest work the same way, in every language |
| **Typed end to end** | The sender and every receiver share the generated types |
| **Your stack stays** | The real library runs underneath, and `weft.http.raw` hands you the Express app or the Kafka client |
| **Behaviour that matches** | Validation, retries, dead letters, timeouts, error format and OpenTelemetry traces work the same on every transport |
| **Breaking changes caught** | `weft check` compares your contracts with the last release and says what would break |
| **Generated code you can read** | One file, in your language's own style, checked into your repo |

<br>

## What works with what

| | TypeScript | Go |
| --- | :---: | :---: |
| `weft.http` | Express | net/http |
| `weft.kafka` | KafkaJS | franz-go |
| `weft gen`, `weft init`, `weft check` | ✓ | ✓ |
| `weft.gql` · `weft.grpc` · `weft.rpc` · `weft.ws` · `weft.sse` · `weft.mq` · `weft.nats` · `weft.redis` · `weft.cloud` · `weft.mqtt` · `weft.pulsar` | | |

The contract language already describes all thirteen transports. The libraries behind them, and the packages for Python, JVM, .NET, Rust, Ruby, PHP, Elixir, Swift and Dart, follow the [roadmap](https://github.com/weft-sdk/weft/blob/main/docs/12-roadmap.md).

<br>

## Packages

| Where | Package |
| --- | --- |
| npm | [`@weft-sdk/core`](https://www.npmjs.com/package/@weft-sdk/core) · [`@weft-sdk/http-express`](https://www.npmjs.com/package/@weft-sdk/http-express) · [`@weft-sdk/kafka-kafkajs`](https://www.npmjs.com/package/@weft-sdk/kafka-kafkajs) |
| Go | `go get github.com/weft-sdk/weft/go` |
| CLI | `cargo install --git https://github.com/weft-sdk/weft weft-cli` |

<br>

## Repositories

| Repository | What is in it |
| --- | --- |
| [**weft**](https://github.com/weft-sdk/weft) | The compiler and CLI, the TypeScript and Go packages, the conformance suite, the website and the docs |

<br>

<div align="center"><sub>Apache-2.0 &nbsp;·&nbsp; Contracts in, typed code out.</sub></div>
