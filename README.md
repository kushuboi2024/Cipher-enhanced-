# cipher. 🔐
### Decode any word, without leaving the page.

**cipher.** is a browser-based reading tool built for anyone who has ever lost their flow mid-sentence because of an unfamiliar word. Paste any text, upload a PDF, or scan an image — click any word to instantly see its meaning.

No backend. No login. No framework. One HTML file.

---

## ✨ Live Demo

👉 **[Try cipher. here](https://your-username.github.io/cipher)**

---

## 🎯 Why I Built This

Preparing for CAT, I found that Reading Comprehension was less about comprehension and more about vocabulary. Every time I hit a word I didn't know — *ephemeral, laconic, inimical* — I'd open a new tab, Google it, come back, and realise I'd completely lost the thread of the passage.

Do that 3–4 times in one essay and you just stop wanting to read.

cipher. fixes that. The meaning comes to you, right where you're reading.

---

## 🚀 Features

### Core Reading
- **Click to decode** — click any word to instantly see its dictionary definition, pronunciation, word type, and an example sentence
- **PDF reader** — upload a text-based PDF and read it page by page with full paragraph formatting preserved
- **OCR / Scan mode** — upload a scanned PDF or photo of a page; Tesseract.js extracts the text so you can read and decode it
- **Split view** — paste text and edit it on the left while reading on the right; the reader syncs as you type

### Smart Lookup
- **Persistent cache** — once a word is fetched, it's stored in your browser's `localStorage` forever. Every future click is instant — zero API calls
- **3-retry logic** — if the dictionary API fails, it retries automatically (400ms → 800ms intervals) before showing an error. Tap to retry manually if needed
- **Nested word lookup** — if the definition itself contains a hard word, type it in the search bar inside the panel and look it up without closing anything. Full back-navigation history included
- **Words decoded tracker** — looked-up words are highlighted green. A badge in the header counts unique words decoded this session

### AI Contextual Meaning
- **Get Context** — paste the sentence where you found the word, tap *Get Context*, and Claude explains what the word means *in that specific context* — not just a generic dictionary definition
- Requires a Claude API key (free to get at [console.anthropic.com](https://console.anthropic.com)). Costs fractions of a cent per lookup
- Your API key is stored only in your browser — never sent anywhere except directly to Anthropic's servers

### Vocabulary Export
- **Export CSV** — download all decoded words with their type, phonetic, definition, and example sentence. Opens in Excel / Google Sheets
- **Export plain text** — formatted word list, great for printing or pasting into notes

### Customisation & Accessibility
- **Font picker** — choose from DM Sans, Playfair Display, Georgia, or Courier
- **Font size slider** — 13px to 22px
- **Dark mode** — full dark theme toggle
- **Touch / tap mode** — for mobile and tablet users; tap a word to decode, tap elsewhere to dismiss
- **Collapsible editor** — hide the edit panel for a full-width reading experience
- **Click outside to dismiss** — the definition panel closes when you tap anywhere outside it

---

## 🛠 How It Works

### Dictionary API
```
Click word
    ↓
GET https://api.dictionaryapi.dev/api/v2/entries/en/{word}
    ↓
Returns: phonetic, part of speech, definition, example
    ↓
Saved to localStorage — instant on every future click
```

The [Free Dictionary API](https://dictionaryapi.dev/) is community-maintained, completely free, and requires no API key.

### Retry Logic
```
Attempt 1 fails → wait 400ms → Attempt 2
Attempt 2 fails → wait 800ms → Attempt 3
Attempt 3 fails → show error with manual retry option
```

### Caching Strategy
```
First click  → API call → result saved to localStorage
Second click → read from cache → instant (0ms API calls)
Cache persists across sessions, page reloads, and browser restarts
Failed lookups are never cached — they always retry fresh
```

### Claude API (Get Context)
```
User pastes sentence → clicks Get Context
    ↓
POST https://api.anthropic.com/v1/messages
System: "Explain what this word means in this sentence. 1-2 sentences."
    ↓
Claude returns contextual explanation
    ↓
Cached in memory for the session
```

### OCR Pipeline
```
Upload scanned PDF or image
    ↓
If PDF → PDF.js renders each page to canvas at 2× scale
    ↓
Tesseract.js reads pixel data → returns text string
    ↓
Text fed into the normal split-view reader
```

---

## 📦 Tech Stack

| Layer | Technology |
|---|---|
| UI & Logic | Vanilla HTML / CSS / JavaScript (zero frameworks) |
| PDF parsing | [PDF.js](https://mozilla.github.io/pdf.js/) by Mozilla |
| OCR | [Tesseract.js](https://github.com/naptha/tesseract.js) |
| Dictionary | [Free Dictionary API](https://dictionaryapi.dev/) |
| AI definitions | [Claude API](https://www.anthropic.com/) by Anthropic |
| Hosting | GitHub Pages (free) |
| Persistence | Browser `localStorage` |

---

## ⚡ Getting Started

### Option 1 — Use the live version
Visit the link above. No setup required.

### Option 2 — Run locally
```bash
# Clone the repo
git clone https://github.com/your-username/cipher.git

# Open in browser — that's it
open cipher/index.html
```

No `npm install`. No build step. No server needed for the core features.

> **Note:** The Claude API (Get Context) requires the file to be served over HTTPS, not opened directly from your filesystem. Use the GitHub Pages link or any local server for that feature.

### Setting up Get Context (optional)
1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Create a free account and generate an API key
3. In cipher., click ⚙️ Settings → paste your key in the **Claude API Key** field
4. It saves automatically — you won't need to paste it again

---

## 📱 Mobile Support

cipher. is fully mobile-friendly:
- Split view stacks vertically on small screens
- Definition panel goes full-width
- Settings drawer goes full-screen
- Touch mode auto-enables on devices with no mouse
- Get Context works on mobile too — paste your API key in ⚙️ Settings

---

## ⚠️ Known Limitations

| Limitation | Reason | Workaround |
|---|---|---|
| Some words return "No definition found" | The free dictionary API doesn't cover technical terms, proper nouns, or very obscure words | Use Get Context with Claude for these |
| Scanned PDF quality depends on scan clarity | Tesseract.js is client-side OCR — less accurate than cloud OCR (Google Vision, AWS Textract) | Use a clean, high-resolution scan |
| Get Context requires an API key | Claude API is a paid service (fractions of a cent per call) | Core dictionary features work entirely for free |
| API key lost in incognito mode | `localStorage` is cleared in incognito | Use a regular browser window |

---

## 🗺 Roadmap

- [ ] Browser extension — decode words on any webpage
- [ ] Vocabulary flashcard export (Anki format)
- [ ] Reading statistics dashboard
- [ ] Support for more languages
- [ ] Cloud sync for vocabulary history (requires backend)

---

## 🙏 Acknowledgements

- [Free Dictionary API](https://dictionaryapi.dev/) — for the free, keyless dictionary
- [PDF.js](https://mozilla.github.io/pdf.js/) — Mozilla's open-source PDF renderer
- [Tesseract.js](https://github.com/naptha/tesseract.js) — client-side OCR
- [Anthropic](https://www.anthropic.com/) — Claude API for contextual meanings

---

## 📄 Licence

MIT — do whatever you want with it.

---

*Built by Kushagra — PM at ICICI Bank, IIT Delhi. [LinkedIn](https://linkedin.com/in/your-profile)*
