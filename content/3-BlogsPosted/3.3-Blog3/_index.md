---
title: "Blog 3"
date: 2026-08-04
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

#  Documents Uploaded Successfully, But the AI Still Answered Incorrectly – Lessons Learned About RAG and Knowledge Bases When Building an AI Learning Assistant

Hello everyone! 

While developing my **AI Learning Assistant** project, I wanted to build an AI assistant capable of answering questions based on users' learning materials instead of relying solely on the general knowledge of a Large Language Model (LLM).

I successfully implemented the document upload feature, and the document processing pipeline appeared to work correctly. However, once I started asking questions, the AI produced some unexpected answers.

Some questions were clearly covered in the uploaded documents, yet the AI either returned incorrect answers or responded using its general knowledge instead of the information I had provided.

At first, I thought the language model itself was not performing well. After investigating the system more thoroughly, I realized that the real issue was related to the **Knowledge Base** and the **Retrieval-Augmented Generation (RAG)** pipeline.

---

## System Architecture

When a user uploads a document, the system does not send the entire document directly to the AI model. Instead, the document must go through several processing stages before it can be used to answer questions.

The overall workflow is shown below.

### Figure 1. RAG Architecture of the AI Learning Assistant

![RAG Architecture of the AI Learning Assistant](/images/h1bl3.png)

---

## The Problem I Encountered

After uploading a document, I asked the following question:

> **What is Amazon EC2?**

Although the answer was clearly included in the uploaded document, the AI returned only a generic explanation, as if it were relying on its pre-trained knowledge rather than reading my document.

For some other questions, the AI even responded with:

> *"I couldn't find any relevant information in the document."*

However, that information actually existed in the uploaded document.

### Figure 2. The AI Returned Answers That Did Not Match the Uploaded Document

![The AI answered incorrectly even though the document had been uploaded](/images/h2bl3bl3.png)

---

## Root Cause

After reviewing the entire pipeline, I discovered that **successfully uploading a document does not necessarily mean the AI can immediately use it to answer questions**.

In a RAG system, once a document is uploaded, several additional processing steps are required:

- Extract text from the document.
- Split the content into smaller sections called **chunks**.
- Convert each chunk into a vector using an **Embedding** model.
- Store the vectors in a vector database.
- Convert the user's question into a vector.
- Retrieve the most relevant document chunks.
- Send both the user's question and the retrieved chunks to the AI model.

If any of these steps are incomplete or improperly configured, the AI may fail to retrieve the correct context and instead generate answers based on its general knowledge.

I also found that the system prompt was not restrictive enough. Since the AI was not explicitly instructed to answer only from the uploaded documents, it occasionally generated information that was not present in the Knowledge Base. This behavior is commonly known as **hallucination**.

---

## Solution

To resolve the issue, I performed the following improvements:

- Verified the processing status of the Knowledge Base.
- Asked questions only after document indexing was fully completed.
- Confirmed that the document was split into appropriate chunks.
- Verified that all chunks were successfully converted into vectors and stored in the vector database.
- Checked the Embedding model configuration.
- Updated the system prompt to ensure the AI only answers using the uploaded documents.
- Required the AI to clearly indicate when the requested information cannot be found instead of generating an answer.
- Verified the Retrieval mechanism to ensure the correct document chunks were retrieved.
- Tuned the number of retrieved chunks and similarity threshold when necessary.

The system prompt can be improved as follows:

> **Answer questions only using the information provided in the Knowledge Base. If no relevant information is found, clearly state that the current documents do not contain the requested information. Do not generate or infer information that is not present in the provided documents.**

---

## Optimized RAG Workflow

When a user submits a question, the system converts it into a vector representation and searches for the most relevant document chunks.

The retrieved chunks are then sent together with the user's question to the AI model, enabling it to generate an accurate, context-aware response.

### Figure 3. Optimized Retrieval-Augmented Generation Workflow

![Optimized Retrieval-Augmented Generation Workflow](/images/h3bl3.png)

After optimizing the pipeline, the AI became significantly more accurate. It was able to answer questions based on the uploaded documents while greatly reducing irrelevant and hallucinated responses.

---

## Lessons Learned

From this experience, I realized that **the quality of an AI application depends on much more than just the Large Language Model (LLM)**.

In RAG-based systems, the quality of responses also depends on:

- The quality of the source documents.
- The accuracy of text extraction.
- The document chunking strategy.
- Chunk size and overlap configuration.
- The Embedding model.
- The vector database.
- The Retrieval mechanism.
- The system prompt provided to the AI.

Even the most powerful AI model cannot provide accurate answers without the correct context.

---

## Conclusion

RAG is an effective approach for building AI applications that work with private enterprise or user data. However, achieving reliable results requires every stage of the pipeline—from document processing and embedding generation to retrieval—to be correctly configured.

Through this experience, I learned that optimizing the **Knowledge Base** and **Retrieval** process is just as important as choosing the right AI model.

I hope this article helps anyone building AI chatbots or RAG applications on AWS avoid the same issue that I encountered.

---

## References

 **AWS Documentation**

1. **Amazon Bedrock Knowledge Bases**  
   https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base.html

2. **What is Retrieval-Augmented Generation (RAG)?**  
   https://aws.amazon.com/what-is/retrieval-augmented-generation/

3. **Amazon Bedrock User Guide**  
   https://docs.aws.amazon.com/bedrock/latest/userguide/what-is-bedrock.html

4. **Build a Knowledge Base by Connecting to a Data Source**  
   https://docs.aws.amazon.com/bedrock/latest/userguide/knowledge-base-create.html

---

## Article Link

https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2233469244084702&notif_id=1785773605274872&notif_t=feedback_reaction_generic&ref=notif