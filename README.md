# Intelligent PDF Summarizer

This project demonstrates how to build a serverless document summarization pipeline using **Azure Durable Functions**, **Azure Blob Storage**, **Azure Form Recognizer**, and **Azure OpenAI**.

Uploaded PDF files are processed automatically:
1. Text is extracted using Azure Form Recognizer.
2. The extracted content is summarized using Azure OpenAI.
3. The summary is saved back to Azure Blob Storage as a `.txt` file.

---

##  Architecture Overview

- **Azure Blob Storage**: Stores input PDFs and output summaries.
- **Azure Durable Functions**: Orchestrates the flow.
- **Form Recognizer**: Extracts text from PDFs.
- **Azure OpenAI**: Generates a summary of the extracted text.

---

## Setup 

##  Local Development Setup
### 1. Clone and Set Up Virtual Environment

```bash
git clone https://github.com/<your-repo>/Intelligent-PDF-Summarizer.git
cd Intelligent-PDF-Summarizer
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```
### 2.  Start Azurite (Local Run)
```azurite
```
### 3. local.settings.json (Local Run)
```
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "BLOB_STORAGE_CONNECTION_STRING": "AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;DefaultEndpointsProtocol=http;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;",
    "COGNITIVE_SERVICES_ENDPOINT": "https://pdf-formrec.cognitiveservices.azure.com/",
    "COGNITIVE_SERVICES_KEY": "9fxdiMVGg3MKi6r7EAMMo0hlBORqETkeXBlDbJyd6ruHaW4kG3qJJQQJ99BFACBsN54XJ3w3AAALACOGqmHt",
    "AZURE_OPENAI_ENDPOINT": "https://desa0-mc4woh2d-swedencentral.cognitiveservices.azure.com/openai/deployments/my-gpt-4/chat/completions?api-version=2025-01-01-preview",
    "AZURE_OPENAI_KEY": "3SvqVzBxvNQYuB8z4Meg5LuymKEpjbdcX0mPFaWEzl9uO8DjSlcQJQQJ99BFACfhMk5XJ3w3AAAAACOGzbqt",
    "CHAT_MODEL_DEPLOYMENT_NAME": "my-gpt-4"
  }
}
```
### 4.Start the Azure Functions host
```
func start --verbose ```
---
##  Local Development Setup
### 1. Clone and Set Up Virtual Environment

```bash
git clone https://github.com/<your-repo>/Intelligent-PDF-Summarizer.git
cd Intelligent-PDF-Summarizer
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 3. local.settings.json (Local Run)
```
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "BLOB_STORAGE_CONNECTION_STRING": "AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;DefaultEndpointsProtocol=http;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;",
    "COGNITIVE_SERVICES_ENDPOINT": "https://pdf-formrec.cognitiveservices.azure.com/",
    "COGNITIVE_SERVICES_KEY": "9fxdiMVGg3MKi6r7EAMMo0hlBORqETkeXBlDbJyd6ruHaW4kG3qJJQQJ99BFACBsN54XJ3w3AAALACOGqmHt",
    "AZURE_OPENAI_ENDPOINT": "https://desa0-mc4woh2d-swedencentral.cognitiveservices.azure.com/openai/deployments/my-gpt-4/chat/completions?api-version=2025-01-01-preview",
    "AZURE_OPENAI_KEY": "3SvqVzBxvNQYuB8z4Meg5LuymKEpjbdcX0mPFaWEzl9uO8DjSlcQJQQJ99BFACfhMk5XJ3w3AAAAACOGzbqt",
    "CHAT_MODEL_DEPLOYMENT_NAME": "my-gpt-4"
  }
}
```
### 4.Start the Azure Functions host
```
func start --verbose ```
