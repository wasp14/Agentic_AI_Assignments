# Assignment 4 – n8n Multi-Agent System (MAS)

## Sequential Multi-Agent Architecture using n8n, Ollama and Tavily

---

## 1. Problem Statement

The objective of this assignment is to design and implement a **Multi-Agent System (MAS)** using **n8n**, where multiple AI agents collaborate sequentially to process a user's query and generate a meaningful final response.

Instead of relying on a single AI agent to perform every task, the workflow divides the problem into specialized stages.

The implemented system consists of two AI agents:

1. **Agent 1 – Information Research Agent**
   - Understands the user's query.
   - Identifies relevant keywords and topics.
   - Uses web search to collect comprehensive information.
   - Passes the collected research to the next agent.

2. **Agent 2 – Final Analysis Agent**
   - Receives the research output from Agent 1.
   - Analyzes and synthesizes the collected information.
   - Generates the final response based on the user's query.
   - Can produce summaries, sentiment results, comparisons, insights, recommendations, or conclusions depending on the query.

The workflow demonstrates a **Sequential Multi-Agent System**, where the output of one agent becomes the input/context for the next agent.

---

## 2. Objective

The main objectives of this project are:

- To understand the concept of **Multi-Agent Systems (MAS)**.
- To implement a sequential agent architecture using **n8n**.
- To divide a complex task between specialized AI agents.
- To integrate an **Ollama Chat Model** for local LLM processing.
- To integrate **Tavily Search** for web-based information retrieval.
- To pass information from one AI agent to another.
- To demonstrate agent collaboration through a sequential workflow.
- To generate a final response using the combined capabilities of multiple agents.
- To document the complete workflow and execution process.

---

## 3. Solution Overview

The implemented solution follows a **Sequential Multi-Agent Architecture**.

```text
                         USER
                           │
                           ▼
              ┌────────────────────────┐
              │  Chat Message Trigger  │
              └────────────┬───────────┘
                           │
                           ▼
              ┌────────────────────────┐
              │       AGENT 1          │
              │ Information Research   │
              │        Agent           │
              └────────────┬───────────┘
                           │
                    Research Output
                           │
                           ▼
              ┌────────────────────────┐
              │       AGENT 2          │
              │   Final Analysis       │
              │        Agent           │
              └────────────┬───────────┘
                           │
                           ▼
                    FINAL RESPONSE


