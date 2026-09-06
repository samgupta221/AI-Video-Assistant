# 🎬 AI Video Assistant

> **Transcribe · Summarise · Extract Insights · Chat with Your Meetings**

AI Video Assistant is an AI-powered video analysis application built with **Python and Streamlit**. It can take a YouTube video or local audio/video file, convert it into text, generate an intelligent summary, identify action items and decisions, and let you **ask questions about the meeting using RAG (Retrieval-Augmented Generation)**.

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

## 🏗️ Project Architecture

```text
AI-Video-Assistant/
│
├── app.py                         # Streamlit application
├── main.py                        # CLI pipeline
├── test.py                        # Testing / pipeline example
├── Requirements.txt               # Python dependencies
│
├── core/
│   ├── transcriber.py             # Whisper & Sarvam transcription
│   ├── summarizer.py              # Title & summary generation
│   ├── extractor.py               # Action items, decisions, questions
│   ├── rag_engine.py              # RAG question-answering
│   └── vector_store.py            # Chroma vector database
│
├── utils/
│   └── audio_processor.py         # Download, convert & chunk audio
│
├── downloads/                     # Generated/downloaded audio
├── vector_db/                     # Chroma vector database
└── .env                           # API credentials
```

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
