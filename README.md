# Mental Health Companion Chatbot 🧠

Welcome to the **Mental Health Companion Chatbot**! This application is designed to provide users with compassionate and accurate advice on various mental health topics using a combination of pre-existing mental health guidebooks and advanced language models.

## Features

- **Contextual Responses**: Provides responses based on a combination of user input and relevant documents.
- **Mental Health Guidance**: Offers information on wellness, coping strategies, emotional support, and more.
- **Interactive Chat Interface**: Users can interact with the chatbot using a friendly and intuitive interface.

## Requirements

Ensure you have the following dependencies installed:

- `gradio`
- `huggingface_hub`
- `PyMuPDF` (for PDF handling)
- `sentence_transformers` (for embedding and search)
- `faiss` (for vector search)
- `numpy`

You can install these dependencies using pip:

```bash
pip install gradio huggingface_hub pymupdf sentence_transformers faiss-cpu numpy


Building a Retrieval-Augmented Generation (RAG) bot can significantly enhance the capabilities of a language model by incorporating external knowledge to generate more accurate and contextually relevant responses. This guide will walk you through creating a simple RAG bot using Gradio and the Hugging Face APIs.

But how does RAG enhance LLM’s performance?

RAG improves the performance of language models by augmenting them with external documents. This method retrieves relevant documents based on the user query and combines them with the original prompt before passing them to the language model for response generation. This approach ensures that the language model can access up-to-date and domain-specific information without the need for extensive retraining.



A common scenario of RAG helping LLM (Source)

The basic steps in RAG can be simplified as follows:

Input: The question to which the LLM system responds is referred to as the input. If no RAG is used, the LLM is directly used to respond to the question.

Indexing: If RAG is used, then a series of related documents are indexed by chunking them first, generating embeddings of the chunks, and indexing them into a vector store. At inference, the query is also embedded in a similar way.


Basic retrieval steps in RAG. (Source)

Retrieval: The relevant documents are obtained by comparing the query against the indexed vectors, also denoted as “Relevant Documents”.

Generation: The relevant documents are combined with the original prompt as additional context. The combined text and prompt are then passed to the model for response generation which is then prepared as the final output of the system to the user.

In the example provided, using the model directly fails to respond to the question due to a lack of knowledge of current events. On the other hand, when using RAG, the system can pull the relevant information needed for the model to answer the question appropriately. (Source)

Now Let’s Build a Chatbot using RAG:

I have used Zephyr LLM model and all-MiniLM-L6-v2 sentence transformer model. This sentence-transformers model maps sentences & paragraphs to a 384 dimensional dense vector space and can be used for tasks like clustering or semantic search.

The all-* models were trained on all available training data (more than 1 billion training pairs) and are designed as general purpose models. The all-mpnet-base-v2 model provides the best quality, while all-MiniLM-L6-v2 is 5 times faster and still offers good quality. Toggle All models to see all evaluated original models.

We need the following ingredients:

1. A PDF as your knowledgebase

2. A requirements.txt file

3. An app.py file

4. An account on Hugging Face (See this blog to learn about building a LLM chatbot in Hugging Face)
