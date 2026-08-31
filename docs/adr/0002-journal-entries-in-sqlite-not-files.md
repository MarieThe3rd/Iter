# Journal entries stored in SQLite, not as Markdown files

Journal entries (per-Node notes) support Markdown formatting, which raised the question of storing them as literal `.md` files with YAML frontmatter — Obsidian/Jekyll-style, editable outside the app and git-versionable. We considered it and decided against it: SQLite is the sole source of truth for entries. Structured fields (date, Node reference, Level, tags) are real database columns rather than embedded YAML frontmatter, so filtering and sorting (e.g. "everything at Beginner level tagged Azure from last month") stays a plain SQL query instead of scanning and parsing every file on disk. Only the entry's free-text body is stored as a Markdown string.

File-based editing and git history on the notes themselves were appealing but not a stated requirement, and remain addable later as an export/sync feature without changing the core model.
