# Novel Autocomplete Studio

A local-only prototype for fiction and novel-writing autocomplete.

This project is an experimental single-page editor that tries to provide GitHub Copilot-style inline completions for prose. It is aimed specifically at novel drafting rather than general note-taking, business writing, or chat.

## What it does

Novel Autocomplete Studio provides a browser-based writing editor with:

- Inline ghost-text suggestions accepted with `Tab`
- Local retrieval over an imported writing corpus
- TXT, Markdown, and PDF corpus import
- Google Docs paste handling for basic formatting
- Scene notes for steering context
- A corpus-derived style profile
- Local fallback autocomplete
- Optional LLM-backed autocomplete through the OpenAI Responses API
- Debouncing, request throttling, and backoff for HTTP 429 rate limits

The intended workflow is to open `index.html` locally, import prior writing, add scene notes, and draft inside the editor.

## Local-only warning

This is **not intended to be deployed**.

The current implementation is deliberately a local prototype. It allows entering an OpenAI API key directly in the browser page for convenience during local testing. That is not safe for a public website, GitHub Pages, shared demo, or hosted deployment.

If this project is ever turned into a deployed application, the LLM calls should be moved behind a small backend/proxy so the API key is never exposed to client-side JavaScript.

Do not publish this as a live site with your API key or anyone else's API key in it.

## How to run locally

Clone the repository, then open `index.html` directly in your browser:

```bash
git clone https://github.com/GrantDeljevic/novel-autocomplete.git
cd novel-autocomplete
open index.html
```

On Windows, double-clicking `index.html` should also work.

No build step is required.

## Using a corpus

Use **Import corpus** to load previous writing. TXT or Markdown is preferred for large corpora. PDF import is supported through PDF.js loaded from a CDN, but PDF extraction can be slower and messier depending on the file layout.

For very large writing corpora, export from Google Docs, Word, Scrivener, or another editor as plain text or Markdown when possible.

## Using LLM autocomplete

The LLM section is optional. Without it, the editor uses local retrieval and n-gram-style autocomplete.

To use LLM suggestions locally:

1. Enable **Use LLM for inline suggestions**.
2. Enter an API key.
3. Leave the endpoint as `https://api.openai.com/v1/responses`, or replace it with your own local proxy endpoint.
4. Adjust debounce and minimum request interval if you hit rate limits.

HTTP 429 responses trigger exponential backoff and local fallback instead of throwing a blocking error.

## Privacy notes

Corpus indexing happens in the browser for the local retrieval features. If LLM autocomplete is enabled, the editor sends selected context to the configured endpoint, including recent draft text, scene notes, style profile information, and retrieved excerpts.

For private writing, use this locally and understand what endpoint you are sending text to.

## Project structure

```text
index.html   # Single-file editor prototype
README.md    # Project explanation and local-only warning
.gitignore   # Basic ignores for local artifacts
```

## Status

Prototype. Expect rough edges. This is a drafting experiment, not production software.
