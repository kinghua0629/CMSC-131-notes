# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

An Obsidian vault of personal study notes for UMD CMSC131 (Java, Fall 2026). There is no code, build, lint, or test tooling here — the work is writing and organizing Markdown notes.

## Read-only vs. editable

- **Editable:** only files inside this directory (`CMSC131-notes/`). Don't touch `.obsidian/`.
- **Read-only:** everything in the parent directory `/Users/kinghua/大学学习/CMSC/CMSC131/` (lecture PDFs under `Week 1`–`Week 5`, `Exams/`, `Quiz/`, `Project/`, `code/`, `Exam1.pdf`, `MemoryMapsInformation.pdf`, etc.). Read them as source material; never modify them.
- To read PDFs, extract text with `pdftotext -layout` into the session scratchpad rather than the course folders.

## Notes layout

- `CMSC131 Notes For Exam 1.md` — main exam-review note, organized by lecture topic (sections 0–11, ending with a checklist and code templates).
- `Notes for writing code on paper.md` — the user's own tips for handwritten code on exams (Chinese). Linked from the main note with Obsidian `[[wikilink]]` syntax.

## Conventions

- Language: mix of English (Java terms, headings, rules quoted from slides) and Chinese (explanations/tips). Match the existing mix; keep the user's own wording when editing their content.
- Java snippets go in fenced ```java blocks; use tables for type/operator summaries.
- **Scope follows the official exam page** (https://www.cs.umd.edu/class/fall2026/cmsc131-03XX-04XX/exams/exam1/), whose scope is stated at the top of the Exam 1 note. Exam 1 does **not** cover StringBuffer/StringBuilder, pseudocode, constructors, instance variables, non-static methods, `toString`/`equals` definitions, or heap/stack/memory maps — don't add those back. Check that page again when scope questions come up for later exams.
