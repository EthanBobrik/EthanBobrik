👋 Hey there,

I’m **Ethan Bobrik**, a Data Science student at Western University who builds machine learning systems for finance and applied research.

---

# 💫 About Me

- 🎯 Focused on quantitative finance and applied deep learning
- 🎓 Data Science student at Western University (expected graduation: 2027)
- 🧠 Interested in the engineering side of ML: retrieval, evaluation, and production concerns, not only model accuracy

---

# 🏆 Featured Projects

### 🎓 Undergraduate Thesis: American Option Pricing under Heston-Nandi GARCH *(in progress)*
**[hn-garch-american-options](https://github.com/EthanBobrik/hn-garch-american-options)**

Pricing American options when volatility follows a Heston-Nandi GARCH process, using Least-Squares Monte Carlo (LSM) to learn the early-exercise policy.

- Simulates risk-neutral HN-GARCH price and conditional-variance paths, with separate seeded random streams for fitting the policy and evaluating it
- Prices Europeans with the closed-form Heston-Nandi solution, using the characteristic function and numerical integration
- Uses a Monte Carlo European pricer with standard errors to check the simulator against the closed form
- Runs config-driven experiments over a grid of GARCH environments, strikes, and maturities
- Includes a pytest suite covering simulation, sampling, and European pricing
- **Stack:** Python, NumPy, SciPy, pytest


### 🧠 KDA Gate Granularity: How Fine-Grained Should Forgetting Be?
**[kda-gate-granularity](https://github.com/noahkostesku/kda-gate-granularity)** · with [Noah Kostesku](https://github.com/noahkostesku)

A pre-registered, controlled study of decay-gate granularity in Kimi Delta Attention (KDA), a delta-rule linear attention layer. KDA learns one decay gate per key channel and Gated DeltaNet learns one per head. This study treats the number of gates per head, G, as a dial between those two designs and tests whether finer gates help because a sequence needs several memory timescales at once.

- Sweeps G = 1, 2, 4, 8, 16, 32 in 2-layer, ~0.65M-parameter models trained from scratch on a synthetic multi-timescale recall task, with key-value lags from 16 to 1,024 tokens
- Fixed the hypotheses, margins, and analysis code in a pre-registration before the main runs, and logged every deviation; the final analysis covers 479 runs
- Found that finer gates did not help: one gate per head matched 32 gates and beat them on the longest lag band (94% vs. 47% accuracy), and the predicted benefit of mixing lag bands did not appear
- Showed that heads matter more than gates: 4 heads beat 1 head at the same number of decay rates by 7 to 15 points
- Showed through gate ablations that the long-lived gates carry the long-range memory: disabling the longest-lived 20% costs 43 points, against 30 for a random 20%
- Built a reproducible pipeline: a plain-PyTorch reference recurrence as ground truth for the GPU kernels, hash-pinned test sets, SLURM array jobs on the Alliance clusters, and one command that rebuilds every reported number
- **Stack:** PyTorch, R, SLURM, pytest

### 📈 SurfaceAlpha — Volatility Surfaces as Images
**[SurfaceAlpha](https://github.com/EthanBobrik/SurfaceAlpha)**

A research-grade quantitative finance project that models equity option markets by treating implied volatility surfaces as multi-channel images.

- Fuses a **Vision Transformer** over the IV surface with a temporal returns encoder and a macro context encoder
- Routes the fused representation through a **regime-conditional Mixture of Experts**
- Produces three simultaneous outputs: a forward realized-volatility forecast, a tail-risk probability, and a market-regime classification
- Drives a live portfolio overlay with per-regime position sizing, vol targeting, and short overlays
- **Stack:** PyTorch, multimodal encoders, config-driven training and backtesting


### 🤖 MultiDocChat — RAG with an LLMOps Toolkit
**[RAG-LLMOps](https://github.com/EthanBobrik/RAG-LLMOps)** · [Live demo](https://multidocchat.onrender.com/)
A multi-document conversational RAG application built around production concerns rather than a bare demo. Upload PDFs, Word, or text files and chat with them, with answers grounded in retrieved content and a pipeline that is measurable and swappable.

- **Eval-gated quality:** an LLM-as-judge harness scores correctness, faithfulness, answer relevancy, and context precision/recall against a golden dataset, and fails CI if quality regresses below thresholds
- **Hybrid retrieval + reranking:** BM25 lexical search fused with dense vector search, then re-scored by a cross-encoder reranker, all toggleable from config
- **Agentic corrective-RAG:** an optional LangGraph engine that grades retrieved documents, rewrites the query and retries on weak retrieval, and checks its own answer for grounding before returning
- **Token streaming (SSE):** answers stream token-by-token, cutting time-to-first-token from ~1.5s to ~0.5s versus the blocking endpoint
- **Operable:** structured JSON logging, per-request latency metrics, local on-device embeddings, and a pluggable session store (in-memory or Redis)
- **Stack:** FastAPI, LangChain (LCEL), LangGraph, FAISS, fastembed

---

# 🔬 In Progress

### 🏦 Post-Earnings Announcement Drift (PEAD) Forecasting
**[Post-Earnings-Announcement-Drift-Prediction](https://github.com/EthanBobrik/Post-Earnings-Announcement-Drift-Prediction)**

A pipeline that predicts the drift following earnings announcements from earnings events, call transcripts, and market reactions, with value-glamour controls.

- Builds features from earnings events (EPS surprise, report time, opening gap, volume shock, volatility) and Alpha Vantage transcript sentiment, with optional FinBERT embeddings
- Controls for value-glamour effects with EP, BM, CP, and sales growth
- Produces probabilistic forecasts of 5-day and 20-day drift direction, with optional BHAR magnitude forecasts
- Compares calibrated logistic regression and XGBoost baselines against a multimodal tabular + transcript fusion model and a TCN over pre-event price sequences
- Prevents look-ahead leakage by timing every feature to the first tradeable open after the report
- Includes an event-driven backtest with probability-weighted position sizing and a real-time inference demo
- **Stack:** Python, XGBoost, PyTorch, FinBERT, Alpha Vantage

---

# ✅ Completed

### ⚾ MLB Bullpen Strategy
**[MLB-Bullpen-Strategy](https://github.com/EthanBobrik/MLB-Bullpen-Strategy)**

Offline reinforcement learning to decide when to pull a starting pitcher and which reliever to bring in, trained on recent-season Statcast data.

- Turns pitch-level Statcast into plate-appearance decision points, with state covering inning, outs, base state, score differential, pitch count, times-through-order, platoon matchups, and windowed embeddings of the next hitters
- Reward is the negative change in run expectancy from the fielding team's view, folded over a three-batter SMDP window with a small pull penalty
- Implements dueling DQN, Conservative Q-Learning, and tabular Q, driven by YAML configs
- Offline policy evaluation with TD-error sweeps, policy-versus-behavior stats, and Q-value diagnostics
- Availability masks and behavior labels derived from logged Statcast decisions
- **Stack:** PyTorch, pybaseball, pandas, NumPy

### 👃 ScentFinder
**[ScentFinder](https://github.com/EthanBobrik/ScentFinder)**

An end-to-end pipeline from scraping to model building to evaluation, producing niche fragrance recommendations based on favourite notes and accords.

- Web scraping of notes plus a pre-cleaned Kaggle dataset
- Compares two pipelines: SVD + kNN, and Masked Autoencoder + kNN
- Hybrid model combining LLM-generated preference personas with sparse fragrance encodings for affinity scoring
- Uses Maximum Marginal Relevance to diversify recommendation rankings

### 🛡️ Credit Card Fraud Detection
**[Credit-Card-Fraud-Detection](https://github.com/EthanBobrik/Credit-Card-Fraud-Detection)**

An end-to-end pipeline for highly imbalanced fraud detection.

- Implements XGBoost, Random Forest, and neural networks
- Evaluates with PR-AUC, a strong metric for skewed datasets
- Uses stratified cross-validation, feature scaling, undersampling, and class weighting
- Achieved a 23% recall improvement over a logistic regression baseline

---

# 💻 Tech Stack

**Languages**

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![R](https://img.shields.io/badge/r-%23276DC3.svg?style=for-the-badge&logo=r&logoColor=white)
![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=for-the-badge&logo=openjdk&logoColor=white)
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=csharp&logoColor=white)
![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=for-the-badge&logo=css3&logoColor=white)

**ML / Deep Learning**

![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-%230C55A5.svg?style=for-the-badge&logo=scipy&logoColor=%white)

**LLM / Retrieval**

![LangChain](https://img.shields.io/badge/LangChain-%231C3C3C.svg?style=for-the-badge&logo=langchain&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=for-the-badge&logo=fastapi&logoColor=white)
![FAISS](https://img.shields.io/badge/FAISS-%230467DF.svg?style=for-the-badge&logo=meta&logoColor=white)

**Databases**

![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=for-the-badge&logo=mongodb&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=for-the-badge&logo=mysql&logoColor=white)
![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)
![MSSQL](https://img.shields.io/badge/Microsoft%20SQL%20Server-CC2927?style=for-the-badge&logo=microsoft%20sql%20server&logoColor=white)

**Tooling & Viz**

![Git](https://img.shields.io/badge/git-%23F05033.svg?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/github-%23121011.svg?style=for-the-badge&logo=github&logoColor=white)
![GitLab](https://img.shields.io/badge/gitlab-%23181717.svg?style=for-the-badge&logo=gitlab&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-%233F4F75.svg?style=for-the-badge&logo=plotly&logoColor=white)
![Power BI](https://img.shields.io/badge/power_bi-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

---

# 🌐 Socials

[![LinkedIn](https://img.shields.io/badge/LinkedIn-%230077B5.svg?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/EthanBobrik/)

---

# 📬 Contact

- 📧 **Email:** <ethan.bobrik@gmail.com>
- 🌍 **GitHub:** [github.com/EthanBobrik](https://github.com/EthanBobrik)

---

# ✍️ Inspiring Quote

> “A program is never less than 90% complete, and never more than 95% complete.”
> — Terry Baker, Coder

---

[![](https://visitcount.itsvg.in/api?id=EthanBobrik&icon=0&color=0)](https://visitcount.itsvg.in)
