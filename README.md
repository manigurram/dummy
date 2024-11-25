# Text Search System Using KE-Sieve

## Objective
The goal of this project is to develop an efficient text search system using KE-Sieve on textual data collected from CRISIL. The system leverages advanced embeddings, KE-Sieve indexing, and binary flat indexing to retrieve the most relevant text passages.

---

## Dataset
The dataset consists of:
- **Source**: 20 PDFs.
- **Processed Data**: 30,542 passages, extracted and preprocessed to build the KE-Sieve model.

---

## Pipeline Overview

### **Training Pipeline**
1. **Download the Data**: Collect CRISIL text data in PDF format.
2. **Data Extraction**: Extract text from PDFs using [LangChain](https://github.com/hwchase17/langchain).
3. **Data Preprocessing**: Clean and preprocess the extracted text for embedding generation.
4. **Generate Embeddings**: Use the **Azure OpenAI `text-embedding-3-small` model** for high-quality embeddings.
5. **Build KE-Sieve Model**: Create Orientation Vectors (OVs) and Packbits.
6. **Build the Index**: Use FAISS Binary Flat Index for indexing OVs.
7. **Save the Model**: Persist the model and index for future use.

### **Testing Pipeline**
1. **Input Text**: Provide a query text input.
2. **Generate Embeddings**: Compute embeddings for the input text.
3. **Compute OVs and Packbits**: Prepare the Orientation vector representation.
4. **Index Search**: Use FAISS to retrieve the top 5 nearest passage IDs.
5. **Retrieve Results**: Fetch and display the corresponding text passages.

---

## Install Dependencies

To set up the project, follow the steps below to install the required Python dependencies. It is recommended to create a virtual environment for isolation.

### 1. Create a virtual environment:

```bash
python -m venv env  # Create virtual environment
```

## Install Dependencies

Next, you need to install the required Python dependencies. It is recommended to create a virtual environment for this.

- Python 3.8 or higher
- GPU (optional, for faster embeddings and FAISS indexing)


1. Create a virtual environment:

    ```bash
    python -m venv env  # Create virtual environment
    ```

2. Activate the virtual environment (Linux/Mac):

    ```bash
    source env/bin/activate
    ```

3. Install the required packages listed in the `requirements.txt` file:

    ```bash
    pip install -r requirements.txt
    ```
## How to Obtain the Azure OpenAI API Key

To use the **Azure OpenAI Service** for generating embeddings, follow these steps:

1. **Sign Up for Azure**  
   - Visit [Azure Portal](https://azure.microsoft.com/) and log in with your Microsoft account. If you don’t have an account, create one.

2. **Create an Azure OpenAI Resource**  
   - Go to the **Azure Portal Dashboard**.  
   - Click **Create a resource** and search for **Azure OpenAI**.  
   - Select **Azure OpenAI** and click **Create**.  
   - Choose a subscription and resource group, and provide a name for the OpenAI resource.

3. **Select Pricing Tier**  
   - Select the pricing tier that matches your needs. For embedding generation, use the `text-embedding-3-small` model.

4. **Generate API Key**  
   - After the resource is created, go to the **Keys and Endpoint** section within the Azure OpenAI resource.  
   - Copy the **Primary Key** and the **Endpoint URL**.

5. **Set Up Environment Variables**  
   - Store the API key and endpoint securely as environment variables. For example:  
     ```bash
     export AZURE_OPENAI_API_KEY="your_primary_key"
     export AZURE_OPENAI_ENDPOINT="your_endpoint_url"
     ```

6. **Verify Your API Key**  
   - Test the API key using a simple Python script:  
     ```python
     import requests

     API_KEY = "your_primary_key"
     ENDPOINT = "your_endpoint_url"

     headers = {
         "Content-Type": "application/json",
         "Authorization": f"Bearer {API_KEY}",
     }

     data = {
         "model": "text-embedding-3-small",
         "input": "Test embedding generation",
     }

     response = requests.post(f"{ENDPOINT}/openai/deployments/text-embedding-3-small/embeddings", headers=headers, json=data)
     print(response.json())
     ```


## Running the Semantic Search API
To run the sText Search System, execute the following command:
```bash
streamlit run annual_report_search_kesieve.py
```
