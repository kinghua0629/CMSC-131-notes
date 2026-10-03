# Repository Guidelines

## Project Structure & Module Organization

This repository is an Obsidian vault of personal study notes for UMD CMSC131 (Java, Fall 2026). All content lives at the repository root:

- `CMSC131 Notes For Exam 1.md`: exam review organized by lecture topic, with a checklist and Java templates.
- `Notes for writing code on paper.md`: personal advice for handwritten exam answers.
- `README.md` and `README.zh-CN.md`: English and Chinese introductions and navigation.
- `CLAUDE.md`: existing agent instructions and course-scope guidance.

There are no application sources, test directories, or bundled course assets. Leave `.obsidian/` configuration untouched.

## Build, Test, and Development Commands

No build system, package manager, formatter, linter, or automated test suite is configured.

- Open this directory with Obsidian’s **Open folder as vault** to read and preview notes.
- `git diff --check`: check changes for whitespace errors before committing.
- `git diff --stat` and `git diff`: review the scope and content of edits.

Run commands from the repository root; quote filenames containing spaces.

## Writing Style & Naming Conventions

Preserve the existing bilingual style: English for Java terminology and headings, Chinese for explanations and personal tips. Retain the author’s wording unless a correction is necessary.

Use descriptive Markdown headings, tables for type/operator summaries, and fenced `java` blocks for snippets. Follow surrounding indentation; use consistent four-space indentation in new Java examples. Use `camelCase` for variables and methods, `PascalCase` for classes, and `UPPER_SNAKE_CASE` for constants.

Use Obsidian links such as `[[Notes for writing code on paper]]`. Avoid renaming linked notes without updating references. Keep both READMEs aligned when navigation changes.

## Validation Guidelines

No test framework or coverage requirement applies. Preview edited notes in Obsidian, verify links and tables, and check Java examples and expected outputs. Label intentionally invalid examples clearly. For exam-scope changes, consult the official exam page linked in `README.md`.

## Commit & Pull Request Guidelines

Existing commits use short, imperative descriptions, such as `Add CMSC131 study notes, README and .gitignore`. Follow that pattern and keep each commit focused.

Pull requests should explain which notes changed, why, and how they were checked. Link relevant issues or course references when applicable; include screenshots only for rendering changes.

## Editing Boundaries

Edit only this repository. Treat parent-directory course materials as read-only sources; do not add course PDFs, assignments, or unrelated code to the vault.
