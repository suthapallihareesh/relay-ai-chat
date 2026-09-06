# Relay — Multi-Model AI Chat

A beautiful, fully-featured static web interface for chatting with multiple AI models simultaneously, powered by free and open-source model APIs.

![Relay Preview](https://img.shields.io/badge/Status-Active-brightgreen) ![HTML5](https://img.shields.io/badge/Built%20with-HTML5%2FCSS%2FJS-orange) ![Size](https://img.shields.io/badge/Size-~221KB-blue) ![License](https://img.shields.io/badge/License-MIT-green)

## Features

### 🤖 Multi-Model Support
Chat with models from multiple providers without API keys:
- **OVH Kepler** (EU-hosted, anonymous tier)
  - Qwen 3.6/3.5/3 series
  - Mistral Small 3.2, Nemo
  - GPT-OSS 20B
- **LLM7.io** (aggregated models, ~500K tokens/day)
  - GPT-4.1 nano, GPT-4o mini
  - DeepSeek R1 & V3
  - Gemini 2.5 Flash-Lite
  - Mistral, Qwen, Mixtral
- **Pollinations** (tier-limited, anonymous)
  - GPT-5 Nano, GPT-4.1 Nano
- **Kilo Gateway** (200 req/hr free tier)
  - StepFun Step 3.7, NVIDIA Nemotron 3
  - Poolside Laguna M.1
- **GPT4Free** (via g4f.space → Groq proxy)
- **AI Horde** (crowdsourced GPU cluster)

### 🌐 Web Search & Sources
- Ground answers in live web searches (Wikipedia, Reddit, web, Stack Overflow, Hacker News)
- Auto-select best sources or manually choose text/image sources
- Inline citations with source links
- Weather and news card integration

### 💾 Local Chat History
- All conversations saved **locally in your browser** — nothing uploaded unless you enable Premium
- Search and filter past chats
- Pin favorite conversations
- One-click clear history

### 👤 Account & Premium
- Sign in for premium models (GPT-4.1, Claude Sonnet)
- Plan management and billing portal
- Backend authentication (Node server) for API key security
- Free tier works entirely anonymously

### 📱 Responsive & Progressive
- Beautiful dark theme (navy + violet/azure gradient)
- Mobile-optimized with collapsible sidebar
- Installable as PWA (Progressive Web App)
- Works offline after first load

### 🖼️ Rich Media
- Image display and lightbox viewer
- Image search integration
- Weather cards with forecast
- Inline code and formatting

### ⚙️ Model Management
- Switch between models per message
- Auto-select best model for each query
- Manage available models
- Rate limiting awareness

## Quick Start

### Option 1: Open Online
Simply open `without_api.html` in a web browser:
```bash
# Clone the repo
git clone https://github.com/suthapallihareesh/relay-ai-chat
cd relay-ai-chat

# Serve locally (Python)
python -m http.server 8000

# Then open http://localhost:8000/without_api.html
```

**Note:** The file:// protocol blocks CORS requests. Always serve over `http://` or `https://`.

### Option 2: Direct Browser Open
- Download `without_api.html`
- Open it directly in your browser (works, but may have CORS limitations)
- Or drag & drop into your browser window

### Option 3: Deploy
Upload `without_api.html` to any static hosting:
- **Vercel:** `vercel deploy`
- **Netlify:** Drop file in web UI
- **GitHub Pages:** Push to repo, enable Pages
- **Any web server:** `scp without_api.html user@host:/var/www/`

## Usage

1. **New Chat** — Click "+ New chat" or start typing
2. **Choose Model** — Right panel shows available models (auto-select works great)
3. **Search Web** — Toggle globe icon to ground answers in live sources
4. **Pick Sources** — Click the sources icon to auto-select or manually choose
5. **Send** — Press Enter (Shift+Enter for new line)
6. **Sign In** — Avatar button (top right) for Premium models

### Keyboard Shortcuts
- `Enter` → Send message
- `Shift + Enter` → New line
- `Esc` → Close modals/lightbox

### Configuration
Edit the `CFG` object at the top of the script:
```javascript
var CFG = {
  TIMEOUT: 9000,           // Request timeout (ms)
  MAX_TEXT: 16000,         // Max message length
  HIST_MAX: 25,            // Max chat history
  MMR_LAMBDA: 0.72,        // Search ranking parameter
  GROUND_SENTS: 8,         // Sentences for web context
  SB_MIN_W: 210,           // Sidebar min width
  SB_MAX_W: 420,           // Sidebar max width
  SB_DEF_W: 264,           // Sidebar default width
};
```

## Premium (Backend)

Free models work entirely anonymously. To unlock premium models (GPT-4.1, Claude Sonnet):

1. **Download backend** — In account modal, click "Download backend files (.zip)"
2. **Set up Node server:**
   ```bash
   unzip backend.zip
   cd backend
   npm install
   npm start
   ```
3. **Connect frontend** — Enter backend URL in account modal (e.g., `http://localhost:8787`)
4. **Sign in** — Upgrade and authenticate

The backend:
- Holds API keys securely (never exposed to frontend)
- Validates subscriptions
- Proxies requests to premium model providers
- Can run locally or on any host

## Architecture

**Single-file design** — Everything in `without_api.html`:
- **HTML:** 832 lines of semantic markup
- **CSS:** 600+ lines of modern design
  - CSS Grid & Flexbox layouts
  - Dark theme with gradient accents
  - Responsive mobile breakpoints
  - Smooth animations & transitions
- **JavaScript:** 8000+ lines
  - Model API integrations (6 providers)
  - Web search & source grounding
  - Local storage management
  - UI state management
  - Auth & account handling

**Dependencies:**
- Google Fonts (optional, cached)
- JSZip (for backend download)
- No frameworks, no build step

## Search Providers

Integrated search sources:
- 🌐 **Web** (general search)
- 📘 **Wikipedia** (encyclopedia)
- 🔗 **Reddit** (community discussion)
- 🔍 **DuckDuckGo** (privacy search)
- 💻 **Stack Overflow** (programming Q&A)
- 🔴 **Hacker News** (tech news)
- 📊 **Wikidata** (structured knowledge)
- 📰 **News** (current events)
- 🌤️ **Weather** (real-time conditions)
- 🖼️ **Images** (visual search)

## Troubleshooting

### "Requests may be blocked here" warning
This page is open as `file://`. Serve over HTTP instead:
```bash
python -m http.server 8000
# Open http://localhost:8000/without_api.html
```

### Models return 429 (rate limited)
Free anonymous tiers are rate-limited per IP:
- OVH: ~2 req/min per model
- LLM7: ~60 req/hr, 10/min
- Pollinations: 1 req/15s
- Kilo: 200 req/hr
- AI Horde: Depends on volunteer availability

Try a different model or wait before retrying.

### Search isn't working
- Ensure web search toggle is **ON** (globe icon)
- Check your internet connection
- Some sources may be temporarily down (fallback works)

### Can't save chats
Chats require browser local storage. Check:
- Private/Incognito mode (clears on close)
- Storage quota (clear old chats if needed)
- Browser settings (localStorage enabled)

### Premium models won't connect
- Ensure backend is running: `npm start`
- Check backend URL in account modal
- Verify API keys are set in backend `.env`
- Check backend logs for errors

## Browser Support

- **Chrome/Edge:** Full support (v90+)
- **Firefox:** Full support (v88+)
- **Safari:** Full support (v14+)
- **Mobile:** Full support (iOS Safari, Chrome Mobile)

## Rate Limits & Fair Use

⚠️ **Important:** All free APIs are public and rate-limited. Be respectful:
- Don't spam requests
- Leave time between messages
- Distribute load across models
- Consider supporting the model providers

## Storage & Privacy

- ✅ Chats stored **locally** (IndexedDB/localStorage)
- ✅ No telemetry or tracking
- ✅ No data sent to external servers (free tier)
- ⚠️ Premium mode requires backend (which stores auth)
- 🔒 All communication HTTPS-only (when deployed)

## Contributing

Found a bug? Have a suggestion? Issues and PRs welcome!

### Development
The entire app is in one file for easy hacking. To modify:
1. Edit `without_api.html`
2. Serve locally with `python -m http.server 8000`
3. Reload browser
4. Check console for errors (F12)

### Adding a Model Provider
1. Find `var SOURCES = { ... }`
2. Add new provider with models array
3. Add integration in message handler (search for `function sendMessage`)
4. Test in app

## License

MIT — Use freely, commercially or otherwise.

## Credits

Built with ❤️ using free & open APIs. Special thanks to:
- **OVHcloud** for Kepler endpoints
- **LLM7.io** for model aggregation
- **Groq** (via g4f.space) for fast inference
- **AI Horde** for community GPU cluster
- **Pollinations** for anonymous access
- All open-source model creators (Mistral, Meta Llama, Qwen, DeepSeek, etc.)

---

**Status:** Active & maintained  
**Last Updated:** 2026-09-06  
**Repository:** [GitHub](https://github.com/suthapallihareesh/relay-ai-chat)
