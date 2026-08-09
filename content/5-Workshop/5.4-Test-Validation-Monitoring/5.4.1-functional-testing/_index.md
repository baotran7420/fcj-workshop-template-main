---
title: "Functional Testing"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

## Objective

Verify the main functions of the **AI Learning Assistant Platform** after the system has been deployed on **Amazon EC2**, particularly the ability to create a Knowledge Base, process documents, and perform queries through the **RAG** system.

---

## Implementation

### 1. Access the Application

Access the **AI Learning Assistant Platform** through the Web address of the Amazon EC2 instance:

```text
http://<ELASTIC_IP>:3000
```

For example:

```text
http://13.219.3.244:3000
```

Then, log in to the system using the **Administrator (Root)** account.

---

### 2. Test the Knowledge Base and RAG

After successfully logging in, create a new **Knowledge Base**.

Upload a sample document in **PDF** or **Word** format.

The document processing process uses **PostgreSQL + pgvector** to store and process **Vector Embeddings**, which are used for information retrieval during the RAG process.

---

### 3. Test the AI Chat Function

Open the **AI Chat** interface and ask a question directly related to the content of the uploaded document.

For example, if the document contains information about AWS, a question related to the content presented in the document can be used.

The system retrieves relevant information from the Knowledge Base and uses the retrieved information to generate the response.

---

### 4. Verify the Result

The test results are evaluated based on the following criteria:

- The system successfully receives and processes the uploaded document.
- The Knowledge Base can use the document content to retrieve relevant information.
- The AI Chat can answer questions related to the document content.
- The generated answer contains information relevant to the source document.
- The system displays the corresponding **Citation** for the source content used to generate the answer.

> **Figure 5.4.1. AI Chat functional testing result and document source citation.**

> ![Figure 5.4.1](/images/5.4.1.png)

---

## Result

The testing process verifies the main functions of the **AI Learning Assistant Platform**, from uploading documents to the **Knowledge Base** to querying information through the **AI Chat** interface.

The test results are used to validate the operation of the **Retrieval-Augmented Generation (RAG)** workflow and the system's ability to provide answers based on the content of the source documents.