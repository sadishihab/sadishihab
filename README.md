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

### 🔍 [Error Journal](https://anna.partners/store/@sadi/error-journal) — *paste an error, get a real fix*

A deterministic error-diagnosis app, live on the [Anna App Store](https://anna.partners/store/@sadi/error-journal). Paste any error — a Python traceback, a Kubernetes pod crash, a Docker build failure — and it gives you a real fix. Hit the exact same problem again later, even on a different machine, and it recognizes it and tells you what fixed it last time.

**Why it's interesting:**
- **Deterministic fingerprinting, not fuzzy matching.** Two logs of the same underlying error almost never look byte-identical — timestamps, pod names, and file paths all differ. The app strips everything volatile, classifies what remains, and hashes it, so the same problem is recognized as the same problem no matter how differently it's phrased each time.
- **109 curated diagnoses**, hand-written and verified, across Python, JavaScript/Node, Go, Java, Rust, Ruby, PHP, plus Kubernetes, Docker, shell, and networking. Outside that list, it says *"not in my playbook"* honestly rather than inventing a fix — a wrong fix during an outage is worse than no fix.
- **Returns runnable commands, not templates.** Real pod names, ports, and module names get substituted into fix steps, gated behind a strict allow-list so error text pasted by a user can never become a shell-injection vector in a command someone copies and runs.
- **Python, stdlib only**, shipped as single-file binaries for Linux, macOS, and Windows via PyInstaller in a GitHub Actions matrix, with a smoke test on every platform before release.
- **Testing surfaced real bugs**, including ANSI color codes silently breaking detection when copied from CI logs, and log-line prefixes like syslog and pytest tags causing correct errors to go unrecognized.

**Stack:** Python (stdlib only) · PyInstaller · JSON-RPC · GitHub Actions

🚀 [**Try it live**](https://anna.partners/store/@sadi/error-journal) · 📦 [**Source**](https://github.com/sadishihab/error-journal) · 🧱 [**Reusable template extracted from this build**](https://github.com/sadishihab/anna-app-template)

---

### 🦾 [Bimanual VLA Table Setting](https://github.com/sadishihab/bimanual-vla) — *measurement over assumption*

Two simulated SO-101 arms set a table in MuJoCo: a scripted expert picks four props out of a randomized layout, hands a prop from one arm to the other when no single arm can both reach it and reach its slot, records the successes as a LeRobot v3.0 dataset, trains an ACT policy on it, and converts the checkpoint to OpenVINO IR for Intel inference hardware.

The interesting part isn't the robotics. It's that every design decision traces back to a measurement, and the failures are reported rather than tuned away.

**Why it's interesting:**
- **A healthy mean hid a fatal failure.** FP16 quantization looked acceptable on mean absolute error — but **14.94% of gripper commands flipped sign**. A sign flip turns *close* into *open*, and a grasp that inverts once mid-carry drops the object. INT8 flips 0.92% and is 3.46× smaller; FP32 is exact. An averaged metric would never have surfaced this, so divergence is reported split by unit group and by sign flip.
- **The original parity check passed, and was wrong.** It ran against a single synthetic uniform-noise frame, where the FP16 IR scored 1.2e-03. On real dataset frames the same IR is off by 1.9e+00 — three orders of magnitude worse. Uniform images sit far outside the training distribution, so a badly wrong precision can look exact there. Conversion now validates against real frames and warns loudly.
- **Nothing is claimed that wasn't measured.** The README opens with a measured / not-measured table. GPU and NPU latency are marked unmeasured because no such device was available, and every NPU expectation in the document is labelled as expectation rather than result.
- **A controlled experiment, reported as one.** The trained policy places 3 of 40 props against the scripted expert's 24. Three causes were diagnosed — no task conditioning, VAE collapse, and plate class imbalance. Language conditioning was added through ACT's existing `environment_state` slot (**197k trainable parameters of 51.8M**, lerobot untouched), and the demonstrations were re-recorded in shuffled order to remove an image-task confound. Attention measurably redirected: non-plate target contact went **0/30 → 7/30**. Task competence did not follow, exactly as the two untouched causes predict. One cause isolated, not a fix claimed.
- **Physical findings from mesh geometry, not guesswork.** MuJoCo collides each gripper jaw as its convex hull, which bridges into a 1428 mm² facet tilted 21.7° off the opening axis — a ramp that wedges objects downward at any grasp height. The fix came from fitting planes through the actual mesh vertices (0.23° off-axis, 0.33 mm residual) rather than inventing geometry. Pick success went **57.5% → 92.5%**.

**Stack:** Python 3.11 · MuJoCo · LeRobot 0.4.4 (ACT, 51.6M params) · PyTorch · OpenVINO 2026.3.1 + NNCF · MiniLM-L6 · Kaggle T4

---

## 🔧 Open Source & Platform Contributions

### [anna-developer-docs](https://github.com/Anna-Partners/anna-developer-docs) — *corrections merged (PR #3)*

While building Error Journal on Anna's platform, I lost a day to platform behaviour that contradicted the documentation. Rather than work around it, I traced each discrepancy through the runtime source and wrote up seven findings with replacement text.

All seven verified as accurate. **Six merged into the public developer docs** — including a capability string that no longer existed in the runtime, a required manifest field missing from the reference table, and a config schema documented with the wrong data type. The seventh turned out to be a **production bug**: a storage-token issue that took the platform team a proper investigation to root cause, traced to a resource silently resetting its visibility when edited through the web UI. Confirmed and fixed in the following release.

> *"One of the best community write-ups we've received — seven precise findings, each verified against actual runtime behavior. We verified all seven items and every single one was accurate."*
> — platform engineering team

### [anna-app-template](https://github.com/sadishihab/anna-app-template)

A working starting point extracted from Error Journal's build, so the next builder doesn't repeat the same discovery. JSON-RPC transport with a forward queue for concurrent reverse-RPC, persistent storage and model sampling with graceful degradation, three-platform binary CI, and a publish runbook covering the failure mode at each step. Clone, run the rename script, get a running plugin.

---

## 🛠️ Tech Stack

**AI / LLM / RAG:** OpenAI APIs (embeddings + chat completions), FAISS, FastAPI, Uvicorn, prompt engineering, cross-lingual prompting, similarity-threshold tuning, multilingual knowledge base curation, intent taxonomy design, Facebook Messenger Platform
**Voice & Real-time:** AssemblyAI Voice Agent API, Universal-3.5 Pro, JSON-Schema tool calling, WebSocket relays, AudioWorklet / PCM16 capture, turn detection and barge-in, server-sent events
**Model Optimization & Robotics:** OpenVINO (IR conversion, INT8 quantization with NNCF, device benchmarking), LeRobot / ACT, MuJoCo, sentence-transformers
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
| [**Bimanual VLA**](https://github.com/sadishihab/bimanual-vla) | Dual-arm table setting in MuJoCo — scripted expert, 134-episode LeRobot dataset, ACT policy, and OpenVINO INT8 conversion. Quantization divergence is reported by sign flip rather than by mean, because a mean hides the failure that matters | Python · MuJoCo · LeRobot / ACT · PyTorch · OpenVINO · NNCF |

### Developer Tooling

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**error-journal**](https://anna.partners/store/@sadi/error-journal) | Deterministic error fingerprinting, live on the Anna App Store — strips timestamps, pod suffixes and container IDs so the same failure is recognised across machines, then surfaces what fixed it last time. 109 curated diagnoses across 7 languages plus Kubernetes, Docker and shell | Python (stdlib) · PyInstaller · JSON-RPC · GitHub Actions |
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
- Model optimization for edge inference — quantization accuracy, and the metrics that reveal what a mean conceals
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
