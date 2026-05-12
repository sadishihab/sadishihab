# Hi, I'm Md. Shihabuddin Sadi 👋

**AI / RAG Application Developer · DevOps & Cloud Native Engineer · Ex-Samsung R&D**

> I build production RAG chatbots and AI agents that ship — multilingual support, grounded retrieval, no hallucinations. Backed by 15+ years of software engineering and the cloud infrastructure to keep it all running.

📅 [**Book a 30-min call →**](https://calendly.com/sadi-shihab/30min)  ·  🌐 [**Portfolio**](https://sadishihab.github.io/)  ·  💼 [**LinkedIn**](https://www.linkedin.com/in/md-shihabuddin-sadi/)

<br>

[![GitHub followers](https://img.shields.io/github/followers/sadishihab?label=Follow&style=social)](https://github.com/sadishihab)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin&style=flat-square)](https://www.linkedin.com/in/md-shihabuddin-sadi/)
[![Gmail](https://img.shields.io/badge/Email-Me-red?logo=gmail&style=flat-square)](mailto:sadi.shihab@gmail.com)

---

## 🌟 Featured: AI / RAG Work

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

## 🛠️ Tech Stack

**AI / LLM / RAG:** OpenAI APIs (embeddings + chat completions), FAISS, FastAPI, Uvicorn, prompt engineering, cross-lingual prompting, similarity-threshold tuning, multilingual knowledge base curation, intent taxonomy design, Facebook Messenger Platform
**Cloud & Infra:** AWS, DigitalOcean, Terraform, Ansible
**Containers & Orchestration:** Docker, Kubernetes, EKS
**CI/CD:** Jenkins, GitHub Actions, GitLab CI/CD
**Monitoring:** Prometheus, Grafana
**Languages:** Python, C, C++, Java, Bash, Groovy, JavaScript, SQL, YAML
**Other:** Linux, Git, Networking, Automation, Embedded Systems

---

## 📂 All Projects

### AI / RAG

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**Minimal RAG Chatbot**](https://github.com/sadishihab/minimal-rag-chatbot) | Multilingual (Bangla / Banglish / English → formal Bangla) RAG chatbot on Facebook Messenger; 224 Q&A entries across 14 intents, with similarity-threshold fallback and human takeover | Python · OpenAI · FAISS · FastAPI · Messenger Platform |

### Cloud, DevOps & Platform Engineering

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**Single-Node-Kubernetes-Cluster**](https://github.com/sadishihab/Single-Node-Kubernetes-Cluster) | Multi-service web app deployed on a single-node Kubernetes cluster using Minikube | Kubernetes · Docker · Ingress |
| [**eks**](https://github.com/sadishihab/eks) | Kubernetes on AWS (EKS) setup and deployment | AWS · EKS · Kubernetes |
| [**aws-services**](https://github.com/sadishihab/aws-services) | Complete CI/CD pipeline in AWS | AWS · CI/CD · Terraform |
| [**terraform**](https://github.com/sadishihab/terraform) | Infrastructure as Code with Terraform | Terraform · IaC · AWS |
| [**prometheus**](https://github.com/sadishihab/prometheus) | Monitoring setup using Prometheus and Grafana | Prometheus · Grafana · Metrics |
| [**ansible**](https://github.com/sadishihab/ansible) | Configuration management using Ansible | Ansible · Playbooks · Automation |
| [**jenkins**](https://github.com/sadishihab/jenkins) | Build automation and CI/CD pipelines using Jenkins | Jenkins · Groovy · Automation |
| [**kubernetes**](https://github.com/sadishihab/kubernetes) | Container orchestration demos and Kubernetes configs | Kubernetes · Pods · Services |
| [**docker**](https://github.com/sadishihab/docker) | Docker projects and containerized applications | Docker · Compose · Images |
| [**nexus**](https://github.com/sadishihab/nexus) | Running Nexus on droplet and publishing artifacts | Nexus · Artifact Mgmt · CI/CD |
| [**java-app-deploy**](https://github.com/sadishihab/java-app-deploy) | Create a server and deploy an app on DigitalOcean | Java · DO · Deployment |

### Programming & Automation

| Project | Description | Tech Highlights |
|---------|-------------|----------------|
| [**automation-with-python**](https://github.com/sadishihab/automation-with-python) | Automating workflows and tasks using Python scripting | Python · Automation |
| [**Leetcode**](https://github.com/sadishihab/Leetcode) | Python solutions to Leetcode problems | Python · DSA · Algorithms |
| [**python**](https://github.com/sadishihab/python) | Learning and practicing Python programming | Python · Basics · Projects |
| [**linux**](https://github.com/sadishihab/linux) | Basic Linux commands and shell utilities | Bash · Linux · SysOps |

---

## 📖 Blog

[Read my latest posts →](https://sadishihab.github.io/blog/) · [Subscribe via RSS](https://sadishihab.github.io/feed.xml) <a href="https://sadishihab.github.io/feed.xml"><img src="https://upload.wikimedia.org/wikipedia/commons/4/43/Feed-icon.svg" alt="RSS Feed" width="16" style="vertical-align: middle;"></a>

---

## 🌱 What I'm Working On

- Production RAG pipeline design without heavy framework abstractions
- Embedding strategy, vector search tuning, and cross-lingual prompt engineering
- Multilingual NLP for low-resource and script-mixed languages (Bangla / Banglish)
- Multi-agent AI workflows for research, ops, and customer support
- Evaluation pipelines and observability for production AI systems

---

## 🎯 Goals

- Ship reliable AI / RAG applications with strong evaluation, safety, and human-in-the-loop design
- Build production-grade Kubernetes clusters end-to-end for AI workloads
- Design secure, automated CI/CD pipelines for AI-powered microservices
- Contribute to open-source AI, DevOps, and cloud projects

---

## 💬 Let's Connect

Open to **AI / RAG project work**, contract engagements, and remote collaboration.

📅 [Book a 30-min call](https://calendly.com/sadi-shihab/30min) · 📧 [sadi.shihab@gmail.com](mailto:sadi.shihab@gmail.com) · 💼 [LinkedIn](https://www.linkedin.com/in/md-shihabuddin-sadi/) · 🌐 [Portfolio](https://sadishihab.github.io/)

---

> *"Automate everything. Consistency builds reliability."*

---

**Check out all my repositories → [github.com/sadishihab?tab=repositories](https://github.com/sadishihab?tab=repositories)**
