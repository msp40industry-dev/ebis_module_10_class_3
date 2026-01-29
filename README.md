# 🔍 RAG Verification Agent - Automated Fact Checking

Intelligent agent that verifies claims using Retrieval-Augmented Generation (RAG) with local knowledge base and web search capabilities.

Part of Master's in Generative AI Engineering - EBIS Business Techschool
Module: Popular Frameworks and Libraries - Class 3

## 📋 Description

This project implements an AI agent that acts as an automated fact-checker. Given a claim or statement, the agent:

1. Searches a local vector database of trusted documents
2. Uses web search when needed for current information
3. Evaluates the claim's veracity using retrieved context
4. Returns: **True**, **False**, or **Insufficient Information**

The system combines RAG (Retrieval-Augmented Generation) with agentic reasoning to make intelligent decisions about information sources.

## 🎯 Features

* **Local Knowledge Base**: Wikipedia documents vectorized with OpenAI embeddings
* **Vector Search**: Qdrant for semantic similarity search
* **Web Search Integration**: Brave Search API for real-time information
* **Agentic Reasoning**: LangGraph orchestrates tool usage decisions
* **Structured Verification**: Clear True/False/Insufficient responses
* **Source Attribution**: Cites sources used for verification

## 🏗️ Architecture
```
User Claim
   ↓
Agent Decision Layer (LangGraph)
   ↓
   ├─→ Local Vector Search (Qdrant)
   │   ├─→ Retrieve relevant docs
   │   └─→ Calculate similarity scores
   │
   ├─→ Web Search (Brave Search API)
   │   ├─→ Query recent information
   │   └─→ Fetch external sources
   │
   └─→ LLM Verification (OpenAI GPT-4)
       ├─→ Analyze retrieved context
       ├─→ Cross-reference sources
       └─→ Return verdict + reasoning
```

## 🛠️ Tech Stack

- **LangChain**: RAG pipeline and agent framework
- **OpenAI**: GPT-4 for reasoning, embeddings for vectorization
- **Qdrant**: Vector database for semantic search
- **LangGraph**: Agent orchestration and tool routing
- **Brave Search API**: Web search integration
- **Wikipedia API**: Document retrieval
- **Python 3.8+**

## 🚀 Usage

Check the `rag_verification_agent.ipynb` notebook for the complete implementation.

### Example Outputs

**Example 1: Local Knowledge**
```
Claim: "The Eiffel Tower is located in Paris"
Verdict: ✅ TRUE
Reasoning: Multiple documents confirm the Eiffel Tower is an iron lattice 
           tower located on the Champ de Mars in Paris, France.
Sources: Wikipedia - Eiffel Tower
```

**Example 2: Contradiction Detection**
```
Claim: "The Eiffel Tower is 500 meters tall"
Verdict: ❌ FALSE
Reasoning: The Eiffel Tower measures 330 meters (1,083 ft) in height, 
           not 500 meters as claimed.
Sources: Wikipedia - Eiffel Tower
```

**Example 3: Insufficient Information**
```
Claim: "France's GDP in 2024 increased by 3%"
Verdict: ⚠️ INSUFFICIENT INFORMATION
Reasoning: Local knowledge base contains general France info but lacks 
           specific 2024 GDP data. Web search recommended.
Sources: None (requires current data)
```

## 📊 How It Works

### 1. Knowledge Base Creation

Wikipedia documents are loaded, converted to embeddings using OpenAI, and stored in Qdrant vector database for semantic similarity search.

### 2. Agent Tools

**Tool 1: Vector Search (Qdrant)**
- Searches local Qdrant database
- Returns most relevant document chunks
- Includes similarity scores

**Tool 2: Web Search (Brave)**
- Queries Brave Search API for current information
- Fetches reliable external sources
- Privacy-focused search results
- Used when local knowledge is insufficient

### 3. Verification Logic

The agent follows this reasoning process:

1. **Analyze claim**: Identify key entities and facts
2. **Search locally**: Query Qdrant vector database first
3. **Evaluate context**: Check if local docs are sufficient
4. **Web search (if needed)**: Fetch additional sources via Brave
5. **Cross-reference**: Compare information from multiple sources
6. **Generate verdict**: True/False/Insufficient with reasoning

## 💡 Key Concepts

**RAG (Retrieval-Augmented Generation)**
- Combines retrieval and generation for factual accuracy
- Reduces hallucinations by grounding in source documents
- Enables citing sources for transparency

**Vector Embeddings**
- Semantic representation of text
- Enables similarity search beyond keyword matching
- OpenAI's text-embedding-3-small model used

**Qdrant Vector Database**
- High-performance vector similarity search
- Efficient filtering and metadata support
- Scalable for production deployments

**Agentic Reasoning**
- Agent decides which tools to use
- LangGraph manages decision flow
- Autonomous information gathering

## 🎯 Use Cases

### Media & Journalism
- Automated fact-checking of news articles
- Real-time verification during breaking news
- Source validation for investigative reporting

### Social Media
- Misinformation detection
- Automated content moderation
- Flagging dubious claims for review

### Education
- Validating educational content
- Student assignment verification
- Research fact-checking

### Enterprise
- Internal document verification
- Compliance checking
- Knowledge base validation

## 📁 Project Structure
```
rag-verification-agent/
├── rag_verification_agent.ipynb  # Main notebook
├── qdrant_storage/               # Qdrant data (generated)
├── requirements.txt              # Dependencies
├── .env.example                  # Environment variables template
├── .gitignore
└── README.md
```

## ⚙️ Configuration

Required environment variables:
```env
OPENAI_API_KEY=your_openai_key
BRAVE_API_KEY=your_brave_search_key
QDRANT_URL=http://localhost:6333  # or cloud URL
```

### Setting up Qdrant

**Local (Docker)**:
```bash
docker pull qdrant/qdrant
docker run -p 6333:6333 qdrant/qdrant
```

**Cloud**: Use Qdrant Cloud free tier at https://qdrant.tech/

## 🔜 Potential Improvements

- [ ] Add multiple source validation (cross-reference 3+ sources)
- [ ] Implement confidence scores for verdicts
- [ ] Support for multiple languages
- [ ] Real-time news API integration
- [ ] Historical fact database
- [ ] Bias detection in sources
- [ ] User feedback loop for accuracy improvement
- [ ] Export verification reports (PDF/JSON)
- [ ] Web interface with Streamlit/Gradio
- [ ] Qdrant hybrid search (dense + sparse vectors)

## 🧪 Testing Examples

### Politics & History
- "Abraham Lincoln was the 16th President of the United States" → Expected: TRUE
- "World War II ended in 1950" → Expected: FALSE

### Science & Geography
- "Mount Everest is the tallest mountain on Earth" → Expected: TRUE
- "The Pacific Ocean is smaller than the Atlantic Ocean" → Expected: FALSE

### Current Events (requires web search)
- "The current inflation rate in the US is X%" → Expected: INSUFFICIENT or uses Brave Search

## 📚 References

- [LangChain Documentation](https://python.langchain.com/)
- [Qdrant Documentation](https://qdrant.tech/documentation/)
- [OpenAI Embeddings](https://platform.openai.com/docs/guides/embeddings)
- [Brave Search API](https://brave.com/search/api/)
- [LangGraph](https://langchain-ai.github.io/langgraph/)

## 📄 License

MIT License

## 👨‍💻 Author

Miguel - Master's in Generative AI Engineering @ EBIS Business Techschool

[LinkedIn](tu-perfil-linkedin) | [GitHub](tu-perfil-github)

---

⭐ If you find this project useful, give it a star on GitHub!
