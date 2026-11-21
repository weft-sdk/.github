<div align="center">

<img src="https://raw.githubusercontent.com/weft-sdk/.github/main/profile/logo.svg" alt="Weft" width="72" height="72">

# Weft

**One interface for every way services talk.**

HTTP · GraphQL · gRPC · WebSockets · Kafka · RabbitMQ · NATS · Redis · MQTT · and more,<br>
through one API, in 13 languages.

[Repository](https://github.com/weft-sdk/weft) ·
[Docs](https://github.com/weft-sdk/weft/tree/main/docs) ·
[Languages](https://github.com/weft-sdk/weft/blob/main/docs/languages.md) ·
[Contract language](https://github.com/weft-sdk/weft/blob/main/docs/contract-language.md)

</div>

<br>

```ts
weft.http.post("/orders", createOrder)      // Express underneath
weft.kafka.publish("order.placed", order)   // KafkaJS underneath
weft.ws.emit("courier.moved", position)     // Socket.io underneath
```

Weft runs the real library under every call, so your stack stays. Contracts are written once in language-neutral `.weft` files, and a Rust compiler generates typed code for each language.

<br>

## Repositories

| | |
| --- | --- |
| [**weft**](https://github.com/weft-sdk/weft) | The compiler, the SDKs for every language, the CLI, the dashboard and the docs |

<br>

## Packages

| Registry | Name |
| --- | --- |
| npm | `@weft-sdk/*` |
| PyPI · RubyGems | `weft-core` |
| crates.io | `weft-sdk` |
| NuGet | `WeftSdk.*` |

<br>

<div align="center"><sub>TypeScript · Go · Python · JVM · .NET · Rust · Ruby · PHP · Elixir · Swift · Dart</sub></div>
