# Text Search System Using KE-Sieve

## Objective
The goal of this project is to develop an efficient text search system using KE-Sieve on textual data collected from CRISIL. The system leverages advanced embeddings, KE-Sieve indexing, and binary flat indexing to retrieve the most relevant text passages.

---

## Dataset
The dataset consists of:
- **Source**: 20 PDFs.
- **Processed Data**: 30,542 passages, extracted and preprocessed to build the KE-Sieve model.

---

## Clone the model

First, you need to clone the BioBERT model from Hugging Face:

```bash
git clone https://huggingface.co/sentence-transformers/paraphrase-multilingual-mpnet-base-v2
```


## Pipeline Overview

### **Training Pipeline**
1. **Download the Data**: Collect CRISIL text data in PDF format.
2. **Data Extraction**: Extract text from PDFs using [LangChain](https://github.com/hwchase17/langchain).
3. **Data Preprocessing**: Clean and preprocess the extracted text for embedding generation.
4. **Generate Embeddings**: Use [paraphrase-multilingual-mpnet-base-v2] for text embeddings.
5. **Build KE-Sieve Model**: Create Orientation Vectors (OVs) and Packbits.
6. **Build the Index**: Use FAISS Binary Flat Index for indexing OVs.
7. **Save the Model**: Persist the model and index for future use.

### **Testing Pipeline**
1. **Input Text**: Provide a query text input.
2. **Generate Embeddings**: Compute embeddings for the input text.
3. **Compute OVs and Packbits**: Prepare the Orientation vector representation.
4. **Index Search**: Use FAISS to retrieve the top 5 nearest passage IDs.
5. **Retrieve Results**: Fetch and display the corresponding text passages.

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


## Running the Semantic Search API
To run the sText Search System, execute the following command:
```bash
streamlit run annual_report_search_kesieve.py
```
