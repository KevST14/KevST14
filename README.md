## Hi, I'm Kevin 👋

I'm a Computer Science grad from Newcastle, and most of what I build ends up being about money: ledgers, fraud detection, pricing models and prediction markets.

- 🔨 **Now:** building [Clearhouse](https://github.com/KevST14/clearhouse), a small bank back office for experimenting with fraud detection
- 🎓 **Bsc Dissertation:** a layered safety architecture that stops AI agents from making payments they shouldn't
- 🔍 **Looking for:** graduate software engineering and data roles
- 📫 **Reach me:** [LinkedIn](https://www.linkedin.com/in/kevin-steepan/) · [ksteepan14@icloud.com](mailto:ksteepan14@icloud.com)

### Projects

| Project | What it does | Built with |
|---|---|---|
| [**Clearhouse**](https://github.com/KevST14/clearhouse) | A double-entry ledger that streams every transfer to Redpanda, plus a traffic generator that can set off card testing, money mule rings and account takeovers | Java, Spring Boot, PostgreSQL, Redpanda, React |
| [**Rent Reality Check**](https://github.com/KevST14/london-rent-reality-check) · [demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app) | Predicts a fair nightly price for a London Airbnb and explains it with SHAP. R² 0.72 on areas it never saw in training | Python, scikit-learn, Streamlit |
| [**Split Decision**](https://github.com/KevST14/SplitDecision) | Tracks Polymarket odds, flags big swings and scores your own forecasts against what actually happened | Python, FastAPI, React, SQLite |

### Things I learned the hard way

- **Retries can charge you twice.** Every Clearhouse payment carries an idempotency key, and a test sends the same request 20 times from 8 threads to check that only one goes through.
- **Optimistic locking struggles on busy accounts.** It kept failing under load, so I switched to pessimistic locks taken in a fixed order.
- **Your laptop isn't CI.** GitHub Actions on Linux caught a nanosecond vs microsecond timestamp bug that never showed up on my Mac.
- **Location beats copywriting.** For Airbnb prices, distance to stations and parks mattered far more than how the listing was written, which was worth about £1–2 a night.

### Stack

- **Languages:** Python, Java, TypeScript, JavaScript
- **Backend:** Spring Boot, FastAPI, PostgreSQL, SQLite, Kafka/Redpanda, Docker
- **Frontend:** React, Next.js, Tailwind
- **ML:** scikit-learn, SHAP, Streamlit
