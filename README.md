# 🎬 AI Video Assistant

An AI-powered video analysis platform that transforms video/audio content into actionable insights through automatic transcription, summarization, extraction, and intelligent Q&A using RAG (Retrieval-Augmented Generation).

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-Web%20App-red?logo=streamlit)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## ✨ Features

### 🎥 **Multi-Source Input**
- Download and process YouTube videos
- Support for local audio/video files (MP3, MP4, WAV, etc.)

### 🔊 **Audio Processing**
- Automatic audio extraction from video
- Conversion to 16kHz mono WAV format for optimal transcription
- Intelligent chunking of long audio files to handle API limits

### 📝 **Transcription**
- **Local Speech-to-Text**: OpenAI Whisper running locally (no cloud dependency)
- **Multi-language support**: English & Hinglish (Hindi-English code-switching)
- Real-time progress tracking

### 🏷️ **Intelligent Extraction**
- **Auto-generated titles**: AI-generated session titles from meeting content
- **Summaries**: Concise meeting summaries capturing key points
- **Action Items**: Automatically extracted tasks and follow-ups
- **Key Decisions**: Important decisions made during the meeting
- **Open Questions**: Unanswered questions requiring follow-up

### 🧠 **RAG Chat Interface**
- Ask natural language questions about your meeting
- Retrieval-Augmented Generation (RAG) for accurate, context-aware answers
- Maintains conversation history
- Uses Mistral AI + LangChain + ChromaDB vector store

### 🎨 **Beautiful UI**
- Modern dark theme with gradient accents
- Real-time pipeline status visualization
- Responsive design with Streamlit
- Smooth animations and transitions

---

## 🚀 Quick Start

### Prerequisites
- **Python 3.10+**
- **FFmpeg** (required for audio processing)
  - **macOS**: `brew install ffmpeg`
  - **Ubuntu/Debian**: `sudo apt-get install ffmpeg`
  - **Windows**: Download from [ffmpeg.org](https://ffmpeg.org/download.html)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/HarshadKavade/AI_Video_Assistant.git
   cd AI_Video_Assistant/AI-Video-Assistant--main
   ```

2. **Create a Python virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r Requirements.txt
   ```

4. **Set up environment variables**
   Create a `.env` file in the project root:
   ```env
   # Mistral API Key (get from https://console.mistral.ai)
   MISTRAL_API_KEY=your_mistral_api_key_here
   
   # Optional: HuggingFace token for private models
   HUGGINGFACE_API_KEY=your_hf_token_here
   ```

### Usage

#### **Web UI (Recommended)**
```bash
streamlit run app.py
```
Open your browser and navigate to `http://localhost:8501`

#### **Command Line**
```bash
python main.py
```
Follow the interactive prompts to analyze your video/audio.

---

## 📋 Pipeline Architecture

```
Input (YouTube URL / Local File)
         ↓
    🔊 Audio Processing
         ↓
    📝 Transcription (Whisper)
         ↓
    🏷️ Title Generation
         ↓
    📋 Summarization
         ↓
    🔍 Extraction (Actions, Decisions, Questions)
         ↓
    🧠 RAG Engine Setup
         ↓
    💬 Interactive Q&A Chat
```

---

## 📦 Key Dependencies

### Audio & Video
- **yt-dlp**: YouTube video downloading
- **pydub**: Audio format conversion
- **ffmpeg-python**: FFmpeg bindings
- **openai-whisper**: Local speech-to-text (runs on CPU/GPU)

### LLM & RAG
- **langchain**: LLM orchestration (LCEL)
- **mistralai**: Mistral API client
- **chromadb**: Local vector database
- **sentence-transformers**: Embedding generation

### UI
- **streamlit**: Web framework
- **streamlit-extras**: Enhanced widgets

See `Requirements.txt` for complete dependencies.

---

## 🎯 Use Cases

✅ **Meeting Transcription & Summarization**  
✅ **Lecture Note Generation**  
✅ **Interview Transcripts**  
✅ **Podcast Analysis**  
✅ **Training Video Documentation**  
✅ **Legal/Medical Dictation**  

---

## 🔧 Configuration

### Adjust Audio Chunking
Edit in `utils/audio_processor.py`:
```python
CHUNK_SIZE = 600000  # bytes, adjust based on API limits
```

### Change Language
In the Streamlit UI, select from:
- `english`: English transcription
- `hinglish`: Hindi-English mixed language support

### Mistral API Model
The RAG pipeline uses **Mistral-large** by default. Adjust in `core/rag_engine.py`:
```python
model = "mistral-large-latest"  # Change to mistral-medium or mistral-small
```

---

## 📂 Project Structure

```
AI-Video-Assistant--main/
├── app.py                      # Streamlit web interface
├── main.py                     # CLI entry point
├── Requirements.txt            # Python dependencies
├── core/
│   ├── transcriber.py         # Whisper transcription
│   ├── summarizer.py          # Title & summary generation
│   ├── extractor.py           # Action items, decisions, questions
│   └── rag_engine.py          # RAG pipeline (Mistral + ChromaDB)
└── utils/
    └── audio_processor.py      # Audio extraction & chunking
```

---

## 🌐 API Requirements

### Mistral API
1. Sign up at [console.mistral.ai](https://console.mistral.ai)
2. Create an API key
3. Add to `.env` file as `MISTRAL_API_KEY`

**Note**: HuggingFace embeddings (used for RAG) are free and downloaded locally.

---

## 🐛 Troubleshooting

### FFmpeg not found
```bash
# macOS
brew install ffmpeg

# Ubuntu/Debian
sudo apt-get install ffmpeg

# Windows
choco install ffmpeg  # If using Chocolatey
```

### Whisper model download takes too long
First run downloads the model (~3GB). Subsequent runs use the cached model.

### CUDA/GPU support
For faster transcription, install PyTorch with CUDA:
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### Memory issues with long videos
Increase audio chunking in `utils/audio_processor.py` to process smaller segments.

---

## 📊 Performance

| Task | Time (Sample 1h Video) | Hardware |
|------|----------------------|----------|
| Audio Extraction | ~2 min | Any |
| Transcription | ~8-15 min | CPU / ~2 min on GPU |
| Summarization | ~10 sec | Any |
| RAG Setup | ~5 sec | Any |
| Per Chat Query | ~2-5 sec | Any |

---

## 🔒 Privacy & Security

- ✅ **Local Processing**: Transcription runs locally using Whisper
- ✅ **Optional Cloud**: Only Mistral API calls (for LLM) require cloud connectivity
- ✅ **No Data Logging**: Your transcripts are not stored anywhere
- ⚠️ **API Keys**: Keep `.env` file secure and never commit to version control

---

## 📝 License

This project is licensed under the **MIT License** – see LICENSE file for details.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📧 Support & Contact

For questions, issues, or suggestions:
- **GitHub Issues**: [Open an issue](https://github.com/HarshadKavade/AI_Video_Assistant/issues)
- **GitHub Discussions**: [Start a discussion](https://github.com/HarshadKavade/AI_Video_Assistant/discussions)

---

## 🙏 Acknowledgments

- [OpenAI Whisper](https://github.com/openai/whisper) for transcription
- [Mistral AI](https://mistral.ai) for LLM capabilities
- [LangChain](https://langchain.com) for LLM orchestration
- [Streamlit](https://streamlit.io) for the web framework
- [ChromaDB](https://www.trychroma.com) for vector storage

---

**Made with ❤️ by [HarshadKavade](https://github.com/HarshadKavade)**

⭐ If you find this project helpful, please consider giving it a star!
