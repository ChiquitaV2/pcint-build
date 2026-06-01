# PCINT Translate Tool - Build Pipe

This repository serves as a **Shadow Build Runner** for the [PCINT Translate Tool](https://codeberg.org/bell/pcint-translate-tool) hosted on Codeberg.

## What is this project?
The **PCINT Translate Tool** is a specialized desktop application designed for researchers and archivists working with historical political journals from [pcint.org](https://www.pcint.org). It automates the extraction of complex, multi-language documents and provides a side-by-side translation environment.

## The Problem
Archived historical documents (like those on pcint.org) often suffer from:
1. **Legacy HTML Structures**: Difficult to parse or convert into modern, editable formats while preserving hierarchy.
2. **Complex Layouts**: Frequent use of nested lists, varying header styles, and mixed-language content.
3. **Translation Friction**: Manually copying hundreds of sentences between different translation engines (DeepL/Google) and a word processor is extremely slow and error-prone.

This tool solves these problems by:
- **Auto-Extracting**: Using a Python-based intelligent scraper that detects document hierarchy.
- **Unified Workflow**: Providing a single UI to compare multiple translations, swap words with alternatives, and export perfectly formatted documents (DOCX/CSV) instantly.

## Purpose of this Repository
Codeberg is the primary source of truth for the codebase. This GitHub repository exists solely to provide:

1. **Windows x86_64** builders.
2. **Linux x86_64** builders.
3. **macOS ARM64** builders.

It leverages GitHub's hosted runners to compile and bundle the application with python sidecar and automatically uploads the binaries back to the Codeberg Release page.

## How it Works
1. A **Forgejo Action** on Codeberg detects a new tag (e.g., `v1.2.0`).
2. Codeberg sends a `repository_dispatch` event to this GitHub repository.
3. This repository's workflow (`.github/workflows/build.yml`) clones the code from Codeberg.
4. It builds the binaries for all platforms using `wails` and `task`.
5. It uses the Codeberg API to upload the binaries as assets to the original release.
