# Plain Japanese Window (やさしい日本語の窓口)

Take a photo of a Japanese letter. Gemini turns it into three things on one screen:

1. **Plain Japanese** (やさしい日本語): short sentences, simple words, mostly hiragana.
2. **Your language**: a natural translation (English, 简体中文, Tiếng Việt, 한국어, Português, Español, Filipino, नेपाली).
3. **What to do**: at most three actions, each with "by when". If the letter gives no deadline, the app says so instead of guessing.

Plain Japanese and your language sit side by side, so a Japanese coworker, landlord or teacher can look at the same screen and say "is this the part?".

## Run it

It is a single file with no build step and no dependencies.

```
open index.html          # or: python3 -m http.server 8000
```

- **Demo mode**: with no API key, the "Try a sample letter" button shows a prepared result for a municipal health-insurance notice. Everything works offline.
- **Gemini mode**: paste a Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey). The key is kept in `sessionStorage` of the current tab and is sent only to `generativelanguage.googleapis.com`. Nothing is stored on a server, and no key is in this repository.
- **Language of the screen**: the button in the top right switches Japanese / English. `?ui=en` opens the English screen directly.

## How it works

One call to Gemini Flash (`gemini-flash-latest`, falling back to other current Flash models if one is busy) with the photo (inline image) and/or pasted text, a system prompt, and a JSON response schema (`easy`, `native`, `todo[{what, when, note}]`). The page renders the JSON in three panels. The code is in `index.html` (about 200 lines).

## Limits

- Machine translation can be wrong. Check amounts and dates against the original letter, which is why the original photo stays on screen.
- Blurry or handwritten letters may be misread.
- The letter is sent to the Gemini API. Do not use it for documents you are not allowed to share.

## License

MIT. See `LICENSE`.
