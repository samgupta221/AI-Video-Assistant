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

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/AI-Video-Assistant.git

cd AI-Video-Assistant
```

### 2. Create a Virtual Environment

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 3. Install Dependencies

```bash
pip install -r Requirements.txt
```

---

## ⚙️ FFmpeg Setup

The application uses FFmpeg through Pydub for audio/video processing.

Make sure **FFmpeg is installed and available in your system PATH**.

Verify the installation:

```bash
ffmpeg -version
```

If the command returns the FFmpeg version, you're ready to go.

---

## 🔐 Environment Variables

Create a `.env` file in the project root:

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key

WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5
```

### API Keys

The project requires:

| Variable          | Purpose                            |
| ----------------- | ---------------------------------- |
| `MISTRAL_API_KEY` | Mistral LLM operations             |
| `SARVAM_API_KEY`  | Hinglish transcription/translation |

> **Important:** Never commit your `.env` file or API keys to GitHub.

---

# ▶️ Run the Application

Start the Streamlit application with:

```bash
streamlit run app.py
```

Then open the local Streamlit URL shown in your terminal, usually:

```text
http://localhost:8501
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

## 🌐 Supported Input

### YouTube

```text
https://www.youtube.com/watch?v=...
```

The application uses `yt-dlp` to extract the video's audio.

### Local Files

Audio/video files can also be processed locally.

The application converts the input into:

```text
Mono WAV
16 kHz
```

and then splits the audio into approximately **10-minute chunks** for processing.

---

## 🎙️ Transcription Modes

### English

English input uses the local:

```text
OpenAI Whisper
```

The default model is:

```text
small
```

You can change it through:

```env
WHISPER_MODEL=small
```

For example:

```env
WHISPER_MODEL=medium
```

---

### Hinglish

Hinglish input is routed through:

```text
Sarvam AI
```

The audio is further split into smaller pieces because the synchronous Sarvam endpoint accepts limited audio duration per request.

The resulting transcript is returned in English.

---

## 📂 Main Modules

### `utils/audio_processor.py`

Responsible for:

* YouTube audio downloading
* Local media conversion
* WAV conversion
* Audio normalization
* Audio chunking

Main functions:

```python
download_youtube_audio()
convert_to_wav()
chunk_audio()
process_input()
```

---

### `core/transcriber.py`

Handles speech-to-text.

Supports:

```text
Whisper
Sarvam AI
```

Main functions:

```python
transcribe_chunk_whisper()
transcribe_chunk_sarvam()
transcribe_chunk()
transcribe_all()
```

---

### `core/summarizer.py`

Generates:

* Meeting title
* Meeting summary

It uses a map-and-combine summarisation approach for longer transcripts.

---

### `core/extractor.py`

Extracts structured meeting information:

```text
Action Items
Key Decisions
Open Questions
```

---

### `core/vector_store.py`

Responsible for:

* Transcript chunking
* Embedding generation
* ChromaDB creation
* Vector store loading
* Retriever configuration

---

### `core/rag_engine.py`

Implements the question-answering pipeline.

```text
Question
   ↓
Retriever
   ↓
Relevant Transcript Chunks
   ↓
Mistral AI
   ↓
Answer
```

---

### `app.py`

Provides the Streamlit UI, including:

* Input controls
* Language selection
* Processing status
* Results dashboard
* Transcript viewer
* Meeting insights
* RAG chat interface

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

## 🧪 CLI Usage

The project also includes a command-line pipeline.

Run:

```bash
python main.py
```

You will be prompted for:

```text
Enter YouTube URL or local file path:
Language (english/hinglish):
```

The CLI outputs:

* Title
* Summary
* Action items
* Key decisions
* Open questions

It also provides an interactive meeting Q&A mode.

Type:

```text
exit
```

to leave the chat.

---

## 📦 Dependencies

Major dependencies include:

```text
streamlit
openai-whisper
torch
torchaudio
langchain
langchain-mistralai
chromadb
sentence-transformers
yt-dlp
pydub
requests
python-dotenv
reportlab
ffmpeg-python
```

See `Requirements.txt` for the complete dependency list.

---

## 🔒 Security

Do not commit sensitive credentials.

Your `.env` should contain secrets locally:

```env
MISTRAL_API_KEY=...
SARVAM_API_KEY=...
```

Add `.env` to `.gitignore:

```gitignore
.env
__pycache__/
*.pyc
downloads/
downloades/
vector_db/
*.wav
```

---

## 🚧 Future Improvements

Potential improvements include:

* 🎤 Speaker diarization
* ⏱️ Timestamped transcripts
* 👤 Speaker identification
* 📄 PDF/TXT export
* 📊 Meeting analytics
* 📧 Automatic meeting follow-up emails
* 📅 Calendar integration
* 💾 Persistent meeting history
* 🔎 Search across multiple meetings
* 🌍 More language support
* ⚡ Faster parallel transcription
* ☁️ Cloud deployment
* 🔐 User authentication
* 🗂️ Meeting/project organization

---
