*I like working with people who share the goal but think differently — that’s how innovation thrives.*  
**Motto:** *I'm not afraid of being left behind—I'm excited about what I can build with the emerging technologies of tomorrow. Every new framework, every breakthrough, every innovation is an opportunity to create something that didn't exist yesterday and solve problems we haven't even discovered yet.*

**Site:** https://yeonthelee.tech · **Org:** https://github.com/AmpyFin · **AmpyFin site:** https://www.ampyfin.com

---

## Proof over promises
- Reworked vendor data flow with drift/orphan checks → **bad‑data incidents ↓ >86%**; **same‑day updates** across ~20k SKUs/week.
- Built a tree‑based compatibility engine on AWS Neptune → **multi‑day test matrix → < 1 hour**.
- Standardized **run_id / universe_id / trace context** → deterministic replays that catch ordering bugs **before prod**.

---

## What I’m building
- **ampy‑proto** — canonical market schemas (bars/ticks/fundamentals/news/fx/corp_actions/universe/signals/orders/fills/positions/metrics).  
  `pip install ampy-proto` · https://github.com/AmpyFin/ampy-proto
- **ampy‑bus** — deterministic messaging: envelope, headers, QoS tiers, DLQ, NATS/Kafka helpers, trace propagation.  
  https://github.com/AmpyFin/ampy-bus
- **ampy‑config** — typed config & secrets facade (Go/Python), runtime reloads, secret indirection.  
  https://github.com/AmpyFin/ampy-config
- **ampy‑observability** — JSON logs + Prometheus metrics + OTLP tracing; docker‑compose stack for local.  
  https://github.com/AmpyFin/ampy-observability
- **AmpyFin (first OSS Python version)** — earliest open‑source Python repo that seeded today’s modular platform.  
  https://github.com/AmpyFin
- **yfinance‑go** — free‑data client with bounded concurrency, session rotation, circuit breakers; **library + CLI (`yfin pull`)**.  
  https://github.com/AmpyFin/yfinance-go
- **tiingo‑go** — normalized fundamentals & prices (Go) with safe decimals & time semantics. *(private — link omitted)*

---

## How I work (short list)
1) **Pin the contract** (fields, units, time semantics).  
2) **Make failure boring** (timeouts, retries, backoff, idempotency, DLQ).  
3) **Instrument day 0** (structured logs, labeled metrics, purposeful spans).  
4) **Reproduce before clever** (golden samples, deterministic replays).  
5) **Write it down** so the next person ships faster.

---

## Tech I reach for
Go • Python • C/C++ • SQL · Protobuf · NATS JetStream/Kafka · OpenTelemetry/Prometheus/Grafana · Docker/Linux · PostgreSQL/DuckDB/MongoDB

**Say hi:** yeonholee50@gmail.com · https://www.linkedin.com/in/yeon-lee

