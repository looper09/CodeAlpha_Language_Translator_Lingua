Here is your updated `README.md` file. I have kept all of your original formatting and content, but I inserted a prominent **Live Demo** section right at the top so recruiters can instantly test your app. I also slightly updated the "Common Questions" section to reflect your new Vercel deployment.

You can copy and paste this entire block directly into your GitHub `README.md`:

```markdown
# Quick Start Guide — Language Translation Tool

## 🚀 Live Demo
You can access and test the fully functional application live here:
🔗 **[Insert Your Vercel App URL Here]**

*(Note: This live demo is hosted on Vercel. Standard text translation and audio features work instantly in the browser. However, translating massive documents might hit Vercel's 10-second serverless timeout limit. For very large files, local execution is recommended.)*

---

## Installation & Setup (5 minutes)

### 1. Install Python Dependencies
```bash
cd translation-tool/
pip install -r requirements.txt

```

### 2. Run the Server

```bash
python main.py

```

You should see:

```
Uvicorn running on [http://127.0.0.1:8000](http://127.0.0.1:8000)
Press CTRL+C to quit

```

### 3. Open in Browser

Go to: **http://localhost:8000**

That's it! 🎉

---

## Feature Overview

### 📝 Text Translation

1. Enter text in the input box
2. Pick source & target languages (or use Auto-Detect)
3. Click **Translate** or press `Ctrl+Enter`
4. Result appears below with word count

**Pro Tips:**

* Click **Swap** (⇅) to reverse language direction
* Click **Copy** to copy translation to clipboard
* Use **Listen** buttons (🔊) to hear pronunciation

### 🎤 Speech Features

* **Speak Input:** Click the **mic button** below source text, speak, auto-translates
* **Listen to Result:** Click **Listen** button on translation to hear it read aloud
* Works on Chrome, Edge, Brave (Firefox limited)

### 📚 Translation History

* Every translation auto-saves to the sidebar
* Click any entry to restore & re-translate
* Shows last 50 translations
* Click **Clear** to wipe history

### 📄 Document Translation

1. Scroll to **Document Translation** section
2. Click to upload or drag-drop `.txt` or `.docx` files
3. Pick languages
4. Click **Translate Document**
5. Translated file auto-downloads

**Limits:**

* Max 10 MB file size
* .txt files: split into chunks, translated separately
* .docx files: paragraphs + table content translated, formatting preserved

---

## Troubleshooting

### Speech-to-Text Not Working

**Error:** "Microphone error: network"

**Solutions:**

1. Check internet connection
2. Disable VPN/Proxy temporarily
3. On Brave: Click Shield icon (top-right) and adjust settings
4. Try incognito mode
5. Grant microphone permission when prompted

**Unsupported Browser?**

* Firefox: TTS works, STT doesn't
* Safari: Both work with webkit prefix
* Chrome, Edge, Brave: Full support ✅

### Translation Seems Off

* Google Translate quality varies by language pair
* Technical terms may not translate perfectly (expected)
* Double-check important translations manually
* Specialized domains (legal, medical) need human review

### Document Download Not Working

1. Check file isn't >10 MB
2. Ensure target language is selected
3. Wait for "Translation complete" message
4. Check browser download folder

### Hang or Timeout on Large Document

* Large files (5-10 MB) take 30-60 seconds
* UI shows "Translating…" status
* Be patient, don't refresh
* If it times out after 5 min, split into smaller files

---

## Project Structure

```
translation-tool/
├── main.py                 # FastAPI backend
├── index.html              # Frontend (all-in-one)
├── requirements.txt        # Python dependencies
├── vercel.json             # Vercel deployment configuration
├── PROJECT_AUDIT.md        # Full feature audit
└── README.md               # This file

```

**Total Files:** 6

**Lines of Code:** ~1,500 (500 backend, 1,000+ frontend)

**Dependencies:** 5 packages

---

## API Endpoints (Advanced)

### `GET /languages`

Returns all supported languages:

```json
{
  "English": "en",
  "Spanish": "es",
  "French": "fr",
  ...
}

```

### `POST /translate`

Translate text:

```bash
curl -X POST http://localhost:8000/translate \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Hello world",
    "source_language": "en",
    "target_language": "es"
  }'

```

Response:

```json
{
  "translated_text": "Hola mundo",
  "source_language": "en",
  "detected_language": "en",
  "target_language": "es"
}

```

### `POST /translate-document`

Translate a file:

```bash
curl -X POST http://localhost:8000/translate-document \
  -F "file=@myfile.txt" \
  -F "source_language=auto" \
  -F "target_language=es" \
  > translated_file.txt

```

---

## Browser Support

| Browser | TTS | STT | Score |
| --- | --- | --- | --- |
| Chrome | ✅ | ✅ | 10/10 |
| Edge | ✅ | ✅ | 10/10 |
| Brave | ✅ | ✅ | 10/10 |
| Safari | ✅ | ⚠️ | 8/10 |
| Firefox | ✅ | ❌ | 6/10 |

**Recommendation:** Use Chrome or Edge for full features.

---

## Performance Tips

1. **Large Documents:** Split into chapters/sections first
2. **Long Text:** Keep under 4000 chars per translation for speed
3. **Frequent Translating:** Use keyboard shortcut `Ctrl+Enter`
4. **Multiple Languages:** Use Swap button instead of re-selecting

---

## Limitations You Should Know

1. **No Offline Mode** — Requires internet (uses Google Translate)
2. **No PDF Support** — Use `.docx` instead or copy-paste text
3. **No User Accounts** — History lost on refresh (privacy-first design)
4. **No Rate Limiting** — Don't spam the API in production
5. **Quality Varies** — Google Translate has ~95% accuracy; review manually

---

## For Developers

### Adding a New Feature

1. Backend changes → `main.py`
2. Frontend changes → `index.html` (search, edit, save)
3. Test in browser
4. Update `PROJECT_AUDIT.md`

### Running Tests

```python
# Manual testing only (no test suite included)
# Test each phase in browser, see PROJECT_AUDIT.md for checklist

```

### Code Style

* Python: PEP 8 (4-space indent)
* JavaScript: No semicolons (modern style)
* CSS: Organized by section with comments

---

## Common Questions

**Q: Can I deploy this online?**
A: Yes! It is currently deployed via Vercel using Serverless functions. To deploy it elsewhere, you may want to add rate limiting first (see PROJECT_AUDIT.md for details).

**Q: Will my translations be saved?**
A: Only in browser memory (current session). Refresh = history lost. This is by design for privacy.

**Q: Can I use a different translation API?**
A: Yes, replace `GoogleTranslator` in `main.py` with `AzureTranslator`, `LibreTranslator`, etc. from the `deep-translator` library.

**Q: Why no PDF support?**
A: PDFs are complex (images, layouts, etc.). `.docx` covers 90% of use cases.

**Q: Can I add more languages?**
A: Update the `SUPPORTED_LANGUAGES` dict in `main.py` with any ISO 639-1 codes Google Translate supports.

**Q: Is my data private?**
A: Yes. Text is sent only to Google Translate (Google's privacy policy applies). Not stored locally on server.

---

## License & Attribution

* **Google Translate:** Third-party API (Google's Terms apply)
* **deep-translator:** Python wrapper (MIT License)
* **python-docx:** Word document library (MIT License)
* **Web Speech API:** Browser-native, no attribution needed

---

## Next Steps

1. **Test all features** (see checklist in PROJECT_AUDIT.md)
2. **Try on mobile** to verify responsive design
3. **Test speech features** in Chrome/Edge
4. **Upload test documents** (.txt and .docx)
5. **Read the audit** for optional enhancements

---

**Ready to showcase this to CodeAlpha?** ✨

You have a production-quality translation tool. Highlight:

* ✅ Clean architecture (separation of concerns)
* ✅ Anti-hallucination design (hardcoded dictionaries)
* ✅ Advanced features (audio, documents, history)
* ✅ Beautiful, responsive UI
* ✅ Robust error handling

Good luck! 🚀

```

```
