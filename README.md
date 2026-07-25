<h1 align="center">Amr Mohammed</h1>

<p align="center">
  <b>Machine Learning Engineer</b> · LLM systems, RAG &amp; evaluation · Cairo, Egypt 🇪🇬
</p>

<p align="center">
  <a href="https://amr-mohammed.com"><img src="https://img.shields.io/badge/Portfolio-2088FF?style=for-the-badge&logo=vercel&logoColor=white" alt="Portfolio"></a>
  <a href="https://www.linkedin.com/in/amr-mohammed01"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:amrm88289@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
</p>

---

## `> whoami`

```
name:      Amr Mohammed
role:      Machine Learning Engineer
location:  Cairo, Egypt
focus:
  - RAG & retrieval systems
  - LLM evaluation
  - production deployment
```

I build LLM systems where the quality claims are **measured**, not asserted — golden datasets, retrieval metrics, hallucination guards, and CI that blocks changes which make the system worse. I've also shipped a live product end-to-end, solo, with real payments.

**Currently seeking:** Machine Learning Engineer / AI Engineer roles — remote or Cairo.

---

## Featured: DocuMind — evaluation-first RAG

> **[Live demo](https://documind.amr-mohammed.com)** · **[Case study](https://amr-mohammed.com/documind)** · **[Source](https://github.com/AmrMohamed17/Documind)**

A RAG platform over technical documentation where every quality claim is measured — and a GitHub Actions gate fails any pull request whose retrieval regresses below a committed baseline.

**Measured on a hand-built, programmatically-validated 100-question golden dataset** (FastAPI docs · 40 files → 667 chunks):

| metric | result |
| --- | --- |
| Multi-hop recall@10 | **0.36 → 0.57** after two-stage retrieval (+58%) |
| Single-hop recall@10 | **0.97** — held flat through reranking |
| Hallucination guard | **15/15** unanswerable questions correctly refused |
| Answer faithfulness | **4.82/5** mean · 95% scored ≥ 4 (LLM-as-judge) |

**Stack:** FastAPI · PostgreSQL + pgvector · Gemini embeddings (768d, Matryoshka-truncated) · FlashRank cross-encoder + Reciprocal Rank Fusion · Docker Compose + Caddy on AWS EC2 · GitHub Actions

**Three things I'd point an engineer at:**

- **The CI gate.** Every PR spins up pgvector, loads frozen corpus embeddings from a committed fixture (no re-embedding — cheap and deterministic), runs the recall suite, and fails the build on regression. Only the deterministic metrics are hard-gated; the LLM judge reports but never blocks.
- **The diagnosis before the fix.** Multi-hop recall@3 came back at 0.14. Instead of guessing, I built a per-question tracer and found the correct passage was retrieved every time but ranked below the cutoff — a *ranking* problem. That's what justified the reranker, with a baseline waiting to be beaten.
- **The experiment that didn't ship.** Hybrid search (BM25 + dense, fused via RRF) was implemented and measured: recall moved ≤0.01 at every k. The failures were ranking-shaped, not coverage-shaped, so the complexity didn't earn its place and the branch didn't merge. The negative result stays documented in the repo.

---

## More projects

| Project | What it demonstrates | Stack | Links |
| --- | --- | --- | --- |
| 🎁 **la7za** | Arabic-first digital gift platform — built solo, live, with real payment processing. Fully RTL. | Next.js · TypeScript · Supabase · Paddle | [Code](https://github.com/AmrMohamed17/la7za) · [Live](https://la7za.vercel.app) |
| ☕ **BeanBuddy** | Stateful conversational ordering agent — multi-turn dialog, transactions persisted to managed cloud DB. | Dialogflow ES · FastAPI · MySQL/AWS RDS · EC2 | [Code](https://github.com/AmrMohamed17/BeanBuddy) |
| 🔎 **Local Product Finder** | Graduation project (**A+**) — real-time product recognition + hybrid recommender, shipped in a mobile app with a cross-functional team. | MobileNet · Sentence-BERT · LightFM · TensorFlow | [Code](https://github.com/AmrMohamed17/Local-Product-Finder) |
| 📚 **Elevvo Internship** | 6 end-to-end ML tasks: regression, clustering, imbalanced classification (SMOTE), recommenders (SVD), CNN transfer learning — tracked with MLflow. | scikit-learn · XGBoost · TensorFlow · MLflow | [Code](https://github.com/AmrMohamed17/Elevvo_Internship) |

---

## Stack

**LLM & RAG** — RAG pipelines · vector search &amp; embeddings · cross-encoder reranking · rank fusion · LLM-as-judge evaluation · hallucination guards · golden-dataset design · prompt engineering

**Backend & data** — Python · FastAPI · Pydantic · psycopg 3 · PostgreSQL/pgvector · MySQL · SQL · REST APIs · TypeScript

**Infra & CI** — Docker &amp; Compose · GitHub Actions · AWS (EC2, RDS) · Caddy · Linux · Git · Pytest

**Core ML** — PyTorch · TensorFlow · scikit-learn · pandas · NumPy · MLflow · Computer Vision · NLP

---

## Certifications

**DeepLearning.AI & Stanford Online** — Advanced Learning Algorithms; Supervised Machine Learning (2024)
**Imperial College London** — Mathematics for Machine Learning Specialization (2024)
**Harvard University** — CS50's Introduction to AI with Python (2024); CS50x (2022)

---

<p align="center">
  If you want AI that survives contact with production — and can prove it did — let's talk.
</p>

<p align="center">
  <a href="https://amr-mohammed.com"><img src="https://img.shields.io/badge/See%20my%20work-2088FF?style=for-the-badge&logo=vercel&logoColor=white" alt="Portfolio"></a>
  <a href="https://www.linkedin.com/in/amr-mohammed01"><img src="https://img.shields.io/badge/Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:amrm88289@gmail.com"><img src="https://img.shields.io/badge/Reach%20out-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="Email"></a>
</p>
