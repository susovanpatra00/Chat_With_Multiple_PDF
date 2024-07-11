## Libraries Used

### Streamlit
- **Purpose:** Streamlit is used for creating interactive web applications. In this code, it is utilized to build a user interface for uploading PDF files and asking questions.
- **Usage:** `import streamlit as st`

### PyPDF2
- **Purpose:** PyPDF2 is a library for reading PDF files. It helps in extracting text from PDF documents.
- **Usage:** `from PyPDF2 import PdfReader`

### Langchain
- **Purpose:** Langchain is used for text processing and handling AI models. Specific modules from Langchain used in this code include text splitting, embeddings, vector stores, and question-answering chains.
- **Usage:**
  - `from langchain.text_splitter import RecursiveCharacterTextSplitter`
  - `from langchain.vectorstores import FAISS`
  - `from langchain.chains.question_answering import load_qa_chain`
  - `from langchain.prompts import PromptTemplate`

### Langchain-Google-GenAI
- **Purpose:** This library integrates Google’s Generative AI models with Langchain for generating embeddings and conversational models.
- **Usage:**
  - `from langchain_google_genai import GoogleGenerativeAIEmbeddings`
  - `from langchain_google_genai import ChatGoogleGenerativeAI`

### Google Generative AI
- **Purpose:** This library is used to configure and interact with Google’s Generative AI models.
- **Usage:** `import google.generativeai as genai`

### Dotenv
- **Purpose:** Dotenv is used for loading environment variables from a `.env` file. It helps in securely managing API keys and other sensitive information.
- **Usage:** `from dotenv import load_dotenv`

### OS
- **Purpose:** The OS module provides a way to interact with the operating system. It is used to retrieve environment variables.
- **Usage:** `import os`

## Functions

### `get_pdf_text(pdf_docs)`
- **Purpose:** Extracts text from a list of PDF documents.
- **Parameters:** `pdf_docs` - List of PDF files.
- **Returns:** Concatenated text extracted from all the pages of the provided PDFs.
- **Details:**
  - Loops through each PDF file.
  - Reads each page and extracts text using `PdfReader`.

### `get_text_chunks(text)`
- **Purpose:** Splits the extracted text into manageable chunks.
- **Parameters:** `text` - The text to be split.
- **Returns:** List of text chunks.
- **Details:**
  - Uses `RecursiveCharacterTextSplitter` to split the text.
  - Defines chunk size and overlap to ensure context continuity.

### `get_vector_store(text_chunks)`
- **Purpose:** Converts text chunks into a vector store for similarity search.
- **Parameters:** `text_chunks` - List of text chunks.
- **Details:**
  - Generates embeddings for each text chunk using `GoogleGenerativeAIEmbeddings`.
  - Stores the embeddings in a FAISS vector store.
  - Saves the vector store locally.

### `get_conversational_chain()`
- **Purpose:** Sets up a conversational chain for question answering.
- **Returns:** A question-answering chain.
- **Details:**
  - Defines a prompt template for the model.
  - Uses `ChatGoogleGenerativeAI` to load the conversational model.
  - Loads the QA chain using the defined model and prompt.

### `user_input(user_question)`
- **Purpose:** Handles user questions, searches for relevant documents, and generates responses.
- **Parameters:** `user_question` - The question input by the user.
- **Details:**
  - Loads the local FAISS index and searches for similar text chunks.
  - Uses the conversational chain to generate a detailed response.
  - Displays the response using Streamlit.

### `main()`
- **Purpose:** Main function to run the Streamlit application.
- **Details:**
  - Sets up the page configuration and header.
  - Provides an input box for user questions.
  - Handles file uploads and processing in the sidebar.
  - Calls the necessary functions to process PDFs and generate responses.
