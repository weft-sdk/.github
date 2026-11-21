<h1 align="center">Weft</h1>

<p align="center"><b>One interface for every way services talk.</b></p>

<p align="center">
  <a href="https://github.com/weft-sdk/weft">Repository</a> ·
  <a href="https://github.com/weft-sdk/weft#how-weft-works">How it works</a> ·
  <a href="https://github.com/weft-sdk/weft/tree/main/docs">Documentation</a>
</p>

---

Weft is a thin layer over the communication libraries you already use. Call `weft.http`, `weft.gql`, `weft.grpc`, `weft.ws`, `weft.kafka` and the rest. Weft runs the real library underneath: Express, Apollo, KafkaJS, Socket.io, Spring Kafka, FastAPI and more.

```ts
weft.http.post("/orders", createOrder)          // Express underneath
weft.kafka.publish("order.placed", order)       // KafkaJS underneath
weft.ws.emit("courier.moved", position)         // Socket.io underneath
```

## Write the contract once

Contracts live in small, language-neutral `.weft` files. A Rust compiler turns them into typed code, so the service that sends a message and every service that receives it share the same types.

```weft
type Order {
  id: uuid
  items: OrderItem[]
  total: Money
}

event order.placed: Order
```

## What you get

- **One API** for every transport, in every language.
- **Typed end to end** across languages, from one contract.
- **Your stack stays.** The original client is always one call away.
- **Shared behaviour:** tracing, retries, timeouts and error formats work the same on every transport.
- **Breaking changes caught early** with `weft check`, before you merge.
- **A live map** of which services talk to which, over what.

## Supported

**13 languages:** TypeScript/JavaScript, Go, Python, JVM (Java, Kotlin, Scala), .NET (C#, F#), Rust, Ruby, PHP, Elixir/Erlang, Swift, Dart, plus browser and mobile clients.

**Transports:** HTTP, GraphQL, gRPC, typed RPC, WebSockets, SSE, Kafka, RabbitMQ, NATS, Redis, cloud queues, MQTT and Pulsar.

## Packages

| Registry | Scope |
| --- | --- |
| npm | `@weft-sdk/*` |
| PyPI, RubyGems | `weft-core` |
| crates.io | `weft-sdk` |
| NuGet | `WeftSdk.*` |

---

<p align="center"><sub>© Weft</sub></p>
