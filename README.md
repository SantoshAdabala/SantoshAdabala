<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=Santosh%20Adabala&fontSize=52&fontColor=ffffff&fontAlignY=38&desc=Machine%20Learning%20Engineer&descAlignY=58&descSize=20&descColor=a78bfa" width="100%"/>

<br/>

[![Portfolio](https://img.shields.io/badge/Portfolio-santoshadabala.com-6366F1?style=for-the-badge&logo=googlechrome&logoColor=white)](https://santoshadabala.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/santosh-adabala/)
[![Email](https://img.shields.io/badge/Email-santoshbalu25%40gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:santoshbalu25@gmail.com)
[![Location](https://img.shields.io/badge/Lakewood%2C%20CO-USA-10B981?style=for-the-badge&logo=googlemaps&logoColor=white)](https://www.google.com/maps/place/Lakewood,+CO)

</div>

---

## What I work on

I build ML systems end-to-end — from training runs on rented GPUs to production inference APIs that actually stay up. My focus is the gap between "it works in the notebook" and "it runs at scale without falling over."

Current obsessions: LLM alignment (why does reward accuracy diverge from factuality?), model compression without killing accuracy, and distributed ML pipelines that don't require a dedicated ops team to maintain.

---

## Benchmarks that matter

<div align="center">

| | Result | Project |
|---|---|---|
| **DPO Reward Accuracy** | 82% (peak 88%) | distill-align-llm |
| **Factuality — LLM-judge** | 75.7% on 500-prompt benchmark | distill-align-llm |
| **Model Compression** | 107.7M → 65.2M params · 93.2% F1 retained | clinical-nlp-optimization |
| **Inference Speedup** | 39ms → 10.8ms · 1.9× faster | clinical-nlp-optimization |
| **Weak Label Generation** | 19,506 entities from 7,064 PubMed abstracts | clinical-nlp-optimization |
| **SLA Compliance** | 97% of requests under 50ms (100-req load test) | clinical-nlp-optimization |
| **Training Cost** | ~$27 total · SFT + DPO on Llama-3.1-8B | distill-align-llm |

</div>

---

## Projects

<details>
<summary><b>distill-align-llm</b> — SFT → DPO alignment on Llama-3.1-8B · <a href="https://distill-align-llm-aembgrswzfay6bjupbnjpp.streamlit.app">Live dashboard</a></summary>

<br/>

Full alignment pipeline using QLoRA (r=16, α=32, 4-bit NF4). Trained on RunPod for ~$27 total.

The main finding: reward accuracy and factuality are not the same thing. 82% reward accuracy on DPO, but only 17.6% factuality with strict keyword matching on 51 prompts — and 75.7% with a proper 500-prompt LLM-judge benchmark. Same model. The evaluation methodology matters more than people admit.

Token probability analysis showed the model knows the answers — it just suppresses them. Median correct token rank after SFT/DPO: position 2. It's a generation suppression problem, not a forgetting problem.

**Stack:** PyTorch · HuggingFace TRL · PEFT · bitsandbytes · Streamlit · pytest (44 passing)

[![Repo](https://img.shields.io/badge/GitHub-distill--align--llm-181717?style=flat-square&logo=github)](https://github.com/SantoshAdabala/distill-align-llm)
[![Dashboard](https://img.shields.io/badge/Streamlit-Live%20Dashboard-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://distill-align-llm-aembgrswzfay6bjupbnjpp.streamlit.app)

</details>

<details>
<summary><b>clinical-nlp-optimization</b> — Knowledge distillation + distributed NLP pipeline for clinical NER</summary>

<br/>

Compressed Bio_ClinicalBERT (107.7M params) down to DistilClinicalBERT (65.2M) while retaining 93.2% of F1. Deployed as a FastAPI inference server with Prometheus + OpenTelemetry observability.

The pipeline covers six components end-to-end: distillation, distributed weak labeling on PySpark/EMR, ONNX pruning + INT8 quantization, LangChain agentic evaluation, statistical A/B testing (Mann-Whitney + Wilcoxon), and a production observability stack. 97% SLA compliance on a 100-request load test.

**Stack:** PyTorch · HuggingFace · ONNX Runtime · PySpark · AWS EMR/S3/Lambda · FastAPI · LangChain · Prometheus · Grafana · Terraform

[![Repo](https://img.shields.io/badge/GitHub-clinical--nlp--optimization-181717?style=flat-square&logo=github)](https://github.com/SantoshAdabala/clinical-nlp-optimization)

</details>

<details>
<summary><b>TheInheritableAgent</b> — Cryptographic AI inheritance · Auth0 for AI Agents Hackathon</summary>

<br/>

When someone passes away, their family inherits their belongings — but never their way of thinking. This lets a parent's AI-extracted decision patterns be inherited by their child through cryptographically scoped Auth0 tokens, while keeping every piece of personal data permanently inaccessible.

The boundary is enforced at the identity layer, not application code. 2-of-3 trustee multi-sig, step-up auth for sensitive topics, multi-generational token delegation where scopes can only shrink — never expand.

**Stack:** Python · Flask · Auth0 Token Vault · JWT · Claude API

[![Repo](https://img.shields.io/badge/GitHub-TheInheritableAgent-181717?style=flat-square&logo=github)](https://github.com/SantoshAdabala/TheInheritableAgent)

</details>

<details>
<summary><b>PHI/PII Parser</b> — FHIR-compliant redaction on AWS Lambda</summary>

<br/>

Reads HL7 FHIR Bundle JSON files from S3, detects and redacts PII/PHI fields (name, DOB, SSN, address), and writes a cleaned CSV back to S3. Two deployment modes: FastAPI for local on-demand scanning, Lambda for serverless auto-triggering on every S3 upload.

**Stack:** Python · FastAPI · AWS S3/Lambda · Pydantic v2 · Docker/LocalStack

[![Repo](https://img.shields.io/badge/GitHub-PHI--PII--Parser--from--AWS-181717?style=flat-square&logo=github)](https://github.com/SantoshAdabala/PHI-PII-Parser-from-AWS)

</details>

<details>
<summary><b>Agentic AI Parenting</b> — Multi-agent system on Google ADK + FatSecret</summary>

<br/>

A modular parenting agent built on Google's Agent Development Kit. Root agent delegates to specialized sub-agents: parenting analyst, nutrition meal planner (FatSecret API), and a basic pediatric medical advisor. Stateful sessions remember user context across turns.

**Stack:** Python · Google ADK · Gemini · LiteLLM · FatSecret Nutrition API

[![Repo](https://img.shields.io/badge/GitHub-Agentic__AI__Parenting-181717?style=flat-square&logo=github)](https://github.com/SantoshAdabala/Agentic_AI_Parenting)

</details>

---

## Stack

<div align="center">

**Core ML**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![PEFT](https://img.shields.io/badge/PEFT%2FQLoRA-8B5CF6?style=flat-square)
![ONNX](https://img.shields.io/badge/ONNX_Runtime-005CED?style=flat-square&logo=onnx&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)

**Distributed & Cloud**

![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![AWS](https://img.shields.io/badge/AWS%20EMR%20%7C%20S3%20%7C%20Lambda-232F3E?style=flat-square&logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat-square&logo=terraform&logoColor=white)

**Agents & APIs**

![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Google ADK](https://img.shields.io/badge/Google%20ADK-4285F4?style=flat-square&logo=google&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)

**Observability & Infra**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat-square&logo=opentelemetry&logoColor=white)

</div>

---

## GitHub Stats

<div align="center">

![Santosh's GitHub Stats](https://github-readme-stats.vercel.app/api?username=SantoshAdabala&show_icons=true&theme=tokyonight&hide_border=true&include_all_commits=true&count_private=true&bg_color=0d1117&title_color=a78bfa&icon_color=6366f1&text_color=e2e8f0)

![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=SantoshAdabala&layout=compact&theme=tokyonight&hide_border=true&langs_count=6&bg_color=0d1117&title_color=a78bfa&text_color=e2e8f0)

![GitHub Streak](https://streak-stats.demolab.com?user=SantoshAdabala&theme=tokyonight&hide_border=true&background=0d1117&ring=a78bfa&fire=6366f1&currStreakLabel=a78bfa)

</div>

---

<div align="center">

![Profile Views](https://komarev.com/ghpvc/?username=SantoshAdabala&style=flat-square&color=6366f1&label=Profile+Views)

*Open to senior ML engineering roles. Best contact: [santoshbalu25@gmail.com](mailto:santoshbalu25@gmail.com)*

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:24243e,50:302b63,100:0f0c29&height=100&section=footer" width="100%"/>

</div>
