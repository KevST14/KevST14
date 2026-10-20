<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=24&duration=3500&pause=1200&color=3B82F6&center=true&vCenter=true&width=700&lines=Hi%2C+I'm+Kevin+%F0%9F%91%8B;CS+grad+from+Newcastle;Building+payment+and+fraud+systems;Interested+in+fintech+and+AI+safety" alt="Hi, I'm Kevin. CS grad from Newcastle. Building payment and fraud systems. Interested in fintech and AI safety." />

**SWE/DA enthusiast · Newcastle University CS grad · Fintech, fraud and AI safety · Interested in ML/AI **

<a href="https://www.linkedin.com/in/kevin-steepan/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:ksteepan14@icloud.com"><img src="https://img.shields.io/badge/Email-333333?style=for-the-badge&logo=icloud&logoColor=white" alt="Email"></a>
<a href="https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app"><img src="https://img.shields.io/badge/Try_my_live_demo-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Live demo"></a>

</div>

---

I'm Kevin, a Computer Science grad from Newcastle. Most of my projects end up being about money in some way: a small bank ledger, an Airbnb price model, a tool for tracking prediction markets. My dissertation was on how to stop AI agents from making payments they shouldn't.

Right now I'm mostly working on Clearhouse (below).

## Quick quiz

A few questions that came up while building these. Have a guess before opening the answer.

<details>
<summary><b>Q1.</b> I say a market has a 70% chance of YES and it resolves NO. What's my Brier score? (lower is better)</summary>
<br>

**0.49.** Brier score is (forecast − outcome)², so (0.7 − 0)² = 0.49.
If I'd said 50% I'd have scored 0.25, and 10% would have scored 0.01. [Split Decision](https://github.com/KevST14/SplitDecision) works this out for your own guesses over time.
</details>

<details>
<summary><b>Q2.</b> You tap "pay", lose signal, and the app sends the request again. How many times should you be charged?</summary>
<br>

**Once.** Each payment has an *idempotency key*, so a retry gets back the original transfer instead of creating a new one. In [Clearhouse](https://github.com/KevST14/clearhouse) I test this by sending the same request 20 times from 8 threads at once. Only one goes through.
</details>

<details>
<summary><b>Q3.</b> When pricing a London Airbnb, what helps the model more: <i>where</i> it is, or <i>how the listing is written</i>?</summary>
<br>

**Where it is.** Adding location features (distance to stations, parks and places to eat) took R² from 0.62 to 0.65. The listing text was only worth about £1–2 a night. You can try it in the [live demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app).
</details>

<details>
<summary><b>Q4.</b> An AI agent is 60% sure a payment is legit. Should it send the money?</summary>
<br>

**Not by itself.** This is what my dissertation was about. The agent's action goes through several separate checks, and if it isn't confident enough, a human makes the call instead. There's a diagram further down.
</details>

## Projects

<details open>
<summary><h3>Clearhouse</h3></summary>

![Java](https://img.shields.io/badge/Java_21-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redpanda](https://img.shields.io/badge/Redpanda_(Kafka)-E4405F?style=flat-square&logo=apachekafka&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

A small version of a bank's back office that I'm building to learn how payments actually work. There's a double-entry ledger (amounts stored in pence, idempotency keys, row locking), and every transfer gets published to Redpanda through a transactional outbox. A traffic generator simulates 120 customers and 22 shops spending money, and you can trigger fraud on top of that: card testing, a money mule ring, or an account takeover. Each one shows up as a different pattern in the dashboard.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevST14/clearhouse/main/docs/dashboard-dark.png">
  <img alt="Clearhouse dashboard showing three fraud attacks in the money-flow network" src="https://raw.githubusercontent.com/KevST14/clearhouse/main/docs/dashboard-light.png">
</picture>

```mermaid
flowchart LR
    G[Traffic generator] -->|pay + idempotency key| L[Ledger · Spring Boot]
    L -->|debit, credit + event<br/>in one transaction| P[(Postgres)]
    L -->|outbox publisher| R[[Redpanda]]
    G -->|true label| K[(Answer key)]
    G -->|live stream| D[Dashboard]
    R -.->|next| A[AI fraud analyst]
    K -.->|scored against| A
```

- After every test, each transfer has to net to zero and each currency has to sum to zero. The tests run against a real Postgres using Testcontainers, not a mock.
- Optimistic locking kept failing on busy accounts in an 8-thread test, so I switched to pessimistic locks taken in a fixed order. CI on Linux also caught a timestamp bug (nanoseconds vs microseconds) that never showed up on my Mac.
- Next I'm adding a dbt/DuckDB pipeline over the event stream, then an AI fraud analyst that gets scored on precision and recall against the generator's answer key.

**[View repo](https://github.com/KevST14/clearhouse)**
</details>

<details>
<summary><h3>Split Decision</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

Pulls prices from Polymarket on a schedule, stores snapshots in SQLite and flags markets where the odds move a lot. You can also enter your own probability before seeing the market price, and once the market resolves you get a Brier score, so you can see whether you'd have beaten it.

```mermaid
flowchart LR
    A[Polymarket API] -->|polled by APScheduler| B[(SQLite snapshots)]
    B --> C[Swing alerts]
    B --> D[Correlation across markets]
    E[Your blind guess] --> F[Brier score vs outcome]
    B --> F
```

**[View repo](https://github.com/KevST14/SplitDecision)**
</details>

<details>
<summary><h3>Rent Reality Check</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![SHAP](https://img.shields.io/badge/SHAP-explainable_AI-555555?style=flat-square)

Predicts a fair nightly price for a London Airbnb listing using Inside Airbnb and OpenStreetMap data, and uses SHAP to show which features pushed the price up or down. I used spatial cross-validation so the model is always tested on areas it hasn't seen. Without that it can memorise neighbourhoods and look better than it really is.

Results on held-out areas:

| R² | Median error | Mean error |
|:---:|:---:|:---:|
| **0.72** | **22%** | **~£60/night** |

**[Try the live demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app)** · **[View repo](https://github.com/KevST14/london-rent-reality-check)**
</details>

<details>
<summary><h3>Patch Notes</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

A news dashboard I built for myself. It pulls stories from Hacker News, Lobsters, GitHub and about a dozen news sites, then groups articles about the same story into one card. The grouping uses TF-IDF similarity on headlines with extra weight on names, so three outlets covering one earnings call get merged but two unrelated "critical flaw" stories don't.

![Patch Notes today view](https://raw.githubusercontent.com/KevST14/patchnotes/main/docs/today.jpg)

It also learns from what I keep, skip and save, and shows the reason each story is in my feed. There's a trending section for terms that suddenly appear across more than one source, compared against each source's normal baseline so a fresh install doesn't flag everything. I added a swipe-through catch-up mode and a weekly headline quiz too, mostly because they were fun to build. No sign-up, no API keys and no tracking.

**[View repo](https://github.com/KevST14/patchnotes)**
</details>

<details>
<summary><h3>SpendSync</h3></summary>

![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)

A personal finance app for tracking income and spending, with category budgets, savings goals and recurring transactions. Built on Next.js and Prisma, with Zod validating everything that comes into the REST API.

**[View repo](https://github.com/KevST14/SpendSync)**
</details>

<details>
<summary><h3>Dissertation</h3></summary>

*Design and Evaluation of a Layered Safety Architecture for Autonomous Financial Execution Agents* (2026)

```mermaid
flowchart LR
    A[Agent proposes an action] --> B{Layered safety checks}
    B -->|all pass, confident| C[Execute]
    B -->|uncertain| D[Escalate to a human]
    B -->|fails a check| E[Block]
```

The idea is that you shouldn't rely on one model always getting it right. Every action the agent proposes goes through a set of independent checks. If they all pass and the agent is confident, it goes ahead. If one fails, it's blocked. If the agent isn't sure, a human decides.
</details>

## Tools I use

<div align="center">

<img src="https://skillicons.dev/icons?i=python,java,ts,js,react,nextjs,spring,fastapi,postgres,sqlite,prisma,kafka,docker,sklearn,tailwind,vite,d3,git&perline=9" alt="Tech stack" />

</div>

## Contributions

<div align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake-dark.svg" />
  <img alt="Contribution snake" src="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake.svg" />
</picture>
</div>

---

<div align="center">
<i>If you want to talk about any of this, my email and LinkedIn are at the top.</i>
</div>
