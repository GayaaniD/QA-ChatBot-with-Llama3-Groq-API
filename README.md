# QA-ChatBot-with-Llama3-Groq-API
![image](https://github.com/GayaaniD/QA-ChatBot-with-Llama3-Groq-API/assets/125920863/6b8eb4ea-6e58-4647-91f3-b28c8fb7f300)

This project is about building such a powerful Q&A chatbot using cutting-edge tools: Llama3 (large language model), LangChain (document processing framework), and Groq API (LLM interaction interface).

## How the Chatbot Works: From User Input to Insightful Answers 

1. Data Preparation :

A folder containing data in PDF format. The code assumes this folder is located at ./folder_name (adjust the path if needed).

2. User Interface (UI) :
![image](https://github.com/GayaaniD/QA-ChatBot-with-Llama3-Groq-API/assets/125920863/5a8f0352-17f6-49c9-b894-2ff6199e8fd0)

The Streamlit app provides a user-friendly interface with:
  - A title : “Chatgroq with Llama3”
  
  - A text input field : “Enter Your Question From Documents” for users to type their questions.
  
  - A button : “Documents Embedding” (initially clicked once to process the PDFs).
  
  - An answer section : Display the retrieved answer from the documents.
  
  - An expandable section : “Document Similarity Search” to show relevant document snippets.

3. Behind the Scenes :

  1. Document Processing (triggered by “Documents Embedding” button) :
    - This part runs only once to prepare the data for efficient retrieval.
    - If you haven't processed the documents yet and click the button:
      - The code creates an OpenAI embeddings object to generate numerical representations of text data.
      - It loads the PDFs from your data directory using the `PyPDFDirectoryLoader`.
      - It splits the large PDFs into smaller, more manageable chunks using the `RecursiveCharacterTextSplitter`. This helps the LLM process the data more efficiently.
      - It creates a vector store using FAISS. This allows for fast retrieval of similar documents based on their embeddings.
      - Finally, it generates embeddings for the document chunks and stores them in the FAISS vector store.
      - A message "Vector Store DB Is Ready" is displayed to indicate successful processing.

  2. User Question Processing (triggered when a question is entered) :
     - The code checks if the user has entered a question in the text input field.
     - If there's a question:
       - It creates a chain that processes the question using the Llama3 LLM. This chain uses a pre-defined prompt template that incorporates context (empty for now) and the user's question.
      - It retrieves relevant document chunks based on their similarity to the user's question using the FAISS vector store and the retriever interface.
      - It invokes the retrieval chain, passing the user's question as input.
      - The retrieval chain retrieves the most relevant document chunks and feeds them along with the original prompt template to the Llama3 LLM.
      - The LLM then processes the combined context (question and relevant document snippets) and generates an answer.
      - The retrieved answer is displayed in the UI.
      - Additionally, the "Document Similarity Search" section expands to show the page content of the retrieved document chunks, providing context for the answer.


## Overall Workflow :
  - The user enters a question related to the US census data.
  - If the documents haven’t been processed yet, the user clicks “Documents Embedding” to prepare the data (one-time step).
  - The code retrieves relevant document snippets based on the question’s similarity to the document embeddings.
  - The retrieved snippets are combined with the question and fed to the LLM to generate an answer.
  - The answer and relevant document snippets are displayed in the UI.
    
## Outcome :
![image](https://github.com/GayaaniD/QA-ChatBot-with-Llama3-Groq-API/assets/125920863/04beddac-5930-4656-8e44-f02d6807a682)
Here you can see , it shows the response and the relevant document from the response was extracted.

## The response time also very less : Response time : 0.078125
