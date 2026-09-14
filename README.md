# Hi, I'm Md. Shihabuddin Sadi 👋

**Software Engineer · AI / RAG & Voice Agent Developer · DevOps & Cloud Native · Ex-Samsung R&D**

> I build production RAG chatbots and voice agents that ship — multilingual support, grounded retrieval, and validation layers that refuse to guess. Backed by 15+ years of software engineering and the cloud infrastructure to keep it all running.

**Available for contract and subcontract work.** I work directly with product teams, and as the engineering layer behind agencies — white-label, under NDA, your client relationship stays yours.

📅 [**Book a 30-min call →**](https://calendly.com/sadi-shihab/30min)  ·  🌐 [**Portfolio**](https://sadishihab.github.io/)  ·  💼 [**LinkedIn**](https://www.linkedin.com/in/md-shihabuddin-sadi/)

<br>

[![GitHub followers](https://img.shields.io/github/followers/sadishihab?label=Follow&style=social)](https://github.com/sadishihab)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin&style=flat-square)](https://www.linkedin.com/in/md-shihabuddin-sadi/)
[![Gmail](https://img.shields.io/badge/Email-Me-red?logo=gmail&style=flat-square)](mailto:sadi.shihab@gmail.com)

---

## 🌟 Featured: AI / RAG / Voice Work

### 🎙️ [Claim Intake Agent](https://github.com/sadishihab/claim-intake-agent) — *the agent that refuses to guess*

A voice agent that takes insurance claims by phone and **cannot write a value into the record unless server-side code approves it**. The agent listens and proposes. A validator decides, returning one of three verdicts — accepted, unconfirmed, rejected — along with the exact sentence the agent must then speak, phonetically spelled. It never invents a readback.

**Why it's interesting:**
- **Biasing the recogniser manufactured false accepts.** Feeding AssemblyAI's `keyterms` the list of valid policy numbers improved accuracy — and started rewriting mis-heard numbers into real ones. One call's transcript partial was `C411`; its final answer was `KD4-1188`, a real policy belonging to someone else, which then passed exact-match validation perfectly. The validator's power rested on an assumption never written down: that the transcript is an *independent* observation of what the caller said. Biasing toward the answer key removed that, and every guard downstream stayed intact and stopped working.
- **Three attempts to fix it in the recogniser, three null results.** Transcription mode, turn-detection patience and tool-schema format hints were each measured against the same four policy numbers. All null — the same letter is lost in every configuration, including one that produced a single perfectly patient turn. The failure is acoustic, and no setting reaches it. That negative result is the argument for the validation layer.
- **Consent is bound to the question asked.** Agreeing that a value was heard correctly is not agreeing to replace a value already recorded. Two separate consents, enforced in code rather than requested in a prompt.
- **Evidence trail** — every attempt is logged as it happens, rejections included, each linked to what the caller actually said and when. Crash-safe JSONL append, swept after 24 hours so caller PII does not accumulate.
- **206 tests**, including 62 on the validation layer alone — confusable policy pairs like `BX7-4402` vs `BX7-4420`, and all three verdicts. Several pin design decisions rather than behaviour, so a later change that quietly undoes one fails with an explanation of why it existed.
- **Three documentation corrections published by AssemblyAI** from findings during the build; the keyterms result escalated to their research team.

**Stack:** Python 3.14 · AssemblyAI Voice Agent API (Universal-3.5 Pro) · FastAPI · raw WebSocket relay · AudioWorklet (PCM16 @ 24 kHz) · Server-sent events · Docker · nginx · Let's Encrypt · DigitalOcean

🎧 [**Try it live**](https://claims.sadishihab.com) · 📊 [**What validation catches**](https://claims.sadishihab.com/compare)

---

### 🤖 [Minimal RAG Chatbot](https://github.com/sadishihab/minimal-rag-chatbot)

A production multilingual RAG chatbot deployed on **Facebook Messenger** for an interior design company in Dhaka. Customers send questions in **Bangla, Banglish, or English** — the bot always replies in **formal Bangla**, grounded in a curated knowledge base, with graceful human takeover when confidence is low.

**Why it's interesting:**
- Built from scratch **without LangChain or LlamaIndex** — every line of the pipeline is transparent and debuggable
- **Embedding the question, not the answer** (the design choice that fixed more bugs than any prompt tweak)
- **Similarity-threshold fallback** so the bot says *"share your number, our manager will call"* instead of hallucinating
- **4-stage safe deployment** workflow: terminal → local web → test FB page → live page
- 12 passing pytest tests covering schema, language enums, intent coverage, and answer rules

**Stack:** Python 3.13 · OpenAI (`text-embedding-3-small`, `gpt-4o-mini`) · FAISS (`IndexFlatIP`, L2-normalized) · FastAPI · Uvicorn · Facebook Graph API · Pytest

📖 [Full case study on my blog →](https://sadishihab.github.io/blog/)

---

## 🔧 Open Source

### [anna-developer-docs](https://github.com/Anna-Partners/anna-developer-docs) — *corrections merged (PR #3)*

Lost a day to platform behaviour that contradicted the documentation. Traced each discrepancy through the runtime source rather than working around it, and wrote up seven findings with replacement text.

All seven verified as accurate. **Six merged into the public developer docs** — including a capability string that no longer existed in the runtime, a required manifest field missing from the reference table, and a config schema documented with the wrong data type. The seventh turned out to be a **platform bug**: editing a resource through the web UI silently reset its visibility, causing publish failures that looked like user error. Confirmed and fixed in the following release.

> *"One of the best community write-ups we've received — seven precise findings, each verified against actual runtime behavior. We verified all seven items and every single one was accurate."*
> — platform engineering team

### [anna-app-template](https://github.com/sadishihab/anna-app-template)

A working starting point extracted from a shipped app, so the next builder doesn't repeat the discovery. JSON-RPC transport with a forward queue for concurrent reverse-RPC, persistent storage and model sampling with graceful degradation, three-platform binary CI, and a publish runbook covering the failure mode at each step. Clone, run the rename script, get a running plugin.

---

## 🛠️ Tech Stack

**AI / LLM / RAG:** OpenAI APIs (embeddings + chat completions), FAISS, FastAPI, Uvicorn, prompt engineering, cross-lingual prompting, similarity-threshold tuning, multilingual knowledge base curation, intent taxonomy design, Facebook Messenger Platform
**Voice & Real-time:** AssemblyAI Voice Agent API, Universal-3.5 Pro, JSON-Schema tool calling, WebSocket relays, AudioWorklet / PCM16 capture, turn detection and barge-in, server-sent events
**Cloud & Infra:** AWS, DigitalOcean, Terraform, Ansible
**Containers & Orchestration:** Docker, Kubernetes, EKS
**CI/CD:** Jenkins, GitHub Actions, GitLab CI/CD
**Monitoring:** Prometheus, Grafana
**Languages:** Python, C, C++, Java, Bash, Groovy, JavaScript, SQL, YAML
**Other:** Linux, Git, Networking, Automation, Embedded Systems

---

## 📂 Selected Projects

### AI / RAG / Voice

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**Claim Intake Agent**](https://github.com/sadishihab/claim-intake-agent) | Voice claim intake where a server-side validator returns one of three verdicts before anything reaches the record; readbacks are generated by the validator and spoken verbatim. Includes a live comparison of what a transcript-trusting system would have recorded | Python · AssemblyAI Voice Agent API · FastAPI · WebSockets · AudioWorklet · Docker · nginx |
| [**Minimal RAG Chatbot**](https://github.com/sadishihab/minimal-rag-chatbot) | Multilingual (Bangla / Banglish / English → formal Bangla) RAG chatbot on Facebook Messenger; 224 Q&A entries across 14 intents, with similarity-threshold fallback and human takeover | Python · OpenAI · FAISS · FastAPI · Messenger Platform |

### Developer Tooling

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**error-journal**](https://github.com/sadishihab/error-journal) | Deterministic error fingerprinting — strips timestamps, pod suffixes and container IDs so the same failure is recognised across machines, then surfaces what fixed it last time. 109 curated diagnoses across 7 languages plus Kubernetes, Docker and shell | Python (stdlib) · PyInstaller · JSON-RPC · GitHub Actions |
| [**anna-app-template**](https://github.com/sadishihab/anna-app-template) | Reusable scaffold with working transport, storage, sampling and three-platform binary CI. Clone, rename, running plugin | Python · PyInstaller · GitHub Actions |

### Cloud, DevOps & Platform Engineering

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**aws-services**](https://github.com/sadishihab/aws-services) | Complete CI/CD pipeline in AWS | AWS · CI/CD · Terraform |
| [**eks**](https://github.com/sadishihab/eks) | Kubernetes on AWS (EKS) setup and deployment | AWS · EKS · Kubernetes |
| [**terraform**](https://github.com/sadishihab/terraform) | Infrastructure as Code with Terraform | Terraform · IaC · AWS |
| [**prometheus**](https://github.com/sadishihab/prometheus) | Monitoring and alerting with Prometheus and Grafana | Prometheus · Grafana · Metrics |
| [**jenkins**](https://github.com/sadishihab/jenkins) | Build automation and CI/CD pipelines | Jenkins · Groovy · Automation |
| [**Single-Node-Kubernetes-Cluster**](https://github.com/sadishihab/Single-Node-Kubernetes-Cluster) | Multi-service web app on a single-node cluster with ingress routing | Kubernetes · Docker · Ingress |

More infrastructure work — Ansible, Nexus, Docker, Kubernetes configs and deployment runbooks — in [the full repository list](https://github.com/sadishihab?tab=repositories).

---

## 📖 Blog

[Read my latest posts →](https://sadishihab.github.io/blog/) · [Subscribe via RSS](https://sadishihab.github.io/feed.xml) <a href="https://sadishihab.github.io/feed.xml"><img src="https://upload.wikimedia.org/wikipedia/commons/4/43/Feed-icon.svg" alt="RSS Feed" width="16" style="vertical-align: middle;"></a>

---

## 🌱 What I'm Working On

- Production RAG pipeline design without heavy framework abstractions
- Validation layers for voice agents, where speech recognition failures cannot be detected by the agent itself
- Embedding strategy, vector search tuning, and cross-lingual prompt engineering
- Multilingual NLP for low-resource and script-mixed languages (Bangla / Banglish)
- Evaluation pipelines and observability for production AI systems
- End-to-end Kubernetes and CI/CD for AI workloads

---

## 💬 Working Together

I take on RAG, AI agent, and voice agent projects — both direct engagements and subcontract work behind agencies and product studios.

**For agencies:** I work white-label and under NDA. You keep the client relationship and the brand; I build the RAG pipelines, agent backends, validation layers and the infrastructure underneath, or come in when something that worked in the demo stops working in production.

📅 [Book a 30-min call](https://calendly.com/sadi-shihab/30min) · 📧 [sadi.shihab@gmail.com](mailto:sadi.shihab@gmail.com) · 💼 [LinkedIn](https://www.linkedin.com/in/md-shihabuddin-sadi/) · 🌐 [Portfolio](https://sadishihab.github.io/)

---

> *"Automate everything. Consistency builds reliability."*

---

**Check out all my repositories → [github.com/sadishihab?tab=repositories](https://github.com/sadishihab?tab=repositories)**
