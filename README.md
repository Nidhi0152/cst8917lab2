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
```
azurite
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
func start --verbose
 ```

---

##  Azure Cloud Development Setup
### 1. Clone and Set Up Virtual Environment

```bash
git clone https://github.com/<your-repo>/Intelligent-PDF-Summarizer.git
cd Intelligent-PDF-Summarizer
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. local.settings.json 
```
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "DefaultEndpointsProtocol=https;AccountName=desainidhistorage;AccountKey=KtK7JRMorFEo4yzaNdUz1Vt141kOWpRpwCJCnOke3dUUV1wXVLtZ1ZzDXNm+t3JIBc5BattokAgK+AStdM8Zvw==;EndpointSuffix=core.windows.net",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "BLOB_STORAGE_CONNECTION_STRING": "DefaultEndpointsProtocol=https;AccountName=desainidhistorage;AccountKey=KtK7JRMorFEo4yzaNdUz1Vt141kOWpRpwCJCnOke3dUUV1wXVLtZ1ZzDXNm+t3JIBc5BattokAgK+AStdM8Zvw==;EndpointSuffix=core.windows.net",
    "COGNITIVE_SERVICES_ENDPOINT": "https://pdf-formrec.cognitiveservices.azure.com/",
    "COGNITIVE_SERVICES_KEY": "9fxdiMVGg3MKi6r7EAMMo0hlBORqETkeXBlDbJyd6ruHaW4kG3qJJQQJ99BFACBsN54XJ3w3AAALACOGqmHt",
    "AZURE_OPENAI_ENDPOINT": "https://desa0-mc4woh2d-swedencentral.cognitiveservices.azure.com/openai/deployments/my-gpt-4/chat/completions?api-version=2025-01-01-preview",
    "AZURE_OPENAI_KEY": "3SvqVzBxvNQYuB8z4Meg5LuymKEpjbdcX0mPFaWEzl9uO8DjSlcQJQQJ99BFACfhMk5XJ3w3AAAAACOGzbqt",
    "CHAT_MODEL_DEPLOYMENT_NAME": "my-gpt-4"
  }
}
```
### 3.Start the Azure Functions host
```
func start --verbose
```

---
##  Challenges Faced

While deploying the solution using `azd up` from Visual Studio Code, I encountered a significant limitation. The Canada Central region was not available as an option during resource selection, so I selected an alternative region. However, deployment failed with the following error:
```
SubscriptionIsOverQuotaForSku: This region has quota of 0 ElasticPremium instances for your subscription.
ServiceModelDeprecated: The model 'Format:OpenAI, Name: gpt-35-turbo, Version:0613' has been deprecated.
```

This happened because my Azure subscription did not support creating resources like OpenAI and Form Recognizer in different regions or with the selected SKU.

## To resolve this:
- I manually created the required Azure resources.
- Updated the connection string in `local.settings.json`.
- Successfully tested the solution locally using Azurite.
- Created a summarized output by uploading a sample PDF to the `input` container.

---

##  Demo Videos

- Part 1 – Resource Setup and Local Testing
  ([https://youtu.be/demo-part1](https://youtu.be/JHdtdSmeuOY))
- Part 2 – Cloud setup
  ([https://youtu.be/demo-part2](https://youtu.be/cy68sUmtqqE))



