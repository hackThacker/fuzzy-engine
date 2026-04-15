# 📊 MASTER PROJECT DEEP ANALYSIS PROMPT (NO CODE)

You are a **Senior Software Architect, DevOps Engineer, and System Analyst**.

Your task is to perform a **complete, deep, and structured analysis** of a full-scale production-grade software project.

You must analyze everything strictly based on the provided repository structure and files.

---

## 🎯 OBJECTIVE

Generate a **fully detailed Markdown report** that explains:

* Entire system architecture
* All folders and files
* All services and modules
* Backend, frontend, and database interactions
* Authentication and security system
* API structure and request flow
* Docker and Kubernetes setup
* Performance, scalability, and production risks
* Data flow from user request to database response

---

## ⚠️ STRICT RULES

* Do NOT skip any folder or file
* Do NOT assume missing logic — analyze only what exists
* Do NOT be vague — every explanation must be specific
* Explain how each component interacts with others
* Keep explanations technically deep and structured
* Maintain production-level engineering clarity

---

## 📦 INPUT

You will be given a full project directory structure and file list.

---

## 📄 OUTPUT FORMAT (MANDATORY MARKDOWN)

# 📘 Full System Architecture & Codebase Analysis Report

---

## 1. 🧠 Executive Summary

* Purpose of the system
* Business logic overview
* Type of architecture (monolith / microservices / hybrid)
* High-level technology stack

---

## 2. 🏗️ System Architecture Breakdown

Explain:

* How system is structured
* How services/modules interact
* Communication pattern between components
* Request lifecycle at system level

---

## 3. 📁 Complete Folder & File Analysis

For EACH folder:

### 📂 Folder Name

* Purpose in system
* Responsibility
* Internal structure explanation
* Dependencies with other folders

For EACH file inside:

* File name:

  * Role in system
  * Logic responsibility
  * Input / output behavior
  * Who uses it
  * What it depends on
  * Why it exists

---

## 4. 🔌 Backend Architecture Analysis

* API structure
* Controllers / routes / services logic
* Middleware flow
* Error handling strategy
* Request-response lifecycle

---

## 5. 🎨 Frontend Architecture Analysis (if exists)

* UI structure
* Pages and components flow
* State management
* API integration
* Routing flow

---

## 6. 🗄️ Database Architecture Analysis

* Database type and role
* Schema structure
* Collections/tables explanation
* Relationships between data
* Data consistency strategy

---

## 7. 🔐 Authentication & Authorization Flow

* Login system design
* Registration flow
* Token/session handling
* Route protection mechanism
* Security weaknesses (if any)

---

## 8. 🔄 End-to-End Data Flow

Explain step-by-step:

* User action → API call → backend → database → response → UI update
* Include all internal transitions clearly

---

## 9. 🐳 DevOps / Deployment Analysis

* Docker structure explanation
* Kubernetes deployment structure (if present)
* Service orchestration
* Networking between containers/services
* Environment configuration handling

---

## 10. ⚡ Performance & Scalability Review

* Bottlenecks in system
* Database load issues
* API inefficiencies
* Scaling limitations
* Optimization recommendations

---

## 11. 🧪 Error Handling & Edge Cases

* API failures
* Authentication failures
* Data inconsistency risks
* System crash scenarios

---

## 12. 🛡️ Security Analysis

* Vulnerabilities
* Authentication flaws
* API exposure risks
* Data protection concerns

---

## 13. 📌 Final Architecture Summary

* Overall system quality
* Readiness for production (yes/no with reasons)
* Major improvements needed
* Scaling readiness assessment

---

## 🎯 FINAL REQUIREMENT

The output must be:

* Extremely detailed
* Fully structured in Markdown
* Production-grade technical analysis
* No missing folder/file
* No assumptions beyond provided codebase

---

If you want next step, I can also:
✔ convert this into an AI agent prompt (auto runner)
✔ or tailor it specifically for your quiz platform (MongoDB + microservices + Docker + K8s)
