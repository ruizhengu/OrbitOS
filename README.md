# OrbitOS

English | [中文](README_CN.md)

> An **AI-powered** personal productivity system where **knowledge management** and **daily task planning** are intelligently orchestrated by your AI assistant.

![Screenshot](50_Resources/Screenshot.png)

## What is OrbitOS?

OrbitOS is an Obsidian-based productivity framework designed around a simple principle: **everything orbits around you**. Your projects, knowledge, and daily tasks stay in motion and connected — all managed through natural language conversations with AI.

Unlike traditional note-taking systems that require manual organization, OrbitOS leverages **Claude Code** or **Gemini CLI** as your intelligent knowledge manager and daily planner. The AI doesn't just store your information — it actively helps you:

- **Capture ideas** and transform them into structured, actionable projects
- **Plan your day** with context-aware recommendations based on your active work
- **Research topics** and automatically organize findings into your knowledge base
- **Connect the dots** between notes, projects, and concepts through smart wikilinks
- **Archive and clean up** completed work to keep your system lean and focused

## Key Features

### AI-Driven Workflows

Every major workflow is initiated through simple slash commands, with the AI handling the heavy lifting:

| Workflow              | What the AI Does                                                                                      |
| --------------------- | ----------------------------------------------------------------------------------------------------- |
| **Daily Planning**    | Reviews yesterday's progress, surfaces active projects, recommends focus areas, processes inbox items |
| **Project Creation**  | Converts rough ideas into structured projects with objectives, phases, and success metrics            |
| **Research**          | Conducts deep dives, structures findings, creates atomic wiki entries, builds knowledge connections   |
| **Knowledge Parsing** | Takes unstructured text and organizes it into your vault with proper categorization and linking       |
| **Archiving**         | Identifies completed items and moves them to archives while preserving historical context             |

### Intelligent Knowledge Graph

OrbitOS uses wikilinks extensively to build a connected knowledge graph:

- **Projects** link to related **Research** notes for context and reference
- **Daily notes** link to projects you worked on each day
- **Wiki entries** are atomic concepts that can be referenced from anywhere
- **Research notes** synthesize information and link to source concepts

The AI automatically creates these connections as you work, building a web of knowledge over time.

### Structured Yet Flexible

The folder structure provides clear organization while remaining adaptable:

```
├── 00_Inbox/          # Quick captures — the AI processes these into proper locations
├── 10_Daily/          # Daily logs (YYYY-MM-DD.md) — AI-generated each morning
├── 20_Project/        # Active projects — AI helps create and track progress
├── 30_Research/       # Deep research notes — AI-structured from your explorations
├── 40_Wiki/           # Atomic concepts — AI extracts reusable definitions
├── 50_Resources/      # Curated content — newsletters, product launches, references
├── 90_Plans/          # Execution plans — AI drafts, you approve, then archived
└── 99_System/         # System configuration
    ├── Archives/      # Historical records (organized by year/month)
    ├── Prompts/       # AI personas for different domains
    └── Templates/     # Markdown templates for consistency
```

---

## Getting Started

### Prerequisites

- [Obsidian](https://obsidian.md/) installed with this vault opened
- **Claude Code** or **Gemini CLI** configured and running in the vault directory

### Your First Day

1. **Capture your first idea**: Drop a quick note in `00_Inbox/`.
   - Just write down a thought, project idea, or something you want to explore
   - Don't worry about formatting — the AI will help structure it later

2. **Start your day**: Run `/start-my-day` in your AI assistant
   - The AI will scan your inbox and surface items to process
   - Review any active projects (empty on day one, and that's okay!)
   - Generate a daily note with recommendations

3. **Kick off a project**: Run `/kickoff` to transform an inbox item into a project
   - The AI will draft a plan and ask clarifying questions
   - Creates a structured project with objectives, phases, and success metrics

4. **Research something**: Run `/research <topic>`
   - The AI conducts a thorough investigation
   - Creates structured notes in `30_Research/`
   - Extracts atomic concepts to `40_Wiki/`
   - Links everything together automatically

5. **Ask a quick question**: Run `/ask <question>`
   - Get a direct answer without creating heavy documentation
   - Optionally save useful findings to your wiki

---

## Command Reference

### Core Workflows

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/start-my-day` | AI-guided daily planning and review | Every morning to set your focus |
| `/kickoff` | Transform ideas into structured projects | Starting any new initiative |
| `/research` | Deep dive with automatic knowledge structuring | Learning something comprehensively |
| `/ask` | Quick answers without heavy note-taking | Simple questions, fact lookups |
| `/brainstorm` | Interactive idea exploration | Developing and refining concepts |
| `/parse-knowledge` | Structure unstructured text into vault | Processing notes, articles, meeting transcripts |
| `/archive` | Clean up completed items | Regular maintenance, project completion |

### Obsidian-Specific Features

| Skill | Purpose |
|-------|---------|
| `obsidian-markdown` | Wikilinks, callouts, embeds, and Obsidian-flavored syntax |
| `obsidian-bases` | Create database-like views with filters and formulas (.base files) |
| `json-canvas` | Visual mind maps and flowcharts (.canvas files) |

### Content Curation (Optional)

| Command           | Purpose                                                            |
| ----------------- | ------------------------------------------------------------------ |
| `/ai-newsletters` | Curate and summarize AI newsletters (TLDR AI, The Rundown AI)      |
| `/ai-products`    | Discover AI product launches from Product Hunt, HN, GitHub, Reddit |

---
## Project Concepts
### The C.A.P. Project Layout

Every project follows a consistent structure:

- **Context**: What are we trying to achieve? What does success look like?
- **Actions**: Phased checklists of tasks to complete
- **Progress**: Timestamped updates linking to daily notes

### Wikilinks and Connections

OrbitOS relies heavily on Obsidian's wikilink syntax:

```markdown
[[NoteName]]                  # Basic link
[[NoteName|Display Text]]     # Custom display text
![[NoteName]]                 # Embed entire note
![[NoteName#Section]]         # Embed specific section
```

The AI creates these links automatically, but you should also link liberally — connections create value.

### Daily Notes as the Anchor

Daily notes (`10_Daily/YYYY-MM-DD.md`) serve as your central anchor:

- Every project update references the daily note where work happened
- Inbox items are processed and linked from daily notes
- The `/start-my-day` workflow generates these automatically

---

## Philosophy

OrbitOS is built on these principles:

1. **AI as Partner**: The AI isn't just a tool — it's an active collaborator that understands your system and helps maintain it
2. **Capture Everything, Process Later**: The inbox exists so you never lose an idea; the AI helps you process when ready
3. **Connections Over Categories**: Rigid folder hierarchies fail; wikilinks create a flexible, queryable knowledge graph
4. **Daily Rhythm**: The daily note anchors everything, creating a timeline of your work and thoughts
5. **Progressive Formalization**: Ideas start rough and become structured over time through AI-assisted refinement

---

## License

MIT License — Use freely, modify as needed, share with others.
