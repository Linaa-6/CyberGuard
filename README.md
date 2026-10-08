# CyberGuard — Agentic AI Cybersecurity Research System

CyberGuard is an **agentic AI system for cybersecurity research**. It uses multiple specialized agents to investigate cybersecurity questions, retrieve relevant internal security policies, analyze evidence, verify findings, and generate a structured final report.

The project was developed as part of the **SDAIA Building Gen AI Apps program** to explore practical applications of Generative AI, RAG, and agentic workflows.

---

## Project Overview

Cybersecurity research often requires information from multiple sources, including external security resources and organization-specific policies.

CyberGuard combines these sources in one workflow:

**User Question → Planning → Web Research + Policy RAG → Analysis → Fact Checking → Final Report**

The system can also perform additional research when the fact-checking stage determines that the available evidence is insufficient.

---

## System Architecture

```text
                         User Question
                               │
                               ▼
                           Planner
                               │
                  ┌────────────┴────────────┐
                  ▼                         ▼
             Web Research              Policy RAG
               (Tavily)              (Internal Policies)
                  │                         │
                  ▼                         │
             Loop Guard                    │
                  │                         │
                  └────────────┬────────────┘
                               ▼
                            Analyst
                               │
                               ▼
                         Fact Checker
                          │         │
                    Retry Research  │
                          │         │
                          └────┐    │
                               ▼    ▼
                              Writer
                                │
                                ▼
                         Final Report
```

---

## Main Components

### 1. Planner

The Planner breaks the user's cybersecurity question into focused research tasks.

### 2. Researcher

The Researcher gathers information from reliable external cybersecurity sources using web search.

### 3. Policy RAG

The Policy RAG component retrieves relevant information from organization-specific security policies.

### 4. Analyst

The Analyst combines the research findings and policy context, identifies important facts and risks, and develops recommendations.

### 5. Fact Checker

The Fact Checker evaluates whether the evidence is sufficient and reliable.

If more research is needed, the workflow can return to the Researcher.

### 6. Writer

The Writer produces the final structured cybersecurity report using the verified evidence.

### 7. Loop Detection

Loop detection and research-attempt limits help prevent the system from repeatedly performing the same actions.

### 8. Observability

Execution information such as agent activity, timing, and model usage can be tracked to make the workflow easier to understand and debug.

---

## Retrieval-Augmented Generation (RAG)

CyberGuard uses **RAG (Retrieval-Augmented Generation)** to connect the language model with organization-specific security policies.

The pipeline is:

```text
Policy Documents
       ↓
Document Loading
       ↓
Text Splitting
       ↓
Embeddings
       ↓
Vector Store
       ↓
Semantic Retrieval
       ↓
Relevant Policy Context
       ↓
LLM
```

The project uses:

* `RecursiveCharacterTextSplitter`
* Hugging Face embeddings
* `sentence-transformers/all-MiniLM-L6-v2`
* `InMemoryVectorStore`

The policy documents used in this project are **simulated policies created for demonstration purposes**.

---

## External Web Research

CyberGuard uses **Tavily** for external cybersecurity research.

The research workflow focuses on reliable cybersecurity sources and returns source links with the collected findings.

URL validation is also used to reduce the risk of accessing unsafe or internal URLs.

---

## Technologies

* Python
* LangChain
* LangGraph
* OpenRouter
* Tavily
* Hugging Face Embeddings
* InMemoryVectorStore
* Google Colab

---

## Example Query

Example question:

> How can an organization protect itself from phishing attacks?

CyberGuard processes the question through the agent workflow and produces a structured report based on:

* External cybersecurity research
* Internal simulated security policies
* Analysis of the collected evidence
* Fact checking
* Source references

---

## What I Built

This project goes beyond a basic research chatbot by combining:

* Multi-agent architecture
* Agent orchestration with LangGraph
* RAG for internal security policies
* External web research
* Semantic search
* Fact-checking
* Conditional research retry
* Loop detection
* Research attempt limits
* Checkpoint-based workflow state
* Observability

---

## Project Structure

```text
CyberGuard/
│
├── data/
│   └── policies/
│       ├── phishing_policy.txt
│       ├── authentication_policy.txt
│       ├── incident_response_policy.txt
│       └── access_control_policy.txt
│
├── notebooks/
│   └── CyberGuard_Final.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Example Policy Documents

The project includes simulated security policies covering areas such as:

* Phishing
* Authentication
* Incident Response
* Access Control

These documents demonstrate how RAG can provide organization-specific context to an AI system.

---

## Challenges & Lessons Learned

During development, I worked with:

* LangChain and LangGraph agent workflows
* RAG and vector stores
* Embeddings and semantic search
* External web research tools
* Conditional agent routing
* Debugging asynchronous workflows
* Managing model API limitations
* Preventing repeated agent/tool execution

The project helped me understand how individual AI components can be combined into a more reliable agentic system.

---

## Future Improvements

Possible future improvements include:

* Adding more cybersecurity policy documents
* Using a persistent vector database
* Adding more specialized cybersecurity agents
* Improving source credibility scoring
* Adding a user interface
* Adding more advanced security monitoring capabilities
* Improving evaluation and benchmarking
* Supporting additional cybersecurity frameworks

---

## Disclaimer

This project is an **educational demonstration** of agentic AI and RAG concepts.

The security policies included in the repository are simulated and should not be considered real organizational security policies.

---

## Author

**Lina Alharbi**

Information Technology Student
Saudi Electronic University

Built as part of the **SDAIA Building Gen AI Apps program**.

Submitted by: Lina Alharbi — academy: @SDAIAAcademy
