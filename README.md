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

🧪 Testing Endpoints
Use Swagger UI at http://localhost:8000/docs or test via Postman using the examples below:

📬 Chat with Gemini (RAG + Calendar + Language Support)
POST /chat/gemini

json
Copy
Edit
{
  "user_id": "test123",
  "message": "What is the lowest rent for Broadway properties?"
}
Calendar scheduling (with conflict check)

json
Copy
Edit
{
  "user_id": "test123",
  "message": "Schedule a meeting with John tomorrow at 3pm"
}
Greeting intent

json
Copy
Edit
{
  "user_id": "test123",
  "message": "Hi there!"
}
Multi-language input (translated automatically)

json
Copy
Edit
{
  "user_id": "test123",
  "message": "Hola, ¿cuál es la propiedad más barata?"
}
📤 Upload Documents (PDF, TXT, CSV, DOCX)
POST /upload_docs/
Form-Data:

file: (choose file like sample.csv or sample.pdf)

📅 Calendar Endpoints
GET /calendar/user_events/test123
Fetch all scheduled events for the user.

POST /calendar/create_event

json
Copy
Edit
{
  "user_id": "test123",
  "title": "Team Sync",
  "description": "Weekly sync-up",
  "datetime": "2025-07-20T10:00:00",
  "conversation_id": "abc-123"
}
PUT /calendar/update_event/<event_id>
Update event info:

json
Copy
Edit
{
  "title": "Team Sync Updated",
  "datetime": "2025-07-21T11:00:00"
}
DELETE /calendar/delete_event/<event_id>
Remove a scheduled calendar event.

👤 User Endpoints
POST /crm/create_user

json
Copy
Edit
{
  "user_id": "test123",
  "name": "Test User",
  "email": "test@example.com"
}
PUT /crm/update_user/test123

json
Copy
Edit
{
  "email": "updated@example.com"
}
DELETE /crm/delete_user/test123
Removes user and all related data.

💬 Conversation Management
GET /crm/conversations/test123
Get all conversations by a user.

GET /crm/conversations/filter_by_tag?tag=calendar
Filter all conversations tagged as "calendar".

PUT /crm/update_tag/<conversation_id>

json
Copy
Edit
{
  "new_tag": "important"
}
🧼 Reset the System
POST /reset
This will delete all:

Documents

Vectors

Users

Conversations

Calendar events

Use with caution in dev/testing environments.

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


