# 🎬 AI Video Assistant

> **Transcribe · Summarise · Extract Insights · Chat with Your Meetings**

AI Video Assistant is an AI-powered meeting/video analysis application built with **Python and Streamlit**. It can take a YouTube video or local audio/video file, convert it into text, generate an intelligent summary, identify action items and decisions, and let you **ask questions about the meeting using RAG (Retrieval-Augmented Generation)**.

---

## ✨ Features

* 🎥 **YouTube Video Support** — Analyse videos directly from a YouTube URL
* 📁 **Local File Support** — Process local audio/video files
* 🎙️ **AI Transcription**

  * English → OpenAI Whisper
  * Hinglish → Sarvam AI Speech-to-Text Translation
* 📝 **Automatic Meeting Summary**
* 🏷️ **AI-Generated Meeting Title**
* ✅ **Action Item Extraction**

  * Task description
  * Responsible owner
  * Deadline when available
* 🔑 **Key Decision Extraction**
* ❓ **Open Question / Follow-up Detection**
* 🧠 **RAG-powered Meeting Chat**
* 🔍 **Semantic Search over Transcripts**
* 💾 **Local Chroma Vector Database**
* 🖥️ **Modern Streamlit Interface**
* 📊 **Pipeline Status Tracking**
* 💬 **Interactive Chat History**

---

## 🛠️ Tech Stack

### Frontend

* **Streamlit**
* Custom CSS
* Responsive dashboard layout

### Backend

* **Python**
* Modular pipeline architecture

### AI / LLM

* **OpenAI Whisper** — English transcription
* **Sarvam AI** — Hinglish transcription and English translation
* **Mistral AI** — Summarisation, title generation, extraction and Q&A
* **LangChain** — LLM orchestration and RAG pipeline

### Vector Search

* **ChromaDB**
* **HuggingFace Embeddings**
* `all-MiniLM-L6-v2`

### Audio Processing

* **yt-dlp** — YouTube audio extraction
* **Pydub** — Audio conversion and chunking
* **FFmpeg** — Audio/video processing

---

## 🔄 How It Works

```text
             YouTube URL / Local File
                       │
                       ▼
              ┌─────────────────┐
              │ Audio Processing│
              └────────┬────────┘
                       │
                       ▼
                Audio Chunking
                       │
                       ▼
              ┌─────────────────┐
              │  Transcription  │
              │                 │
              │ Whisper /       │
              │ Sarvam AI       │
              └────────┬────────┘
                       │
                       ▼
                  Transcript
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      Summary      Extraction    Title
                       │
              ┌────────┼────────┐
              ▼        ▼        ▼
           Actions Decisions Questions
                       │
                       ▼
              Chroma Vector Store
                       │
                       ▼
                 RAG Retriever
                       │
                       ▼
                Mistral AI Q&A
                       │
                       ▼
                 Meeting Chat
```


---

## 🎥 Using the Application

### Step 1 — Provide Input

Enter either:

```text
https://www.youtube.com/watch?v=VIDEO_ID
```

or a local file path:

```text
C:/Videos/meeting.mp4
```

### Step 2 — Select Language

Choose:

* `English`
* `Hinglish`

### Step 3 — Click Analyse

The application runs the following pipeline:

```text
Audio Processing
      ↓
Transcription
      ↓
Title Generation
      ↓
Summarisation
      ↓
Insight Extraction
      ↓
RAG Engine
```

### Step 4 — Review Results

The application displays:

* 📌 Meeting title
* 📋 Summary
* 📝 Full transcript
* ✅ Action items
* 🔑 Key decisions
* ❓ Open questions

### Step 5 — Chat With Your Meeting

Ask questions such as:

```text
What were the main decisions made?
```

```text
Who was responsible for the deployment?
```

```text
What tasks were assigned?
```

```text
Were there any unresolved issues?
```

The RAG system retrieves relevant transcript chunks before sending the context to Mistral AI.

---

# 🧠 RAG Pipeline

The application uses **Retrieval-Augmented Generation** to answer questions based on the meeting transcript.

### 1. Split Transcript

The transcript is divided into smaller chunks using:

```text
RecursiveCharacterTextSplitter
```

### 2. Generate Embeddings

The project uses:

```text
all-MiniLM-L6-v2
```

to convert transcript chunks into vector embeddings.

### 3. Store Vectors

Embeddings are stored locally using:

```text
ChromaDB
```

### 4. Retrieve Relevant Context

For every user question, the retriever searches for the most relevant transcript chunks.

The application retrieves:

```text
Top 4 relevant chunks
```

### 5. Generate Answer

The retrieved context is provided to Mistral AI, which generates a concise answer based only on the meeting transcript.

---


## 🖥️ Interface

The application provides a dark-themed dashboard with:

```text
┌──────────────────────────────────────────────┐
│              AI VIDEO ASSISTANT              │
│        Transcribe · Summarise · Chat        │
├──────────────────┬───────────────────────────┤
│ Input            │ Session Title             │
│                  ├───────────────────────────┤
│ YouTube / File   │ Summary                   │
│                  │                           │
│ Language         │ Transcript                │
│                  │                           │
│ Analyse          ├───────────────────────────┤
│                  │ Actions | Decisions | Qs  │
│ Pipeline Status  │                           │
│                  ├───────────────────────────┤
│                  │ 💬 Chat with Meeting      │
└──────────────────┴───────────────────────────┘
```

---
