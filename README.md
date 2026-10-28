# TraceIQ Interactive

TraceIQ is an AI-powered code debugger and inspector. It combines a Monaco code editor with an intelligent panel to detect bugs, visualize execution traces, calculate Big-O complexity, and apply fixes directly to your code.

---

## Features

- **Monaco Code Editor**: Full-featured code editor with syntax highlighting and automatic language detection.
- **Issue Detection**: Pinpoints bugs, edge cases, and runtime errors with exact line numbers.
- **One-Click Apply Fix**: Patches your code directly in the editor with a single click.
- **Step-by-Step Trace**: Simulates execution line-by-line and displays changing variable states.
- **Complexity Analysis**: Calculates Time and Space complexity ($O(N)$ notation) with optimization suggestions.
- **Auto-Generated Tests**: Generates test cases covering standard inputs and tricky edge cases.
- **Multi-Model Support**: Works with Google Gemini, xAI Grok, Anthropic Claude, Groq, or OpenAI.

---

## Quick Start

### 1. Install dependencies
```bash
npm install
```

### 2. Configure your API key
Copy the example environment file:
```bash
cp .env.example .env
```
Open `.env` and add your API key. For example, using Google Gemini:
```env
LLM_PROVIDER=openai
LLM_BASE_URL=https://generativelanguage.googleapis.com/v1beta/openai
LLM_API_KEY=your_gemini_api_key_here
LLM_MODEL=gemini-3.8-flash
```

Or using Anthropic Claude:
```env
ANTHROPIC_API_KEY=your_anthropic_key_here
TRACEIQ_MODEL=claude-sonnet-5-5
```

Or using xAI Grok:
```env
LLM_PROVIDER=openai
LLM_BASE_URL=https://api.x.ai/v1
LLM_API_KEY=your_xai_grok_key_here
LLM_MODEL=grok-2-latest
```

### 3. Run the app
```bash
npm run dev
```

- Web UI: http://localhost:5173
- Backend API: http://localhost:8787

---

## Supported LLM Providers

You can use any of the following providers by editing your `.env` file:

- **Google Gemini**: Set `LLM_BASE_URL=https://generativelanguage.googleapis.com/v1beta/openai` and provide your Gemini API key in `LLM_API_KEY`.
- **xAI (Grok)**: Set `LLM_BASE_URL=https://api.x.ai/v1` and provide your key in `LLM_API_KEY`.
- **Groq**: Set `LLM_BASE_URL=https://api.groq.com/openai/v1` and provide your Groq key in `LLM_API_KEY`.
- **OpenAI**: Set `LLM_BASE_URL=https://api.openai.com/v1` and provide your OpenAI key in `LLM_API_KEY`.
- **Anthropic Claude**: Set `ANTHROPIC_API_KEY=your-key`.

The server automatically handles fallback and retries if a model experiences high demand or runs out of credits.

---

## Project Structure

```text
traceiq-interactive/
├── server/
│   ├── index.js           # Express API server & LLM integration
│   └── systemPrompt.txt   # Core analysis system prompt
├── src/
│   ├── components/        # React components (Editor, Inspector, Cards)
│   ├── hooks/             # Custom React hooks (Language detection)
│   ├── utils/             # API client & code patching utilities
│   ├── App.jsx            # Main app component
│   └── styles.css         # UI styles
├── .env.example           # Example environment variables
├── package.json           # Scripts and dependencies
└── vite.config.js         # Vite configuration & proxy
```

---

## How It Works

1. The frontend takes your code from the Monaco editor and sends it to `POST /api/analyze`.
2. The server numbers each line of code and sends it with `systemPrompt.txt` to the configured LLM.
3. The LLM returns a structured JSON response containing detected issues, execution steps, complexity, and test cases.
4. The server validates line numbers and formats the response for the frontend.
5. The frontend displays the results in the inspector panel and highlights relevant lines in the editor.

---

## License

MIT
