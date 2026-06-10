# 🧠 AI Counselor Client Therapy Simulation

An automated, closed-loop simulation where two different AI models engage in a realistic therapeutic conversation. One AI model plays the role of an empathetic mental health counselor (Gemini), while another (Ollama/Llama 3.2) plays the role of a client seeking support.

## 📋 Overview

This project demonstrates how AI can be used to simulate therapeutic interactions. It creates a safe, scripted environment where:

- **Gemini** (via LiteLLM) acts as **Dr. Sarah**, an experienced and empathetic mental health counselor
- **Ollama/Llama 3.2** acts as **Alex**, a software developer experiencing work stress, anxiety, and emotional exhaustion
- Both models communicate directly with each other in a realistic therapy session format

The simulation includes:
- Warm, non-judgmental counseling responses
- Realistic client responses with hesitations and vulnerabilities
- Active listening and reflective techniques
- A complete session flow from opening greeting to closing summary

## ✨ Features

✅ **AI-to-AI Conversation**: Two LLMs interact autonomously without human intervention  
✅ **Realistic Dialogue**: Client responses include natural hesitations, self-doubt, and vulnerability  
✅ **Therapeutic Techniques**: Counselor uses active listening, validation, and open-ended questions  
✅ **Multi-Model Support**: Works with Gemini API and local Ollama models  
✅ **Session Transcript**: Displays and saves complete conversation logs  
✅ **Configurable Sessions**: Adjustable number of conversation turns  

## 🛠️ Tech Stack

- **Python 3.9+**
- **Jupyter Notebook** - Interactive environment
- **Gemini 2.5 Flash Lite** - Counselor model (via Google Generative AI)
- **Ollama + Llama 3.2** - Client model (local inference)
- **LiteLLM** - Unified API for multi-model calls
- **OpenAI SDK** - For Ollama API compatibility
- **python-dotenv** - Environment variable management

## 📦 Prerequisites

### 1. Install Required Python Packages

```bash
pip install requests python-dotenv google.generativeai openai litellm
```

### 2. Set Up API Keys

Create a `.env` file in the project root:

```env
GOOGLE_API_KEY=your_gemini_api_key_here
OLLAMA_API_KEY=your_ollama_api_key_here
```

**Get your Google API Key:**
- Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
- Create a new API key
- Copy it to your `.env` file

### 3. Install and Run Ollama

**Install Ollama:**
- Download from [ollama.ai](https://ollama.ai)
- Follow the installation guide for your OS

**Pull the Llama 3.2 Model:**
```bash
ollama pull llama3.2
```

**Start Ollama Server:**
```bash
ollama serve
```

The Ollama server runs on `http://localhost:11434` by default.

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Devanshi-gite/ai_counselor_client_therapy.git
cd ai_counselor_client_therapy
```

### 2. Set Up Environment

```bash
# Create virtual environment
python -m venv venv

# Activate it
# On macOS/Linux:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Run the Jupyter Notebook

```bash
jupyter notebook counselor_therapy_conversation.ipynb
```

### 4. Execute All Cells

Run each cell in order. The notebook will:
- Set up API connections for both models
- Define the counselor and client personalities
- Run the conversation loop
- Display the full session transcript
- Save the transcript to a text file

## 📖 How It Works

### Session Flow

1. **Opening**: Counselor greets the client warmly and invites them to share
2. **Main Loop** (Configurable Turns):
   - Client (Ollama) responds to the counselor
   - Counselor (Gemini) responds with empathy and guidance
   - Exchange repeats for specified number of turns
3. **Closing**: Counselor provides a warm summary, acknowledges the client's courage, highlights strengths, and ends with encouragement

### Conversation Architecture

The project uses separate message histories for each model:

```
gemini_messages  → Gemini sees its responses as 'assistant', client's as 'user'
ollama_messages  → Ollama sees its responses as 'assistant', counselor's as 'user'
session_log      → Full conversation transcript for display
```

This ensures each model maintains proper context while enabling seamless back-and-forth dialogue.

## 🎭 Key Prompts

### Counselor System Prompt

Dr. Sarah is an experienced mental health counselor who:
- Communicates warmly and non-judgmentally
- Uses active listening and emotional validation
- Asks one thoughtful open-ended question at a time
- Encourages healthy coping and self-reflection
- Sounds human, not robotic
- Maintains professional boundaries with compassion
- Provides warm session closings

### Client System Prompt

Alex is a software developer who:
- Experiences chronic work stress and anxiety
- Struggles to articulate feelings clearly
- Speaks naturally with hesitations and deflections
- Opens up gradually as trust builds
- References specific situations (deadlines, isolation)
- Shows authentic vulnerability and self-doubt
- Takes time to heal—doesn't resolve quickly

## 📊 Customization

### Adjust Session Length

In the notebook, modify the `num_turns` parameter:

```python
session_log = run_counseling_session(num_turns=10)  # More turns = longer session
```

### Customize Personalities

Edit `GEMINI_SYSTEM` and `OLLAMA_SYSTEM` prompts to:
- Change the counselor's approach or experience level
- Modify the client's background, presenting issues, or communication style
- Add specific therapeutic techniques or modalities

### Switch Models

- Replace `gemini/gemini-2.5-flash-lite` with another Google model
- Replace `llama3.2` with another Ollama model (e.g., `mistral`, `neural-chat`)

## 📁 Project Structure

```
ai_counselor_client_therapy/
├── README.md                              # This file
├── counselor_therapy_conversation.ipynb   # Main Jupyter notebook
├── session_transcript.txt                 # Generated session output
└── .env                                   # API keys (not in repo)
```

## 🔍 Understanding the Output

The notebook displays a formatted transcript showing:

```
🟢 Gemini (Counselor) (Turn 1)
> [Counselor response...]

🔵 Ollama (User) (Turn 1)
> [Client response...]
```

### Saved Transcript Format

Sessions are saved as `session_transcript.txt` with:
- Clear speaker labels (Counselor / User)
- Full message content
- Visual separators between exchanges

## ⚠️ Important Notes

### Rate Limiting
- Gemini API has rate limits (free tier: 15 requests per minute)
- The code includes retry logic with `num_retries=3`
- For longer sessions, consider adding delays between API calls

### Privacy & Ethics
- ⚠️ This is a **simulation for educational and research purposes only**
- **Not a substitute for real mental healthcare**
- Do not use outputs for actual clinical decision-making
- Always recommend professional help for real concerns

### Local Models
- Ollama runs locally for privacy
- Ensure you have sufficient CPU/GPU for Llama 3.2
- First run may be slow while the model is loaded

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `❌ Set GOOGLE_API_KEY or GEMINI_API_KEY in your .env file` | Add your Google API key to `.env` |
| `Connection refused: http://localhost:11434` | Start Ollama with `ollama serve` |
| Empty response from Gemini | Check API quota, rate limits, or connection |
| Ollama model not found | Run `ollama pull llama3.2` |
| Import errors | Run `pip install -r requirements.txt` |

## 📚 References

- [Google Generative AI Docs](https://ai.google.dev/)
- [Ollama Documentation](https://ollama.ai)
- [LiteLLM Docs](https://docs.litellm.ai/)
- [Therapeutic Communication Techniques](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4360391/)

## 📝 License

This project is open source and available under the MIT License.

## 👤 Author

**Devanshi Gite**  
GitHub: [@Devanshi-gite](https://github.com/Devanshi-gite)


**Happy exploring! 🚀**

*Remember: This is an AI simulation for educational purposes. Always seek professional help for real mental health concerns.*
