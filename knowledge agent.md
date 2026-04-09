# Knowledge Agent
*Second brain, semantic search, spaced repetition, and Obsidian vault management*

The Intelligence Agent finds and digests new information. The Knowledge Agent owns what you already know — connects, retrieves, strengthens, and surfaces it.

---

## Tools

| Tool                                          | Why                                                |
| --------------------------------------------- | -------------------------------------------------- |
| Obsidian vault reader/writer                  | Read and write .md notes directly                  |
| Vector database (Qdrant / ChromaDB)           | Embed and semantically search all notes            |
| Embedding model (local or API)                | Convert notes to vectors for semantic retrieval    |
| Spaced repetition engine (custom or Anki API) | Generate and schedule flashcards                   |
| Web fetch                                     | Resolve links in notes, fetch referenced resources |
| File watcher                                  | Detect new notes added to vault, trigger indexing  |
| Notification channel                          | Review reminders, connection surfacing             |

---

## Skills

### Retrieval & Search
- **Semantic search** — "what do I know about X?" — finds relevant notes even when exact keywords don't match
- **Concept lookup** — given a term, return your own notes about it plus gaps (what you haven't documented)
- **Cross-note connection finder** — scan vault for notes that should link to each other but don't
- **Orphan note detector** — surface notes with no backlinks that may be forgotten knowledge

### Knowledge Synthesis
- **Note summarizer** — given a note or cluster of notes, produce a concise synthesis
- **Topic map** — given a subject, produce a graph of everything you have on it (nodes = notes, edges = links)
- **Contradiction detector** — find notes that make conflicting claims; surface for resolution
- **Gap finder** — given what you know about a topic, identify what's missing and worth learning

### Learning & Retention
- **Flashcard generator** — from any note, extract key facts and generate Anki-compatible flashcards
- **Spaced repetition scheduler** — track what needs review today based on forgetting curve; send daily review set
- **Recall test** — given a topic, quiz you on your own notes; track recall performance
- **Learning streak tracker** — log daily review completions; track consistency

### Vault Health
- **Vault indexer** — on new file events, chunk and embed note into vector DB; keep index current
- **Note quality scorer** — flag notes that are too short to be useful, have broken links, or are outdated
- **Duplicate detector** — find near-duplicate notes that should be merged
- **Tag taxonomy maintainer** — suggest consistent tagging as new notes are added

### Intelligence Agent Integration
- **New learning intake** — when Intelligence Agent produces a summary, Knowledge Agent checks if it connects to existing notes and adds backlinks automatically
- **Reading list manager** — track to-read items, surface when you have bandwidth
- **Concept evolution tracker** — when a new note updates a prior belief, flag the old note as superseded

---

## Data Model

All notes stored in Obsidian as-is. Vector index is a separate sidecar:
- Each note chunked into paragraphs, embedded, stored with metadata (path, date, tags)
- Queries hit vector DB first, then fetch full note from vault
- Index rebuilt nightly or on file-change events
