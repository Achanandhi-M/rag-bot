# Keploy Backend - Chat API

This project provides a backend API built with **FastAPI**, which allows users to ask technical questions about Keploy. It uses **Azure OpenAI** and **LangChain** for conversational AI and answers based on a vector database of MDX files.

## Features

- **Conversational API**: Users can ask technical questions related to Keploy, and the system provides answers using the information in MDX files.
- **Vector Database**: The app uses a vector database created from MDX files to retrieve relevant answers.
- **MongoDB Logging**: All queries and responses are logged into a MongoDB collection for later reference.
- **Asynchronous Operations**: MongoDB operations are asynchronous to ensure fast performance.

## Prerequisites

Before running the project, ensure you have the following installed:

- **Python 3.8+**
- **MongoDB Atlas** account (for cloud-based MongoDB service)
- **Azure OpenAI API Key** (for using GPT models)

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/keploy-chat-api.git
cd keploy-chat-api
````

### 2. Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables

Create a `.env` file in the root of the project directory and add the following variables:

```ini
uri=mongodb+srv://
AZURE_OPENAI_ENDPOINT=<your-azure-openai-endpoint>
OPENAI_API_VERSION=<your-openai-api-version>
AZURE_OPENAI_API_KEY=<your-azure-openai-api-key>
```

Replace the placeholders with your MongoDB URI and Azure OpenAI credentials.

### 5. Create the Vector Database

The vector database is created from MDX files. To set up the database:

1. Place your MDX files in the `docs/` folder.
2. The vector database will be automatically created when the application starts.

### 6. Start the Application

Run the FastAPI app using Uvicorn:

```bash
uvicorn app:app --reload
```

The application will start at `http://127.0.0.1:8000`.

### 7. Test the API

To test the `/chat` API, you can use a tool like  **cURL**. Here's an example of a **cURL** request:

```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/chat' \
  -H 'Content-Type: application/json' \
  -d '{
  "question": "What is Keploy?",
  "session_id": "unique-session-id"
}'
```

#### Sample Response:

```json
{
  "answer": "Keploy is an open-source testing tool...",
  "sources": [
    "Keploy Documentation",
    "Keploy API Reference"
  ]
}
```

If the answer is irrelevant, the response will only include:

```json
{
  "answer": "I am not sure about that."
}
```

### 8. Access the API Docs

FastAPI automatically generates interactive API documentation using **Swagger UI**. Visit:

```
http://127.0.0.1:8000/docs
```

You can also access the alternative ReDoc documentation at:

```
http://127.0.0.1:8000/redoc
```

## Directory Structure

```plaintext
keploy-chat-api/
│
├── docs/                  # MDX files for building the vector database
├── main.py                # FastAPI app and API logic
├── brain.py               # Custom functions for creating the vector database
├── requirements.txt       # Project dependencies
└── .env                   # Environment variables
```

## Troubleshooting

* **MongoDB Connection Issues**: Ensure that your MongoDB URI is correct.
* **Missing Environment Variables**: Check that all required environment variables are set in the `.env` file.
* **MDX File Parsing Errors**: Make sure the MDX files are correctly formatted and placed in the `docs/` folder.

## Contributing

If you'd like to contribute to this project, please fork the repository checkout our contribuion guide and submit a pull request. We welcome all contributions!