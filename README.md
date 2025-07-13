# Multi-Agentic Conversational AI System

An intelligent, multilingual, and multi-modal assistant powered by Retrieval-Augmented Generation (RAG), Gemini LLM, a CRM database, and calendar integration.

---

## 🚀 Features Implemented

### 🔹 Gemini Chat Endpoint (`/chat/gemini`)

* Handles dynamic user queries.
* NLP-based intent detection (greeting, unrelated, calendar intent).
* Integrates:

  * **RAG** for contextual answers.
  * **Gemini LLM** to generate responses.
  * **Calendar Scheduling** (with conflict checking).
  * **Multi-language Support** (translates queries and responses).
* Logs conversations and classifies with tags.

**Example Test:**

```json
{
  "user_id": "test123",
  "message": "Schedule a meeting with John tomorrow at 3pm for updates."
}
```

---

### 🔹 Upload Document Endpoint (`POST /upload_docs/`)

* Uploads `.pdf`, `.txt`, `.csv`, `.doc`, `.docx` files.
* Indexes content into FAISS vector store using LangChain.

**Test with Swagger:**
Upload a supported file and check for `"File uploaded and processed successfully"`.

---

### 🔹 Calendar API

* **Create Event (auto from chat)**
* **Conflict Detection:** Same-time event not allowed.
* **Update, Fetch, and Delete User Events**

**Endpoints:**

* `POST /calendar/create_event`
* `GET /calendar/user_events/{user_id}`
* `PUT /calendar/update_event/{event_id}`
* `DELETE /calendar/delete_event/{event_id}`

---

### 🔹 User Management

* Create guest or registered users.
* `POST /user/create_user`
* `GET /user/get_user/{user_id}`
* `PUT /user/update_user/{user_id}`
* `DELETE /user/delete_user/{user_id}`

---

### 🔹 Conversation History + Tag Management

* Stores chat logs in MongoDB.
* Filtered by tags or user ID.

**Endpoints:**

* `GET /conversation/user/{user_id}`
* `GET /conversation/filter?tag=calendar`
* `PUT /conversation/update_tags/{conversation_id}`
* `DELETE /conversation/delete_user_conversations/{user_id}`

---

## 🧠 RAG Service (Retrieval-Augmented Generation)

* Uses `faiss-cpu` + LangChain for indexing.
* Dynamically extracts context and checks scope using Gemini.
* Uses Google Generative AI Embeddings.

### Indexing Supported:

* PDF, TXT, CSV, DOC, DOCX

---

## 🌐 Language Support

* Auto-detects language.
* Translates input to English before processing.
* Translates output back to original language.

---

## 🔧 Development Stack

* **Backend:** FastAPI, Python
* **LLM:** Gemini via `google-generativeai`
* **RAG:** LangChain + FAISS
* **NLP:** Custom `analyze_intent` function
* **Multilingual:** `langdetect`, `deep-translator`
* **Document Parsing:** `pypdf`, `python-docx`, `pandas`
* **Database:** MongoDB

---

## 🧪 Testing Endpoints

Use Swagger at `http://localhost:8000/docs` or Postman with the following:

```http
POST /chat/gemini
{
  "user_id": "test123",
  "message": "What is the lowest rent for Broadway properties?"
}
```

```http
POST /upload_docs/
Form-data:
  file: sample.csv
```

```http
GET /calendar/user_events/test123
```

---

## 📂 File Structure

```
app/
├── main.py
├── routers/
│   ├── chat_gemini_router.py
│   ├── calendar_router.py
│   ├── upload.py
│   └── user_router.py
├── services/
│   ├── rag_service.py
│   ├── calendar_service.py
│   ├── gemini_service.py
│   ├── language_service.py
│   └── logger_service.py
├── schemas/
│   └── crm_schema.py
```

---

## 📦 Installation

```bash
pip install -r requirements.txt
```


---



---



---


