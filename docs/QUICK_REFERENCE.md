# Quick Reference Guide

## 🚀 Quick Start

### Installation
```bash
pip install -r requirements.txt
export GROQ_API_KEY="your_api_key"
python main.py
```

### Configuration
```python
# main.py
HARDCODED_FOLDER_PATH = "./Insurance PDFs"  # Document folder
SUPPORTED_EXTENSIONS = {'.pdf', '.docx', '.txt', '.doc', '.md'}
```

## 📁 File Structure
```
LLM_RAG_Agent/
├── main.py                 # Main application
├── requirements.txt        # Dependencies
├── README.md              # Main documentation
├── docs/                  # Documentation folder
│   ├── ARCHITECTURE.md    # Technical architecture
│   ├── API_REFERENCE.md   # API documentation
│   ├── DEPLOYMENT.md      # Deployment guide
│   ├── USER_GUIDE.md      # User guide
│   └── QUICK_REFERENCE.md # This file
└── Insurance PDFs/        # Document storage
    ├── policy_1.pdf
    ├── policy_2.docx
    └── ...
```

## 🔧 Core Functions

### Document Loading
```python
# Load PDF
documents = load_pdf("file.pdf")

# Load Word document
documents = load_docx("file.docx")

# Load text file
documents = load_txt("file.txt")

# Load all from folder
documents = load_documents_from_folder("./Insurance PDFs")
```

### Vector Database
```python
# Build vector store
vectorstore = build_vectorstore(documents)

# Search similar documents
results = vectorstore.similarity_search("query", k=3)
```

### Query Processing
```python
# Process user query
response = ques_responses(
    question="What is the deductible?",
    history=[],
    system_prompt="You are Meera, an insurance expert.",
    token_limit=150
)
```

## ⚙️ Configuration Variables

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `GROQ_API_KEY` | str | Required | Groq API key |
| `HARDCODED_FOLDER_PATH` | str | `"./Insurance PDFs"` | Document folder |
| `SUPPORTED_EXTENSIONS` | set | `{'.pdf', '.docx', '.txt', '.doc', '.md'}` | File types |


## 🔍 Troubleshooting

### Common Issues

| Issue | Solution |
|-------|----------|
| API Key Error | Verify `GROQ_API_KEY` environment variable |
| No Documents Found | Check `HARDCODED_FOLDER_PATH` and file extensions |
| Memory Issues | Reduce chunk size or increase system RAM |
| Port Conflicts | Change port: `gr.ChatInterface(...).launch(server_port=7861)` |
| Model Download Fail | Clear cache: `rm -rf ~/.cache/huggingface` |

### Performance Tuning
```python
# Reduce memory usage
splitter = RecursiveCharacterTextSplitter(
    chunk_size=300,  # Smaller chunks
    chunk_overlap=30
)

# Faster responses
retriever_docs = db.similarity_search(question, k=2)  # Fewer results
```

## 🔐 Security

### API Key Management
```python
# Environment variable (recommended)
export GROQ_API_KEY="your_key"


### Custom Prompts
```python
custom_template = """
You are an insurance expert. Answer based on this context:

Context: {context}
Question: {question}

Answer:
"""

custom_prompt = PromptTemplate(
    input_variables=["context", "question"],
    template=custom_template
)
```

## 📞 Support

### Error Reporting
- **Technical Issues**: Check logs in `meera.log`
- **API Issues**: Verify Groq API key and credits
- **Performance**: Monitor memory and CPU usage
- **Documentation**: See full docs in `docs/` folder

### Useful Commands
```bash
# Check system resources
htop
free -h
df -h

# Test API key
curl -H "Authorization: Bearer $GROQ_API_KEY" \
  https://api.groq.com/openai/v1/models
```

---

**Version**: 1.0.0  
**Last Updated**: August 2025 
**For full documentation**: See `docs/` folder
