# PDF-enhanced-RAG

**PDF-enhanced-RAG** (Retrieval-Augmented Generation) is a pipeline that enables question-answering from a PDF document using the RAG framework. This setup combines LangChain components to retrieve information from a PDF document and uses OpenAI embeddings to answer questions based on the content of the document. The script is optimized for use with Azure OpenAI's API.

## Features

- Loads and processes PDF documents for information retrieval.
- Splits document content for optimized semantic search and retrieval.
- Uses retrieval-augmented generation (RAG) to answer questions based on document content.
- Powered by Azure OpenAI and LangChain for embedding, retrieval, and response generation.

## Prerequisites

- **Python 3.8** or higher
- **Azure OpenAI API key** and access to the Azure OpenAI deployment.
- PDF file (modify the default file path in the code as needed).

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/PDF-enhanced-RAG.git
   cd PDF-enhanced-RAG
   ```

2. **Install Dependencies**:
   Install dependencies with `pip`:
   ```bash
   pip install -r requirements.txt
   ```
   
   Ensure the following packages are included in your `requirements.txt` or install them directly:
   ```bash
   pip install langchain-core langchain-community langchain-openai
   ```

3. **Environment Variables**:
   Set up environment variables required for Azure OpenAI. In the project root, create a `.env` file with the following details:

   ```env
   AZURE_OPENAI_API_KEY=your_azure_openai_api_key
   AZURE_OPENAI_ENDPOINT=your_azure_openai_endpoint
   AZURE_OPENAI_DEPLOYMENT_NAME=your_azure_openai_deployment_name
   AZURE_OPENAI_API_VERSION=your_azure_openai_api_version
   ```

## Usage

The following steps outline the main actions performed by the script in `main.py`:

1. **Load and Process the PDF**:
   The script loads a PDF file (`data/nke-10k-2023.pdf` by default) using `PyPDFLoader`, extracts content, and prints a snippet and metadata of the first page.

2. **Initialize Language Model and Vector Store**:
   - **Azure OpenAI** is used for embedding and question-answering, with credentials provided through environment variables.
   - **RecursiveCharacterTextSplitter** splits PDF content into manageable chunks to ensure better retrieval quality.
   - These chunks are embedded and stored in an in-memory vector store for similarity-based retrieval.

3. **Define Prompt and Retrieval-Augmented Generation (RAG) Chain**:
   - A concise prompt is created to guide responses from the language model, directing the model to answer questions based on the retrieved context.
   - The **retrieval-augmented generation (RAG) pipeline** first retrieves relevant document chunks, then generates answers using both retrieved context and the question.

4. **Ask Questions**:
   Run the script and test it with sample questions such as:
   ```bash
   python main.py
   ```
   Example output:
   ```plaintext
   Answer: "Nike's revenue in 2023 was..."
   Context: "Page content of the relevant answer..."
   Metadata: { ... }
   ```

   You can modify the input question directly in `main.py` to test different queries.

## Example

To query information about Nike's revenue in 2023, the script automatically runs with the question:
```plaintext
What was Nike's revenue in 2023?
```

The response provides both the answer and relevant context from the document.

## Project Structure

- **main.py**: Main script for loading the PDF, setting up the RAG pipeline, and running queries.
- **data/**: Folder where the PDF document (`nke-10k-2023.pdf`) should be placed.

## Contributing

Contributions are welcome! If you find a bug or have an improvement idea, please fork the repository and create a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Acknowledgments

- [LangChain](https://github.com/hwchase17/langchain): For providing a robust framework to build retrieval and generation pipelines.
- [Azure OpenAI](https://azure.microsoft.com/en-us/services/openai/): For providing access to OpenAI models for embedding and generation.
