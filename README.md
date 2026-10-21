<div align="center">

# Hi, I'm Kevin 👋

CS grad from Newcastle · building payment and fraud systems · into fintech, ML and AI safety

<a href="https://www.linkedin.com/in/kevin-steepan/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="mailto:ksteepan14@icloud.com"><img src="https://img.shields.io/badge/Email-333333?style=for-the-badge&logo=icloud&logoColor=white" alt="Email"></a>
<a href="https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app"><img src="https://img.shields.io/badge/Try_my_live_demo-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Live demo"></a>

</div>

Most of my projects end up being about money in some way. My dissertation was on stopping AI agents from making payments they shouldn't, and right now I'm building a small bank back office to learn how payments and fraud actually work.

## Projects

### [Clearhouse](https://github.com/KevST14/clearhouse) · what I'm working on now
*Java 21 · Spring Boot · PostgreSQL · Redpanda · React · Docker*

A double-entry ledger that publishes every transfer to Redpanda through a transactional outbox. A traffic generator simulates 120 customers and 22 shops, and you can set off card testing, a money mule ring or an account takeover on top of it. Each attack shows up as a different pattern in the dashboard. Next I'm adding an AI fraud analyst that gets scored against the generator's answer key.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevST14/clearhouse/main/docs/dashboard-dark.png">
  <img alt="Clearhouse dashboard showing three fraud attacks in the money-flow network" src="https://raw.githubusercontent.com/KevST14/clearhouse/main/docs/dashboard-light.png">
</picture>

### [Rent Reality Check](https://github.com/KevST14/london-rent-reality-check) · [live demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app)
*Python · scikit-learn · SHAP · Streamlit*

Predicts a fair nightly price for a London Airbnb and shows which features pushed it up or down. I tested it with spatial cross-validation so it can't just memorise neighbourhoods. On areas it hadn't seen it scored **R² 0.72** with a **22% median error**.

### [Split Decision](https://github.com/KevST14/SplitDecision)
*Python · FastAPI · React · SQLite*

Tracks Polymarket odds and flags big swings. You can log your own probability before you see the market's, and when the market resolves you get a Brier score, so you find out whether you'd have beaten the crowd.

## Quick quiz

<details>
<summary>You tap "pay", lose signal, and the app sends the request again. How many times should you be charged?</summary>
<br>

**Once.** Each payment has an idempotency key, so a retry gets back the original transfer instead of creating a new one. Clearhouse tests this by sending the same request 20 times from 8 threads at once. Only one goes through.
</details>

<details>
<summary>When pricing a London Airbnb, what helps more: <i>where</i> it is, or <i>how the listing is written</i>?</summary>
<br>

**Where it is.** Location features (distance to stations, parks and places to eat) took R² from 0.62 to 0.65. The listing text was only worth about £1–2 a night.
</details>

## Tools I use

<img src="https://skillicons.dev/icons?i=python,java,ts,react,nextjs,spring,fastapi,postgres,kafka,docker,sklearn,git" alt="Tech stack" />

<br><br>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake-dark.svg" />
  <img alt="Contribution snake" src="https://raw.githubusercontent.com/KevST14/KevST14/output/github-contribution-grid-snake.svg" />
</picture>
