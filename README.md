# MAIN CHANGES

Changed the code for export-chatgpt-console.js to handle my use-case. If you have a ridiculous amount of conversations (1000+) to export, this could help.
Refer to the fork here: https://gist.github.com/eileenthg/af15b92fcf73cf75fc9a6bbb14ff766e

Improvements:
- Increased delay time between fetches to avoid "Error 429: Too many requests"
- If fetch failed, retry until succeed. Up to 20 attempts. Delay time increases exponentially between attempts.
- Verbose logging in console (successful attempts and giving up)
- Batch download. My computer froze during ZIP export due to system memory overwrite errors, causing my computer to hang, reboot, and making me lose all my progress. My modification will export a ZIP for every approx 200 conversations.
- List of failed chat exports (ID and conversation title) at the end in console for manual exporting.
Note: This will take very long, about a whole day for me. You'll need to be patient. Also, it does not automate fixing file export issues.

========================================================================================================================================

# ChatGPT Conversation Exporter

Export all your ChatGPT conversations as **JSON + Markdown + HTML + ZIP**.
Works with ChatGPT Business/Team/Enterprise accounts (including SSO/Okta).

## What's exported

- **JSON** — Raw conversation data from the API
- **Markdown** — Clean text with headers per message, relative links to downloaded files
- **HTML** — ChatGPT-style conversation viewer with sidebar navigation, syntax-highlighted code blocks, and embedded images
- **Files** — All images (DALL-E, uploads), documents, and code interpreter outputs are downloaded alongside conversations

## Option 1: Browser Console (easiest, works for everyone)

1. Go to [chatgpt.com](https://chatgpt.com) and log in
2. Open the browser console: **Cmd+Option+J** (Chrome) or **Cmd+Option+K** (Firefox)
3. Copy-paste the contents of [`export-chatgpt-console.js`](https://gist.github.com/ocombe/1d7604bd29a91ceb716304ef8b5aa4b5/raw/export-chatgpt-console.js) and press Enter
4. A progress overlay appears → ZIP file downloads automatically

This runs directly in your browser — no Cloudflare issues, no token copy-paste.

## Option 2: Shell Script (terminal)
Please refer to original gist here: https://gist.github.com/ocombe/1d7604bd29a91ceb716304ef8b5aa4b5


## Troubleshooting

| Problem | Solution |
|---------|----------|
| **Token expired** | Tokens are short-lived. Re-open the session URL and copy again |
| **Console version: no overlay appears** | Make sure you're on chatgpt.com (not another site) |
| **Some files failed to download** | File download URLs can expire. Re-run the export if needed |
| **HTML pages look unstyled** | HTML files need internet access (once) to load marked.js and highlight.js from CDN |
