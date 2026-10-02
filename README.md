## Hi, I'm Kevin

Computer Science graduate from Newcastle University. I build tools that check whether a number can be trusted, not just whether it looks plausible: prediction-market calibration, explainable pricing models, and guardrails for AI agents that act on money.

I'm looking for graduate software engineering roles in banking and financial technology, starting 2027.

### What I'm working on

**[Split Decision](https://github.com/KevST14/SplitDecision)** · Python, FastAPI, SQLite, React, TypeScript
A read-only tracker for Polymarket prediction markets. A scheduled job snapshots prices into SQLite, flags big odds swings, and runs Pearson correlations across related markets. The part I care about most is the calibration tracker: you lock in your own probability *before* seeing the market price, and it scores you against the outcome with a Brier score.

**[Rent Reality Check (London)](https://github.com/KevST14/london-rent-reality-check)** · Python, scikit-learn, SHAP, Streamlit · [Live demo](https://london-rent-reality-check-jikdwpaozdee8hvjjccgaa.streamlit.app)
Predicts a fair nightly price for a London short-let from Inside Airbnb and OpenStreetMap data, then explains the number feature by feature with SHAP. Spatially cross-validated so the model can't cheat by memorising neighbourhoods. R² 0.72 on held-out data.

**[SpendSync](https://github.com/KevST14/SpendSync)** · Next.js, TypeScript, PostgreSQL, Prisma
A personal finance dashboard: expenses, income, category budgets, savings goals and recurring transactions, with a Zod-validated REST API.

**Dissertation:** *Design and Evaluation of a Layered Safety Architecture for Autonomous Financial Execution Agents* (2026). Layered checks, uncertainty-based escalation to a human, and evaluation of where an agent should and shouldn't be allowed to act on its own.

### Tools I use

**Languages:** Python, TypeScript, JavaScript, Java, SQL
**Backend & data:** FastAPI, PostgreSQL, SQLite, Prisma
**Frontend:** React, Next.js, Tailwind CSS, Vite
**ML:** scikit-learn, SHAP, pandas, Jupyter

### Interested in

Financial markets technology · AI assurance and model risk · building agents that know when to stop and ask

### Get in touch

[LinkedIn](LINKEDIN_URL_HERE) · ksteepan14@icloud.com
