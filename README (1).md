# Patient Case Summary RAG Application

## Overview

This application helps clinicians generate case summaries for patients by:
1. Extracting key details from patient data
2. Retrieving relevant clinical guidelines
3. Generating a comprehensive case summary with recommendations

The application is built using open-source tools and runs locally, making it accessible and free to use.

## Features

- **Patient Data Processing**: Upload FHIR JSON files to extract patient information
- **Medical Guidelines Management**: Add guidelines via text files or direct input
- **Case Summary Generation**: Generate comprehensive case summaries with recommendations
- **Interactive Interface**: User-friendly Streamlit interface for easy interaction

## Technical Implementation

This application replaces the proprietary components in the original notebook with open-source alternatives:

| Original Component | Open Source Alternative |
|-------------------|-------------------------|
| OpenAI models (gpt-4o, gpt-4o-mini) | Template-based approach with optional HuggingFace models |
| LlamaCloud for vector storage | ChromaDB |
| LlamaIndex components | LangChain |

## Project Structure

```
rag_app/
├── app.py                  # Main Streamlit application
├── data/
│   ├── create_sample_data.py  # Script to generate sample patient data
│   └── sample_patient.json    # Sample patient data for testing
└── src/
    ├── patient_parser.py      # Patient data parsing functionality
    ├── guideline_retriever.py # Vector storage and retrieval for guidelines
    ├── query_generator.py     # Query generation based on patient data
    └── rag_workflow.py        # Main RAG workflow implementation
```

## Installation

1. Clone the repository
2. Install the required packages:
   ```
   pip install streamlit langchain langchain-community chromadb pydantic python-dotenv
   ```
3. Run the application:
   ```
   streamlit run app.py
   ```

## Usage

### 1. Upload Patient Data

- Navigate to the "Upload Patient Data" tab
- Upload a FHIR JSON file containing patient data
- View the extracted patient information

### 2. Add Guidelines

- Navigate to the "Add Guidelines" tab
- Either upload text files containing guidelines or enter guideline text directly
- Alternatively, use the "Add Sample Guidelines" button to add pre-defined guidelines for testing

### 3. Generate Summary

- Navigate to the "Generate Summary" tab
- View the recommended queries generated based on patient information
- Click "Generate Case Summary" to process the patient data and generate recommendations
- View and download the generated case summary

## Customization

### Adding Custom Guidelines

You can add your own medical guidelines by:
1. Creating text files with guideline content
2. Uploading them through the "Add Guidelines" tab
3. Or entering guideline text directly in the text area

### Using a Different Embedding Model

To use a different embedding model, modify the `GuidelineRetriever` class in `src/guideline_retriever.py`:

```python
self.embeddings = HuggingFaceEmbeddings(
    model_name="your-preferred-model",  # Change this to your preferred model
    model_kwargs={'device': 'cpu'},
    encode_kwargs={'normalize_embeddings': True}
)
```

### Integrating with a Hugging Face LLM

If you have access to Hugging Face API, you can enable LLM-based summaries by setting the `HF_TOKEN` environment variable before running the application:

```
export HF_TOKEN=your_huggingface_token
streamlit run app.py
```

## Limitations

- The template-based approach for generating summaries is less sophisticated than using a full LLM
- The application requires local resources for vector storage and retrieval
- Performance may vary depending on the size of the guidelines database

## Future Improvements

- Add support for more patient data formats beyond FHIR
- Implement more sophisticated query generation
- Add visualization of patient data and trends
- Improve the summary generation with more advanced NLP techniques
