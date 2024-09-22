# Q&A System Using Semantic Search

## Overview

This project, titled **Q&A System Using Semantic Search**, aims to build an intelligent question-answering system leveraging semantic search. The goal is to find the most relevant answers to user queries from a large dataset using embeddings, similarity search, and efficient vector search techniques.

The project integrates various technologies, including pre-trained language models from Vertex AI, to embed and process textual data. It also employs approximate nearest neighbor search (ANN) algorithms like ScaNN to handle large datasets efficiently by clustering data and performing quick vector-based searches.

## Project Breakdown

### 1. **Dataset Overview**
   - The project uses a Stack Overflow (SO) questions and answers dataset (`so_database_app.csv`), which includes technical questions and their respective answers.
   - The dataset was pre-processed to convert questions into embeddings for semantic search.

### 2. **Embeddings and Vector Representation**
   - **Embeddings**: The system relies on embeddings, which transform text into high-dimensional vector representations that capture the semantic meaning of the text.
   - **Pre-trained Model**: We use a pre-trained embedding model from Vertex AI, `textembedding-gecko@001`, to generate embeddings for both user queries and the database of Stack Overflow questions.
   - **Cosine Similarity**: When a user submits a query, the system computes the cosine similarity between the query's embedding and all the question embeddings in the dataset. This helps in identifying the most similar (or semantically related) question.

### 3. **Search Process**
   - When a user asks a question, the system:
     1. Embeds the user's query.
     2. Compares the query embedding with pre-embedded Stack Overflow questions using cosine similarity.
     3. Returns the question with the highest similarity score, assuming it is the most relevant to the user's query.

### 4. **Handling Large Datasets with ScaNN**
   - **ScaNN (Scalable Nearest Neighbors)**: For large datasets, calculating cosine similarity with every possible question becomes computationally expensive. To overcome this, we use ScaNN, which is an efficient method for approximate nearest neighbor (ANN) search.
   - **Indexing for Speed**: ScaNN creates an index of the dataset by clustering the embeddings. This reduces the search space, allowing for faster retrieval of the most similar questions.
   - **Efficiency**: By using ScaNN, the system significantly reduces the time needed to find relevant questions, especially as the dataset grows larger.

### 5. **Response Generation with LLM**
   - Once the most relevant question is found, the corresponding answer from Stack Overflow is retrieved.
   - **LLM Integration**: We use a pre-trained text generation model (`text-bison@001`) to generate a more conversational and user-friendly response, based on the relevant question-answer pair.
   - **Fallback Logic**: If the system doesn't find a good match from the database, the LLM returns a response indicating that no relevant information could be found.

### 6. **Comparison of Methods**
   - The project demonstrates two approaches:
     1. **Brute-Force Search**: Uses cosine similarity across the entire dataset for small-scale searches.
     2. **ANN Search (ScaNN)**: Optimizes large-scale searches with approximate clustering and efficient retrieval, significantly reducing query processing time.

## Key Technologies Used
- **Vertex AI**: For text embedding and text generation models.
- **Cosine Similarity**: To measure semantic similarity between the query and the dataset.
- **ScaNN (Approximate Nearest Neighbor Search)**: For fast, scalable, and efficient search over large datasets.
- **Pandas, Scikit-learn**: For data processing and similarity calculations.

