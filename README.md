# Yeon Lee — Systems‑minded Software Engineer

> I design and ship typed, deterministic data & messaging systems for markets and real‑time apps.  
> Go/Python • Protobuf • NATS/Kafka • OpenTelemetry • Linux

[![Website](https://img.shields.io/badge/yeonthelee.tech-visit-111?logo=firefox-browser)](https://yeonthelee.tech)
[![GitHub Org](https://img.shields.io/badge/AmpyFin-org-0a0?logo=github)](https://github.com/AmpyFin)
[![Resume](https://img.shields.io/badge/resume-pdf-3949ab)](#-resume--contact)
[![Open Source](https://img.shields.io/badge/open%20source-ampy--proto%2C%20ampy--bus%2C%20ampy--config%2C%20ampy--observability-0b7285)](https://github.com/AmpyFin)

---

## 🧭 What I care about

- **Truthful data**: explicit decimals, currencies, and `event_time` vs `ingest_time` vs `as_of` — no silent coercions.  
- **Determinism**: reproducible replays with **run_id**, **universe_id**, and stable contracts so bugs become events you can explain.  
- **Operational empathy**: p95/p99, backpressure, DLQs, circuit breakers, and an on‑call that sleeps at night.  
- **Community**: open contracts, clean examples, and docs a new teammate can implement from day one.

---

## 🚀 Now shipping

- **AmpyFin foundations (OSS + modular)**  
  *Canonical Protobuf schemas*, a **bus envelope** with trace context, typed config facade, and **observability SDKs** with OTLP exporters.  
  Providers include **DataBento (C++)**, **Benzinga (Go)** for earnings/news, **Tiingo (Go)** for fundamentals, and **yfinance-go** for concurrency‑safe free data.

- **Deterministic ingestion & replays**  
  Golden samples, replay tooling, and CI smoke tests to catch schema evolution & ordering regressions before prod.

- **Infra that tells the truth**  
  JSON logs enriched with span/trace IDs, Prometheus metrics with domain labels, and sampling that respects SLOs.

---

## 🧪 Tiny demo — “contract first”

**bars.v1 (excerpt)**

```proto
message Bar {
  string ticker        = 1;   // "AAPL"
  string currency      = 2;   // "USD"
  int64  event_time_ns = 3;   // exchange event time
  string open          = 4;   // decimal as string
  string high          = 5;
  string low           = 6;
  string close         = 7;
  string volume        = 8;   // bigint as string
}
```

**Publish with Go + NATS (enveloped)**

```go
// go:generate buf build && buf generate
b := &barsv1.Bar{
    Ticker: "AAPL", Currency: "USD",
    EventTimeNs: time.Now().UnixNano(),
    Open: "233.12", High: "235.00", Low: "232.80", Close: "234.90",
    Volume: "1865321",
}
payload, _ := proto.Marshal(b)

env := ampybus.EnvelopeFor("bars.v1", payload,
  ampybus.WithRunID("run_2025_10_11"),
  ampybus.WithUniverseID("us_equities"),
  ampybus.WithTraceContextFrom(ctx),
)

js.Publish("bars.v1", env.Bytes())
```

> Same contract works in Python/C++ because **contracts are the source of truth**, not ad‑hoc structs.

---

## 🧩 Selected projects

| Project | What it is | Why it exists | Links |
|---|---|---|---|
| **ampy‑proto** | Canonical Protobuf schemas (bars, ticks, fundamentals, news, FX, corporate actions, universe, signals, orders, fills, positions, metrics) | Precise, typed interoperability across languages and teams | [repo](https://github.com/AmpyFin/ampy-proto) • `pip install ampy-proto` |
| **ampy‑bus** | Messaging conventions: envelope, headers, QoS tiers, trace IDs, DLQ routing, NATS/Kafka helpers | Deterministic replays, observability, and safe evolution | [repo](https://github.com/AmpyFin/ampy-bus) |
| **ampy‑config** | Typed config & secrets facade (Go & Python) | Remove env‑spaghetti; enable runtime reloads and secret indirection | [repo](https://github.com/AmpyFin/ampy-config) |
| **ampy‑observability** | Logs/metrics/tracing SDKs + docker‑compose stack | Uniform, domain‑aware telemetry with OTLP exporters | [repo](https://github.com/AmpyFin/ampy-observability) |
| **yfinance‑go** | Production‑minded Yahoo Finance client (historicals/quotes/fundamentals) with concurrency & backoff | Free data path that still meets deterministic and typing standards | [repo](https://github.com/AmpyFin/yfinance-go) |
| **tiingo‑go** | Fundamentals & prices via Tiingo (Go) | Validated fundamentals for models and sanity checks | [repo](https://github.com/AmpyFin/tiingo-go) |

---

## 🧱 Tech I reach for

**Core**: Go, Python, C/C++, SQL, Bash  
**Data/Messaging**: Protobuf, Kafka, NATS JetStream  
**Obs/Infra**: OpenTelemetry, Prometheus/Grafana, Docker, Linux  
**Datastores**: PostgreSQL, DuckDB, MongoDB, AWS Neptune  
**Practices**: CI/CD, typed contracts, p95/p99 SLOs, replay‑driven debugging

> I keep badges minimal; signal beats sticker walls. Full list lives in project READMEs.

---

## 🗺️ How I work

1. **Pin the contract** (fields, units, timestamp semantics).  
2. **Make failure boring** (backoffs, DLQ, retries, idempotency, timeouts).  
3. **Instrument early** (logs with context, metrics with labels, trace spans that matter).  
4. **Reproduce before cleverness** (golden samples, deterministic replays).  
5. **Automate the path** (scripts/CI to do the right thing by default).

---

## 🌱 Currently learning / exploring

- Low‑latency ingestion patterns and bounded concurrency in C++/Go.  
- Cleaner currency/decimal semantics across providers.  
- Cataloging market microstructure edge cases as test fixtures.

---

## 🤝 I like collaborating on

- Open contracts and adapters that unblock research/ops teams.  
- Observability that explains “what happened and why” without guesswork.  
- Clean example repos that can be forked and run in <10 minutes.

---

## 📝 Personal site

**→ https://yeonthelee.tech/** — notes, write‑ups, and experiments.

---

## 📫 Resume & contact

- **Email**: yeonholee50@gmail.com  
- **LinkedIn**: https://www.linkedin.com/in/yeon-lee  
- **Resume**: see repo root or message me for a tailored version

> If you’ve read this far: THANK YOU. I build in public. If something looks off, open an issue — I’ll fix it and credit you.

