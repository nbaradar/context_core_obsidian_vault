This is an extremely simple POC that will allow you to make a query to multiple LLMs
https://github.com/nbaradar/multiquery

## CHAT GPT DESCRIPTION AS OF FEB 5
### **MultiQuery Overview**

#### **1. Purpose**

- **MultiQuery** is an expansion of your **Proof of Concept**, now turning into a **prototype**.
- It serves as a **unified interface** to interact with multiple **Large Language Models (LLMs)**, including **ChatGPT, Grok, and Gemini**.
- The application allows:
    - **Querying multiple LLMs** concurrently.
    - **Storing query history** and results in **MongoDB**.
    - **Exporting query responses** in different formats.

---

### **2. Architecture**

Your application consists of **three major subsystems**:

1. **MultiQuery (Backend & API Layer - FastAPI)**
    - Handles requests for querying LLMs.
    - Stores query results in a MongoDB database.
    - Provides endpoints for querying, history retrieval, and exporting results.
2. **Context Store (MongoDB)**
    - Stores query logs and responses for future reference.
3. **User Interface (React Frontend)**
    - Allows users to submit queries and view LLM responses in a structured way.
    - Provides an interface for selecting which LLMs to use.

---

### **3. Backend (FastAPI)**

#### **3.1 Overview**

The backend is implemented using **FastAPI**, an asynchronous Python framework. It provides:

- **Query execution** (`/query` endpoint).
- **Query history retrieval** (`/history` endpoint).
- **Result exporting** (`/export` endpoint).
- **Database interaction with MongoDB** (using `motor` for async operations).
- **Dynamic LLM Provider selection** (via `ProviderFactory`).

#### **3.2 Key Backend Components**

##### **🔹 API Layer**

- **`multiquery/api/endpoints/query.py`**:
    
    - Main query endpoint (`/query`) accepts user queries.
    - **Selects and queries LLM providers concurrently** using `asyncio.gather()`.
    - **Saves results in MongoDB** after execution.
    - Has a **potential logic issue** where results might not match provider names correctly.
- **`multiquery/api/endpoints/history.py`**:
    
    - Provides query history.
- **`multiquery/api/endpoints/export.py`**:
    
    - Placeholder for exporting stored query results.

##### **🔹 Core Services**

- **`multiquery/core/services/llm_service.py`**:
    
    - Handles LLM query execution.
    - Uses **async API calls** to different LLM providers.
- **`multiquery/core/services/query_db_service.py`**:
    
    - Saves query results in MongoDB.

##### **🔹 LLM Provider Abstraction**

- **`multiquery/llm_providers/base.py`**:
    
    - Defines an abstract `LLMProvider` class, which all providers inherit.
- **`multiquery/llm_providers/provider_factory.py`**:
    
    - Dynamically loads and creates provider instances.
    - Uses reflection (`importlib.import_module`) to instantiate provider classes based on the config.
- **Individual Providers:**
    
    - **`chatgpt.py`**
    - **`grok.py`**
    - **`gemini.py`**
    - Each provider:
        - **Implements `send_query()`** for asynchronous execution.
        - Reads API keys from `config.yaml`.

##### **🔹 Configuration & Database**

- **`config.yaml`**:
    
    - Defines LLM provider settings (API keys, models, etc.).
    - Configures MongoDB connection details.
- **`mongodb_client.py`**:
    
    - Handles database connection.

---

### **4. Frontend (React)**

#### **4.1 Overview**

- Built with **React + TailwindCSS + DaisyUI**.
- Uses **Axios** to send API requests to the backend.
- Displays query results in a structured, **chat-like UI**.

#### **4.2 Key Components**

- **`App.jsx`**:
    
    - Manages application state (`query`, `results`, `activeProviders`).
    - Handles **query submission** (`handleSendQuery`).
    - Dynamically renders LLM provider response cards.
- **`api.js`**:
    
    - Contains functions to send queries to the backend (`fetchResults`).
- **Main UI Components:**
    
    - **`QueryDisplay.jsx`** → Displays active providers and user queries.
    - **`ResultsWindow.jsx`** → Renders responses from LLMs.
    - **`ResultCard.jsx`** → Displays individual LLM responses.
    - **`InputSection.jsx`** → Provides an input field and provider selection UI.

---

### **5. Next Steps & Improvements**

#### **🔹 Backend Fixes & Enhancements**

✅ **Fix response-provider matching issue** in `query.py` (bug in how results are assigned to providers).  
✅ **Improve error handling** for failed API requests (e.g., invalid API keys, timeout handling).  
✅ **Implement query filtering & context types** (allow different provider selections based on query type).

#### **🔹 Frontend Enhancements**

✅ **Improve response visualization** (consider adding expandable responses).  
✅ **Improve chat history handling** (persist past queries for better UX).  
✅ **Introduce user authentication** (to store user-specific query logs).

---

### **Final Thoughts**

Your **MultiQuery** project is well-structured and modular, making it easy to expand. It provides a **scalable approach to LLM integration**, allowing users to query multiple models efficiently. You're now at a stage where you can **refine the logic, optimize the UX, and improve error handling** before expanding further.

Let me know what you want to focus on next! 🚀


## Temporary Notes
##### Next Steps
- Add more fine-tuned control to LLM settings and expose them to user
- Add export function
- Add ability to select different LLM versions (list out versions)
- Create UI

--- 

%% Begin Waypoint %%
- [[ChatGPT API]]
- [[Concurrency]]
- [[CORS To run Frontend+Backend]]
- [[Dev Notes]]
- [[Export]]
- [[Grok API]]
- [[Integrating MongoDB]]

%% End Waypoint %%

#multiquery