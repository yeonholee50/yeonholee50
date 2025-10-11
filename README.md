<div align="center">

# Yeon Lee
<sub>systems-minded software engineer · early in my career · learning in public</sub>

<a href="https://yeonthelee.tech"><kbd>site</kbd></a> ·
<a href="https://www.ampyfin.com"><kbd>ampyfin</kbd></a> ·
<a href="https://github.com/AmpyFin"><kbd>@AmpyFin</kbd></a> ·
<a href="mailto:yeonholee50@gmail.com"><kbd>email</kbd></a>

<br/>

<a href="#projects"><kbd>#contracts-first</kbd></a>
<a href="#how-i-work"><kbd>#deterministic-replays</kbd></a>
<a href="#projects"><kbd>#observability</kbd></a>
<a href="#projects"><kbd>#typed-config</kbd></a>
<a href="#ampyfin-notes"><kbd>#learn-in-public</kbd></a>

</div>

> *I'm not afraid of being left behind—I'm excited about what I can build with the emerging technologies of tomorrow.*


## Projects
- **AmpyFin (first OSS Python version)** — the seed that became today’s modular platform. <a href="https://github.com/AmpyFin">org</a> · <a href="https://www.ampyfin.com">site</a>
- **ampy-proto** — canonical market schemas (bars/ticks/fundamentals/news/fx/corporate_actions/universe/signals/orders/fills/positions/metrics). <a href="https://github.com/AmpyFin/ampy-proto">repo</a>
- **ampy-bus** — envelope + headers, QoS tiers, DLQ, NATS/Kafka helpers, trace propagation. <a href="https://github.com/AmpyFin/ampy-bus">repo</a>
- **ampy-config** — typed config & secrets façade (Go/Python), with runtime reloads and secret indirection. <a href="https://github.com/AmpyFin/ampy-config">repo</a>
- **ampy-observability** — logs/metrics/tracing (OTLP) and a docker-compose stack for local. <a href="https://github.com/AmpyFin/ampy-observability">repo</a>
- **yfinance-go** — concurrency-safe free-data client + CLI (`yfin pull`) with session rotation and circuit breakers. <a href="https://github.com/AmpyFin/yfinance-go">repo</a>

---

## How I work
I research the problem with stakeholders and end users, then whiteboard the one-line goal, non-goals, and the invariants that must hold.  
I pin **contracts before code** (explicit units/decimals; `event_time` / `ingest_time` / `as_of`) with concrete examples.  
I design for **boring failure** (timeouts, jittered retries, circuit breakers, DLQ, kill-switch), and ship **small, reversible changes** (shadow first, flag-gated release, scripted rollback).  
**Observability is day-0** (structured logs with trace context, labeled metrics, purposeful spans).  
Confidence is **replay-driven** (golden fixtures; deterministic replays; CI guards).  
I communicate **the why**, keep runbooks short, and write down what I learn.

---

## Toolbox
Go · Python · C/C++ · SQL · Protobuf · NATS JetStream/Kafka · OpenTelemetry/Prometheus/Grafana · Docker/Linux · PostgreSQL/DuckDB/MongoDB

---

## Say hi
<a href="mailto:yeonholee50@gmail.com"><kbd>email</kbd></a> · <a href="https://www.linkedin.com/in/yeon-lee"><kbd>linkedin</kbd></a> · <a href="https://yeonthelee.tech"><kbd>site</kbd></a> · <a href="https://www.ampyfin.com"><kbd>ampyfin</kbd></a>


