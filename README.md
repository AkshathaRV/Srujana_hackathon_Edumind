# AI Student Assistant Backend

This backend provides **personalized learning assistance** to students.
It supports **authentication, resume upload, quiz generation, scoring, and learning roadmaps** using **Supabase** (for storage) and **OpenAI/Gemini/Qwen** (for AI responses).

---

## Features

*  User registration & login (with JWT authentication)
*  Resume upload (PDF → text extraction → store in Supabase)
*  AI quiz generation (based on course or resume)
*  Quiz scoring & performance tracking
*  Personalized learning roadmap generation
*  Persistent student profile (memory across sessions)

---

##  Tech Stack

* **Flask** (Python backend framework)
* **Supabase** (Database & auth storage)
* **OpenAI / Gemini / Qwen API** (AI assistant & quiz generator)
* **PyMuPDF (fitz)** (Resume text extraction)

---

##  Project Structure

```
ai-student-assistant/
│── app.py             # Flask backend
│── uploads/           # Folder for uploaded resumes
│── requirements.txt   # Python dependencies
│── README.md          # Project documentation
```

---

##  Setup Instructions

### 1️ Clone the Repository

```bash
git clone https://github.com/your-repo/ai-student-assistant.git
cd ai-student-assistant
```

### 2️ Install Dependencies

```bash
pip install -r requirements.txt
```

If you don’t have a `requirements.txt`, create it:

```txt
flask
flask-cors
bcrypt
pyjwt
openai
supabase-py
pymupdf
```

### 3️ Configure Environment Variables

Create a `.env` file (or set directly in `app.py`) with:

```env
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-service-role-key
OPENAI_API_KEY=your-openai-or-gemini-key
SECRET_KEY=supersecretkey
```

### 4️ Setup Supabase Tables

In Supabase, create the following tables:

**users**

| Column   | Type          |
| -------- | ------------- |
| id       | uuid (PK)     |
| email    | text (unique) |
| password | text          |

**resumes**

| Column   | Type                  |
| -------- | --------------------- |
| id       | uuid (PK)             |
| user\_id | uuid (FK to users.id) |
| content  | text                  |

**scores**

| Column   | Type                  |
| -------- | --------------------- |
| id       | uuid (PK)             |
| user\_id | uuid (FK to users.id) |
| score    | int                   |
| total    | int                   |

---

##  Running the Server

```bash
python app.py
```

The backend will run at:

```
http://127.0.0.1:5000
```

---

##  API Endpoints

###  Authentication

* **POST /register** → `{ "email": "", "password": "" }`
* **POST /login** → `{ "email": "", "password": "" }`

###  Resume

* **POST /upload\_resume** → upload PDF (requires `Authorization` header with token)

###  Quiz

* **POST /generate\_quiz** → `{ "topic": "Python", "level": "beginner" }`
* **POST /score\_quiz** → `{ "answers": [], "correct": [] }`

###  Roadmap

* **POST /roadmap** → `{ "course": "Data Science", "level": "beginner" }`

---

##  Future Enhancements

* Add `/chat` endpoint (student → AI Q\&A)
* Support **file formats** beyond PDF (DOCX, TXT)
* Track detailed learning progress and suggestions

---

##  Author

Built for **personalized student learning assistance** using Python + Supabase + AI.
