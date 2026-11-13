---
layout: default
title: Software Projects | mjselan
description: High-performance, cross-platform native desktop applications built with C++20 and Qt 6.
---

# Selected Projects

High-performance, offline-first native desktop software built with **C++20**, **Qt 6**, and **CMake**. Designed for Windows, macOS, and Linux with native OS integration, secure credential handling, and zero telemetry.

---

## 1. Google AI Studio Viewer

> **A native desktop application for browsing, searching, and organizing Google AI Studio conversation histories.**

Google AI Studio stores chat prompts and session outputs as `.prompt` JSON files inside Google Drive. However, Drive does not index prompt JSON files for full-text search, and managing deep session trees in the web UI can be cumbersome. 

**Google AI Studio Viewer** solves this by establishing a secure, read-only OAuth connection to Drive, synchronizing conversations into a fast local SQLite database, and providing an instant native three-pane browsing interface.

* **GitHub Repository:** [mjselan/Google-AI-Studio-Viewer](https://github.com/mjselan/Google-AI-Studio-Viewer)
* **Tech Stack:** `C++20` · `Qt 6 Widgets` · `SQLite` · `CMake` · `QtKeychain`
* **Platforms:** Windows · macOS · Linux

### Key Capabilities
* **Three-Pane Architecture:** Left sidebar for conversation discovery and sorting, center pane for turn-by-turn prompts, and right pane for markdown-rendered responses.
* **Offline Full-Text Search:** Sub-millisecond SQLite full-text index across conversation titles, prompts, system instructions, and responses.
* **Attachment Search & Parent Linking:** Resolves attachments stored in Drive directly back to their originating conversation.
* **Model "Thoughts" Inspector:** Dedicated toggleable inspector for model chain-of-thought reasoning blocks with high-contrast styling.
* **Secure Credential Storage:** RFC 7636 PKCE loopback handshake strictly requesting `drive.readonly`. Tokens are stored directly in native OS vaults (Windows Credential Manager, macOS Keychain, Linux Secret Service).
* **Quota-Aware Background Sync:** Automatic synchronization featuring rate-limiting and exponential backoff with jitter to stay safely within Google Drive API quotas.
* **Local LLM Backend:** Easily switch from Google AI Studio to any OpenAI-compatible local server (Ollama, LM Studio, llama.cpp) running on `localhost:8000`.

---

## 2. MdEditor (Markdown Editor)

> **A lightweight, offline-first native Markdown editor with live preview, syntax highlighting, and math rendering.**

**MdEditor** provides a responsive, native writing experience for technical documents and notes. Written from the ground up in modern C++20 and Qt 6 Widgets, it avoids the heavy memory overhead of browser-wrapped editors while maintaining complete privacy with zero network calls, accounts, or telemetry.

* **GitHub Repository:** [mjselan/MdEditor](https://github.com/mjselan/MdEditor)
* **Releases & Installers:** [Download v1.0.x](https://github.com/mjselan/MdEditor/releases)
* **Tech Stack:** `C++20` · `Qt 6 Widgets` · `CMake` · `Ninja` · `KF6Sonnet`
* **Platforms:** Windows · macOS · Linux

### Key Capabilities
* **Split View with Live Preview:** Throttled 250 ms live preview ensures smooth typing performance even on large documents exceeding 10,000 lines.
* **Incremental Syntax Highlighter:** Block-state tracked highlighter for headings, lists, quotes, inline code, and fenced code blocks.
* **GFM & Math Rendering:** Built-in CommonMark and GitHub Flavored Markdown support for tables and task lists, plus LaTeX math formulas (`$...$` and `$$...$$`) rendered to Unicode.
* **System Theme Awareness:** Automatically tracks system dark and light modes, drawing high-DPI vector icons in code with adaptive palette accent colors.
* **Crash Recovery & Autosave:** Silently captures recovery snapshots every 30 seconds to restore unsaved documents in case of unexpected termination.
* **Smart Clipboard Image Pasting:** Pasting an image automatically writes a PNG to an `assets/` subfolder and inserts the relative Markdown link.
* **Export & Packaging:** One-click export to PDF and HTML; pre-built native installers (Windows `.exe`, macOS `.dmg`, Linux `.run`) built with Qt Installer Framework.

---

## Core Engineering Principles

Both projects reflect a commitment to native desktop software design:

1. **Performance & Low Footprint:** Compiled C++20 binaries that launch instantly and consume minimal RAM.
2. **Privacy First:** Data remains on your local disk. SQLite storage and OS-level secure credential storage are used without telemetry.
3. **True Cross-Platform Parity:** Engineered to feel like a first-class citizen whether running on Windows 11, macOS, or desktop Linux.
