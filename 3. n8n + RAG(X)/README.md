# Assignment 3 – n8n + RAG Based Credit Appraisal Policy Chatbot

## 1. Project Title

**Document-Grounded Credit Appraisal Policy Chatbot using n8n and Retrieval-Augmented Generation (RAG)**

---

## 2. Assignment Objective

The objective of this assignment is to design and implement a Retrieval-Augmented Generation (RAG) based conversational application using **n8n**.

The chatbot is designed to answer questions strictly from a predefined knowledge base rather than relying on the general knowledge of the Large Language Model (LLM).

The project demonstrates how:

- A domain-specific document can be ingested into a RAG pipeline.
- Documents can be converted into vector embeddings.
- Embeddings can be stored in a vector store.
- User questions can be converted into embeddings.
- Relevant information can be retrieved from the knowledge base.
- An AI Agent can use the retrieved information to generate grounded responses.
- The system can avoid hallucinating values that are not available in the source document.

---

# 3. Domain Selected

## Domain: Financial Services – Credit Appraisal and Loan Eligibility

The selected domain is **Credit Appraisal / Loan Eligibility**.

The chatbot acts as a **Credit Appraisal Policy Assistant** that answers questions related to:

- Car Loan eligibility
- Home Loan eligibility
- Minimum bureau score
- Maximum Loan-to-Value (LTV)
- Fixed Obligations to Income Ratio (FOIR)
- Maximum loan tenor
- Applicant age at loan maturity
- Other eligibility criteria explicitly mentioned in the policy

The knowledge base covers two products:

1. **Car Loan**
2. **Home Loan**

The knowledge base specifically instructs the system to apply only the rules relevant to the identified loan product and not to assume values for unspecified parameters.

---

# 4. RAG Approach Used

## Type of RAG: Vector-Based Retrieval-Augmented Generation

This project uses a **vector-based RAG architecture**.

The system uses the **Simple Vector Store available in n8n** to store document embeddings and retrieve relevant document content based on semantic similarity.

The RAG pipeline consists of two major stages:

### Stage 1 – Document Ingestion

The Credit Appraisal Knowledge Base is:

1. Downloaded from Google Drive.
2. Loaded using the Default Data Loader.
3. Split into text chunks.
4. Converted into vector embeddings using Ollama.
5. Stored in the n8n Simple Vector Store.

### Stage 2 – Question Answering

When a user asks a question:

1. The question is received through the n8n Chat Trigger.
2. The AI Agent analyzes the question.
3. The question is sent to the Vector Store Tool.
4. The question is converted into an embedding.
5. Relevant document chunks are retrieved.
6. The retrieved information is provided to the AI Agent.
7. The Ollama Chat Model generates the final response.
8. The response is grounded in the retrieved policy information.

---

# 5. Why Vector-Based RAG?

A vector-based RAG approach was selected because the objective is to retrieve relevant policy information from an unstructured knowledge document.

Instead of requiring the LLM to memorize the entire policy, the system performs semantic retrieval and provides the relevant information to the model at query time.

This approach is useful for policy-based applications where:

- The source document is domain-specific.
- Exact policy values are important.
- The knowledge base may change over time.
- The system should avoid unsupported assumptions.
- Answers need to be grounded in the provided document.

---

# 6. Knowledge Base

The knowledge base used in this project is:

**Credit Appraisal RAG Knowledge Base**

File:

```text
Credit_Appraisal_RAG_Knowledge_Base.docx
The knowledge base contains:
- Car Loan Eligibility Policy
- Home Loan Eligibility Policy
- Policy Application Guidelines
- RAG Grounding Instructions
- RAG Testing Questions
- Questions that should trigger "Not Available in Policy"
- Quick Reference section
- Scope of the knowledge base
The document explicitly states that the knowledge base covers Car Loan and Home Loan eligibility criteria and does not include additional lending rules.

```
Embedding Model
mxbai-embed-large:latest

Chat Model
llama3.1:latest

## 11. System Architecture

The project consists of two major components:

1. **Document Ingestion Pipeline**
2. **Question Answering Pipeline**

### A. Document Ingestion Pipeline

The document ingestion pipeline processes the Credit Appraisal Knowledge Base and stores its vector embeddings in the Simple Vector Store.

```text
Google Drive
     |
     v
Download File
     |
     v
Default Data Loader
     |
     v
Document Chunks
     |
     v
Embeddings Ollama
(mxbai-embed-large)
     |
     v
Simple Vector Store


```
```

User Question
     |
     v
When Chat Message Received
     |
     v
AI Agent
     |
     +--------------------+
     |                    |
     v                    v
Ollama Chat Model     Simple Memory
     |
     |
     +----------------------------+
                                  |
                                  v
                         Simple Vector Store
                              (Tool)
                                  |
                                  v
                         Embeddings Ollama
                         (mxbai-embed-large)
                                  |
                                  v
                         Relevant Documents
                                  |
                                  v
                             AI Agent
                                  |
                                  v
                           Final Answer

```
### RAG Retrieval Process
```


User Question
      |
      v
AI Agent
      |
      v
Credit Policy Search Tool
      |
      v
Question Embedding
      |
      v
Vector Similarity Search
      |
      v
Relevant Policy Chunk
      |
      v
AI Agent
      |
      v
Final Answer

```
## Vector Store Tool Description
```

The following description is provided to the Vector Store Tool:

Search the Credit Appraisal RAG Knowledge Base for Car Loan and Home Loan eligibility rules.
Use this tool whenever the user asks about loan eligibility, minimum bureau score, maximum LTV, FOIR, loan tenor, applicant age at maturity, or other credit appraisal criteria.
Use only information explicitly stated in the provided Credit Appraisal RAG Knowledge Base. Apply only the rules relevant to the identified loan product.
Do not use general knowledge. Do not invent, estimate, assume, or substitute values. If the requested parameter is not specified in the knowledge base, state that it is not available in the provided policy.
```

## AI Agent System Prompt
```
You are a Credit Appraisal Policy Assistant.
Your only source of factual information is the Credit Appraisal RAG Knowledge Base available through the Credit Policy Search tool.
For every question about Car Loan or Home Loan eligibility, use the Credit Policy Search tool before answering.
Answer only from information retrieved from the knowledge base.
Do not use general knowledge or make assumptions.

Apply Car Loan rules only to Car Loan questions.
Apply Home Loan rules only to Home Loan questions.
If the requested information is not present in the knowledge base, respond:
"I couldn't find this information in the provided policy."
Give the exact value stated in the policy.
