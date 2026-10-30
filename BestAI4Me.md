# BestAI4Me

A single-file, browser-only app for comparing AI answers. Add as many AI names and API profiles as you need, review one AI on its own, or compare multiple answers head-to-head. Saved rounds power the trait summaries, win-rate chart, Elo history, and Gemini agreement metric.

**Live website:** [Open BestAI4Me](https://kameshwaran-vi-britannia.github.io/BESTAI4ME/)

## Run on GitHub Pages

1. Add `index.html` and this `README.md` to your GitHub repository.
2. In the repository, open **Settings → Pages** and publish from the branch and folder containing `index.html` (commonly `main` and `/ (root)`).
3. Open [BestAI4Me](https://kameshwaran-vi-britannia.github.io/BESTAI4ME/). There is no backend, build step, or package installation.

Chart.js loads from jsDelivr. If that CDN is unavailable, comparisons still work, but charts will not render until it loads.

## Connect an AI API

1. In **Setup → AI names**, add an AI label such as `Claude` or `My OpenRouter model`.
2. Tap **Add API connection**. Set the connection's AI name to match the label, choose an API format, then enter the model ID, endpoint, and key.
3. In **Arena**, tap **Generate with [AI name]** to call that profile, or paste the answer manually. Generation only happens when you tap the button.

The page supports Gemini's `generateContent` format, Anthropic Messages, and OpenAI-compatible chat completions. For OpenAI-compatible services, enter a base URL such as `https://api.openai.com/v1` or `https://openrouter.ai/api/v1`, then enter that service's exact model ID. A custom endpoint works only if it accepts the same chat-completions request and response format. This is not a universal adapter for every API; providers with different formats need their own adapter. The browser can also block a request if the provider does not permit cross-origin calls (CORS). In that case, paste the answer instead.

## API key handling

Keys are saved in this browser's local storage so the static app can use them, and are excluded from downloaded backups. They are not embedded in `index.html` or sent to GitHub by the app. However, browser storage is not secure secret storage: people who can access the browser or run scripts on the page may be able to retrieve a key. Provider APIs receive the key with each request, and your prompt is sent when you generate an answer or ask Gemini to judge.

This architecture is convenient for a personal demo, but it is not appropriate for protecting valuable production keys. Use keys with provider-side restrictions and low usage limits; revoke a key if you think it was exposed. A production service normally keeps provider keys on a backend, which this GitHub Pages-only project does not have.

## Solo reviews, comparisons, and judging

Select one AI for a solo review or two or more for a blind comparison. Solo reviews save trait tags and participation, but do not count as head-to-head wins, Elo matches, or Gemini agreement. In comparisons, make your own pick before requesting Gemini's scores. Gemini rates accuracy, clarity, completeness, and tone and includes its own answer if one is in the set.

## Backup and restore

- Tap **Download full backup** before clearing browser data or moving to another browser/device. It contains settings, rounds, and provider profile details, but no API keys. Elo and charts are recalculated from the imported rounds.
- On the new browser, choose the backup file and import with **Replace local history** selected. Enter the API keys again on that browser.
- **Add imported rounds** appends the history. Importing the same backup more than once can create duplicate rounds.
- **Copy history JSON** is a legacy `{weights, rounds}` export. Use **Download full backup** for a full transfer.

The app keeps the original `b4m2` storage key, so existing rounds in the same browser remain available. Older saved Gemini keys are migrated into a Gemini profile. Browser data can still be cleared by the browser, so keep the downloaded backup somewhere safe.

## API references

- [Gemini `generateContent` API](https://ai.google.dev/api/generate-content)
- [Anthropic Messages API](https://platform.claude.com/docs/en/api/messages)
- [Anthropic TypeScript SDK browser guidance](https://platform.claude.com/docs/en/cli-sdks-libraries/sdks/typescript)
- [OpenAI Chat Completions API](https://developers.openai.com/api/reference/resources/chat/subresources/completions/methods/create)
- [OpenAI API key safety guidance](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety)
- [OpenRouter API quickstart](https://openrouter.ai/docs/quickstart)
