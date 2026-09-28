<h1 align="center">Amr Mohammed</h1>

<p align="center">
  <b>Machine Learning Engineer</b> · LLM &amp; agent systems · evaluation · GenAI fine-tuning · Cairo, Egypt 🇪🇬
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
now:
  - ML Engineer @ GETnFORM              # on-prem generation platform, Flux LoRAs (part-time)
  - AI Intern   @ Al Amalka Securities  # Arabic document OCR, market-data pipelines
focus:
  - LLM & agent systems (RAG, LangGraph, MCP)
  - evaluation-first engineering
  - generative vision (LoRA · SDXL · Flux)
```

I build LLM, agent, and vision systems where the quality claims are **measured**, not asserted: golden datasets, retrieval metrics, hallucination guards, and CI that blocks changes which make the system worse. When something fails, I reason from ML fundamentals to find out why. In DocuMind, weak retrieval turned out to be a *ranking* failure, not a coverage one. In my Mamluk LoRA, style leakage was the model overwriting its base class, which is a *regularization* problem. Lately that includes fine-tuning diffusion models, where the eval is fixed prompts and seeds and the failure modes are style bleed and hallucinated architecture.

**Open to:** full-time Machine Learning Engineer / AI Engineer roles, remote or Cairo.

---

## Now

**ML Engineer · GETnFORM** (part-time, remote · Sep 2026–)

- Architecting a confidential client's on-prem image-generation platform: async GPU job queue, swappable inference engines behind one interface, and a LoRA registry. Confidentiality forced self-hosting. My break-even analysis priced that choice (fal is cheaper below ~10–20k images/month) and sized the hardware (48 GB VRAM, Flux licence).
- Training Flux LoRAs for exact architectural style transfer: curation, captioning, and fixed-seed evaluation for style accuracy, hallucination, and bleeding. I got the role on the strength of the Mamluk LoRA below.

**AI Intern · Al Amalka Securities** (EGX brokerage · Aug 2026–)

- Offline Egyptian national-ID extractor (OpenCV + two YOLO models + PaddleOCR 3.x Arabic): **84/84** front fields correct on the test set, every field confidence-tagged. Extended to KSA passports (MRZ + VLM) and birth certificates, where I traced digit errors to a missing Arabic-Indic zero glyph in PaddleOCR v3.
- [Live OCR of the MIST trade feed](https://github.com/AmrMohamed17/egx-ocr). The documented finding: the window repaints in jumps during bursts, so coverage is capped (~90–95%) by the data source, not by the OCR. It feeds an EGX forecasting pipeline I'm building.
- Rebuilt the company's bilingual RTL website (React/Express, admin CMS, auth).

---

## Featured: DocuMind — evaluation-first RAG

> **[Live demo](https://documind.amr-mohammed.com)** · **[Case study](https://amr-mohammed.com/documind)** · **[Source](https://github.com/AmrMohamed17/Documind)**

A RAG platform over technical documentation where every quality claim is measured — and a GitHub Actions gate fails any pull request whose retrieval regresses below a committed baseline.

**Measured on a hand-built, programmatically-validated 100-question golden dataset** (FastAPI docs · 40 files → 667 chunks):

| metric | result |
| --- | --- |
| Multi-hop recall@10 | **0.36 → 0.57** after two-stage retrieval (+58%) |
| Single-hop recall@10 | **0.97** — held flat through reranking |
| Hallucination guard | held on **all 15** unanswerable cases |
| Answer faithfulness | **4.82/5** mean · 95% scored ≥ 4 (LLM-as-judge, spot-checked, used directionally) |

**Stack:** FastAPI · PostgreSQL + pgvector · Gemini embeddings (768d, Matryoshka-truncated) · FlashRank cross-encoder + Reciprocal Rank Fusion · Docker Compose + Caddy on AWS EC2 · GitHub Actions

**Three things I'd point an engineer at:**

- **The CI gate.** Every PR spins up pgvector, loads frozen corpus embeddings from a committed fixture (no re-embedding — cheap and deterministic), runs the recall suite, and fails the build on regression. Only the deterministic metrics are hard-gated; the LLM judge reports but never blocks.
- **The diagnosis before the fix.** Multi-hop recall@3 came back at 0.14. Instead of guessing, I built a per-question tracer and found the correct passage was retrieved every time but ranked below the cutoff — a *ranking* problem. That's what justified the reranker, with a baseline waiting to be beaten.
- **The experiment that didn't ship.** Hybrid search (BM25 + dense, fused via RRF) was implemented and measured: recall moved ≤0.01 at every k. The failures were ranking-shaped, not coverage-shaped, so the complexity didn't earn its place and the branch didn't merge. The negative result stays documented in the repo.

---

## OSS Contribution Copilot — measure before you build

> **[Case study](https://www.amr-mohammed.com/oss-copilot)** · **[Source](https://github.com/AmrMohamed17/oss-copilot)** · **[MCP server on PyPI](https://pypi.org/project/oss-issues-mcp/)**

A supervised multi-agent system (in progress) that finds claimable open-source issues and drafts a human-approved claim comment. Before writing any agent code I audited **2,568 issues** across five ecosystems. **90.7%** of type labels turned out to be author-applied via templates, not maintainer judgment, and I caught a **39.3-point** authorship confound in my own calibration set. The shipped piece is **[oss-issues-mcp](https://github.com/AmrMohamed17/oss-issues-mcp)**: derived triage tools (not a GitHub passthrough), a repo allowlist, and write access off by default. It's listed in the official MCP Registry.

---

## More projects

| Project | What it demonstrates | Stack | Links |
| --- | --- | --- | --- |
| 🎁 **la7za** | Arabic-first digital gift platform — built solo, live, with real payment processing. Fully RTL. | Next.js · TypeScript · Supabase · Paddle | [Code](https://github.com/AmrMohamed17/la7za) · [Live](https://la7za.vercel.app) |
| 🕌 **Mamluk Cairo Style LoRA** | SDXL LoRA built in one day on 42 licensed photos (curated from ~237). v1 overwrote the base class (plain "mosque" prompts came out Mamluk). v2 added prior-preservation regularization to bind the style to the trigger token, and a strength sweep removed the colour cast. | SDXL · LoRA · prior preservation | [Model](https://huggingface.co/Amr292/mmlkcairo-sdxl-lora) · [Dataset](https://huggingface.co/datasets/Amr292/mamluk-cairo-style-dataset) |
| 📨 **Reactivation Agent** | Closed-lost leads → scored, drafted, and **grounding-verified** re-engagement emails. A separate verifier call flags unsupported claims, and the send endpoint refuses anything a human hasn't approved. | Next.js · Supabase · Resend · LLM pipeline | [Code](https://github.com/AmrMohamed17/Reactivation-Agent) · [Live](https://reactivation-agent-one.vercel.app) |
| 🔎 **Local Product Finder** | Graduation project (**A+**) — real-time product recognition + hybrid recommender, shipped in a mobile app with a cross-functional team. | MobileNet · Sentence-BERT · LightFM · TensorFlow | [Code](https://github.com/AmrMohamed17/Local-Product-Finder) |
| 📚 **Elevvo Internship** | 6 end-to-end ML tasks: regression, clustering, imbalanced classification (SMOTE), recommenders (SVD), CNN transfer learning — tracked with MLflow. | scikit-learn · XGBoost · TensorFlow · MLflow | [Code](https://github.com/AmrMohamed17/Elevvo_Internship) |

---

## Stack

**LLM & agents** — LangGraph multi-agent systems · MCP · RAG pipelines · vector search &amp; embeddings · cross-encoder reranking · rank fusion · LLM-as-judge evaluation · hallucination guards · golden-dataset design · prompt engineering

**Backend & data** — Python · FastAPI · Pydantic · psycopg 3 · PostgreSQL/pgvector · MySQL · SQL · REST APIs · TypeScript

**Infra & CI** — Docker &amp; Compose · GitHub Actions · AWS (EC2, RDS) · Caddy · Linux · Git · Pytest

**GenAI & vision** — LoRA fine-tuning (SDXL, Flux) · dataset curation &amp; captioning · PaddleOCR · EasyOCR · YOLO · OpenCV · VLMs

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
