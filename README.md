<div align="center">

# Luminous (javis)

**A personal AI assistant that aims to become your own Jarvis: honest, knowledgeable, voice-enabled.**

![Next.js 15](https://img.shields.io/badge/Next.js-15-000000?style=for-the-badge&logo=nextdotjs&logoColor=white) ![FastAPI backend](https://img.shields.io/badge/FastAPI-backend-009688?style=for-the-badge&logo=fastapi&logoColor=white) ![LLM Claude · GPT · Ollama](https://img.shields.io/badge/LLM-Claude_·_GPT_·_Ollama-7C3AED?style=for-the-badge) ![Voice Whisper STT + TTS](https://img.shields.io/badge/Voice-Whisper_STT_+_TTS-10A37F?style=for-the-badge)

</div>

## Tech stack

<p align="center">
  <img src="https://skillicons.dev/icons?i=nextjs,react,ts,tailwind,threejs,py,fastapi&perline=10" alt="Tech stack" />
</p>

## Architecture

```mermaid
flowchart LR
    U([User]) -->|"text or voice"| W["apps/web\nNext.js 15 hologram UI\nZustand, Three.js, Framer Motion"]
    W <-->|"REST + WebSocket"| API["apps/api\nFastAPI"]
    API --> CH["chat / voice / search /\nlanguage / models endpoints"]
    CH --> MS["model_switcher\nautomatic fallback"]
    MS --> CL["Cloud LLMs\nAnthropic, OpenAI"]
    MS --> OL["Local Ollama"]
    CH --> STT["stt_service\nWhisper (Thai supported)"]
    CH --> TTS["tts_service\nEdge-TTS / Coqui"]
    CH --> WS["web_search_service"]
```

---

Personal AI Assistant for Je — Aiming to become your personal Jarvis.

## 🎯 Vision

Luminous is designed to be:
- **Brutally honest & genuinely helpful** — No empty praise, just real talk
- **Deeply knowledgeable** — AI, finance, career, world events, science, philosophy
- **Critical thinker** — Grounded in reality and data
- **Your trusted advisor** — Not just a chatbot, but a partner

## 🏗️ Architecture

```
luminous/
├── apps/
│   ├── web/          # Next.js 15 frontend (Hologram Dashboard UI)
│   └── api/          # FastAPI backend (Core Intelligence)
├── packages/
│   ├── shared/       # Shared types & utilities
│   └── config/       # Shared configs (ESLint, TSConfig)
```

## 🚀 Getting Started

### Prerequisites
- Node.js >= 22.0.0
- Python >= 3.11
- pnpm >= 9.0.0 (or npm)

### Installation

```bash
# Install dependencies
pnpm install

# Install Python dependencies
cd apps/api
pip install -r requirements.txt

# (Optional) Install Ollama for local LLM
# macOS: brew install ollama && ollama serve
# Linux: curl -fsSL https://ollama.com/install.sh | sh

# Pull an Ollama model (for offline use)
ollama pull llama3.2:3b

# Run all services in development
cd ../..
pnpm dev

# Or run separately
pnpm dev:web   # Frontend: http://localhost:3000
pnpm dev:api   # Backend: http://localhost:8000
```

### Environment Setup

```bash
# Copy example env files
cp apps/web/.env.local.example apps/web/.env.local
cp apps/api/.env.example apps/api/.env

# Edit apps/api/.env with your API keys (optional)
# ANTHROPIC_API_KEY=your_key_here  # For Claude
# OPENAI_API_KEY=your_key_here      # For GPT
```

## 🛠️ Tech Stack

### Frontend (apps/web)
- Next.js 15 with App Router
- TypeScript
- shadcn/ui + Tailwind CSS
- Framer Motion (Animations)
- Web Speech API (Voice built-in)
- Recharts (Data visualization)
- Three.js (Holographic effects)

### Backend (apps/api)
- FastAPI (Python)
- Anthropic SDK (Claude)
- OpenAI SDK (Fallback)
- **Ollama Integration** (Local LLM)
- **Whisper** (STT - Thai supported)
- **Edge-TTS / Coqui TTS** (TTS)
- PostgreSQL (Structured data)
- Redis (Cache & sessions)
- Vector DB (RAG memory)

## 🎙️ Voice Features

Luminous supports both text and voice interaction:

### Text-to-Speech (TTS)
- **Edge-TTS**: Free, good quality (default)
- **Coqui TTS**: Local, high quality (optional)
- **pyttsx3**: Offline, always works (fallback)

### Speech-to-Text (STT)
- **Whisper**: Excellent Thai support, local (recommended)
- **Faster-Whisper**: Faster, less memory (alternative)
- **Google Web Speech**: Browser-based, requires internet (built-in)

### Voice Modes

1. **Browser Voice (No installation needed)**
   - Uses Web Speech API
   - Works immediately
   - Requires internet for recognition

2. **Backend Voice (Full control)**
   - Install required packages (see `apps/api/INSTALL.md`)
   - Better quality, more options
   - Works offline with local models

## 🤖 AI Model Options

Luminous supports multiple AI models with automatic fallback:

### Cloud Models (Requires Internet & API Key)
- **Anthropic Claude** (Best reasoning, safety-focused)
- **OpenAI GPT** (Versatile, widely used)

### Local Models (Offline, Free)
- **Ollama** (Run LLMs locally)
  - `llama3.2:3b` - Fast, 4GB RAM
  - `llama3.2` - Balanced, 8GB RAM
  - `qwen2.5:7b` - Excellent Thai support
  - `phi3.5:3.8b` - Minimal resources

### Model Switching

```bash
# Check current model status
curl http://localhost:8000/api/models/status

# Switch to local Ollama
curl -X POST http://localhost:8000/api/models/set \
  -H "Content-Type: application/json" \
  -d '{"model": "local_ollama"}'

# Switch to Claude
curl -X POST http://localhost:8000/api/models/set \
  -H "Content-Type: application/json" \
  -d '{"model": "cloud_anthropic"}'
```

## 📋 Roadmap

### Phase 1: Foundation ✅
- [x] Monorepo setup
- [x] Basic Chat UI
- [x] AI integration (Claude/OpenAI)
- [x] Bilingual support (Thai/English)
- [x] Voice input/output (Web Speech API)
- [x] Model switcher (Cloud/Local)

### Phase 2: Enhanced Voice
- [x] Backend TTS/STT services
- [x] Ollama integration
- [x] Thai voice support
- [ ] Voice activation (wake word "Luminous")
- [ ] Camera + Vision models
- [ ] Object detection (YOLO)

### Phase 3: Real-time Dashboard
- [ ] Real-time data fetching
- [ ] Live visualizations
- [ ] Holographic UI effects
- [ ] WebSocket updates
- [ ] RAG memory system

### Phase 4: Advanced Features
- [ ] Multi-agent system
- [ ] Personalized learning
- [ ] Tool integrations
- [ ] Mobile app

## 📚 Documentation

- **🧠 Model Architecture**: [docs/MODEL_ARCHITECTURE.md](docs/MODEL_ARCHITECTURE.md) — Qwen, Typhoon, and all model options
- **🎤 Hands-Free Guide**: [docs/HANDS_FREE_GUIDE.md](docs/HANDS_FREE_GUIDE.md) — Wake word activation guide (Thai)
- **📝 API Documentation**: http://localhost:8000/docs (FastAPI docs)
- **🌐 Frontend**: http://localhost:3000
- **💚 Health Check**: http://localhost:8000/api/health/

## 🔧 Troubleshooting

### Ollama not connecting
```bash
# Make sure Ollama is running
ollama serve

# In another terminal, check models
ollama list

# Test connection
curl http://localhost:11434/api/tags
```

### Voice not working in browser
- Make sure you're using HTTPS or localhost
- Check browser permissions for microphone
- Some browsers require user interaction first

### Backend API not responding
```bash
# Check if backend is running
curl http://localhost:8000/

# Check logs
cd apps/api
python -m src.main
```

## 💡 Tips

1. **For offline use**: Install Ollama + pull a model + set model to "local_ollama"
2. **For best voice quality**: Install Whisper for STT and Edge-TTS for TTS
3. **For Thai support**: Use `qwen2.5:7b` Ollama model or Claude
4. **For speed**: Use `llama3.2:3b` or browser Web Speech API

## 📄 License

Private project for Je. Not open source.

---

Made with ❤️ for Je
