<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=26&duration=3000&pause=800&color=3B82F6&center=true&vCenter=true&width=600&lines=Hey%2C+I'm+Kevin+%F0%9F%91%8B;I+build+finance-tech+tools;I+make+AI+agents+ask+before+they+act;Is+that+number+actually+trustworthy%3F" alt="Typing intro" />

**Software engineer · CS graduate, Newcastle University · Looking for 2027 grad roles in bank & fintech tech**

<a href="https://www.linkedin.com/in/kevin-steepan/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:ksteepan14@icloud.com"><img src="https://img.shields.io/badge/Email-333333?style=for-the-badge&logo=icloud&logoColor=white" alt="Email"></a>
<a href="https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app"><img src="https://img.shields.io/badge/Try_my_live_demo-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Live demo"></a>

</div>

---

I like problems where a number *looks* right but might not be. That's taken me into prediction markets, explainable pricing models, and a dissertation on stopping AI agents from doing something stupid with money.

## 🎲 Quick calibration test

Before you scroll, try the thing my projects are built around. Make a guess, then click to check.

<details>
<summary><b>Q1.</b> I say a market has a 70% chance of YES. It resolves NO. What's my Brier score? (lower is better)</summary>
<br>

**0.49.** Brier score = (forecast − outcome)², so (0.7 − 0)² = 0.49.
If I'd hedged at 50% I'd have scored 0.25, and if I'd said 10% I'd have scored 0.01. Confidence only pays when you're right, which is exactly what [Split Decision](https://github.com/KevST14/SplitDecision) tracks over time.
</details>

<details>
<summary><b>Q2.</b> Pricing a London Airbnb: what helps the model more, <i>where</i> it is or <i>how the listing is written</i>?</summary>
<br>

**Where it is.** Adding location features (distance to stations, parks, food) pushed R² from 0.62 to 0.65. Analysing the listing text added only about £1–2 a night. Clever copywriting doesn't change much. [See for yourself in the live demo ↗](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app)
</details>

<details>
<summary><b>Q3.</b> An AI agent is 60% sure a payment is legit. Should it send the money?</summary>
<br>

**Not on its own.** That's the question my dissertation is about: stack independent checks, and when the agent's uncertainty crosses a threshold, it escalates to a human instead of guessing. Scroll down for the diagram.
</details>

## 🔨 Things I've built

<details open>
<summary><h3>📈 Split Decision: can you beat a prediction market?</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)

Watches Polymarket, snapshots prices on a schedule, and alerts when odds swing hard. The fun part: lock in your own probability *before* you see the market price, then get scored against the real outcome.

```mermaid
flowchart LR
    A[Polymarket API] -->|polled by APScheduler| B[(SQLite snapshots)]
    B --> C[Swing alerts]
    B --> D[Correlation across markets]
    E[Your blind guess] --> F[Brier score vs outcome]
    B --> F
```

**[→ View repo](https://github.com/KevST14/SplitDecision)**
</details>

<details>
<summary><h3>🏠 Rent Reality Check: is that Airbnb a fair price?</h3></summary>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)
![SHAP](https://img.shields.io/badge/SHAP-explainable_AI-555555?style=flat-square)

Give it a London short-let and it predicts a fair nightly price from Inside Airbnb and OpenStreetMap data, then shows *why* with a SHAP breakdown. It's spatially cross-validated, so it can't cheat by memorising neighbourhoods.

| R² (held-out) | Median error | Mean error |
|:---:|:---:|:---:|
| **0.72** | **22%** | **~£60/night** |

**[→ Try the live demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app)** · **[View repo](https://github.com/KevST14/london-rent-reality-check)**
</details>

<details>
<summary><h3>💷 SpendSync: personal finance dashboard</h3></summary>

![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)

Track spending and income, set category budgets and savings goals, and automate recurring transactions, all behind a typed, Zod-validated REST API.

**[→ View repo](https://github.com/KevST14/SpendSync)**
</details>

<details>
<summary><h3>🎓 Dissertation: when should an AI agent stop and ask?</h3></summary>

*Design and Evaluation of a Layered Safety Architecture for Autonomous Financial Execution Agents* (2026)

```mermaid
flowchart LR
    A[Agent proposes an action] --> B{Layered safety checks}
    B -->|all pass, confident| C[Execute]
    B -->|uncertain| D[Escalate to a human]
    B -->|fails a check| E[Block]
```

Rather than trusting one model to get it right, the architecture puts independent checks between the agent and the money and treats uncertainty as a reason to hand over to a human.
</details>

## 🧰 Toolkit

<div align="center">

<img src="https://skillicons.dev/icons?i=python,ts,js,java,react,nextjs,tailwind,vite,fastapi,postgres,sqlite,prisma,sklearn,git&perline=7" alt="Tech stack" />

</div>

## 🐍 Contributions

<div align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake-dark.svg" />
  <img alt="Contribution snake" src="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake.svg" />
</picture>
</div>

---

<div align="center">
<i>Happy to chat about markets, models, or agents that know their limits.</i>
</div>
