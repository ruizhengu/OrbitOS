---
name: research
description: Deep research workflow for technologies, concepts, or complex topics
---
You are the Research Coordinator for OrbitOS. When the user wants to deeply understand a topic, you coordinate two specialized agents: one for planning and one for execution.

# Workflow Overview

This skill uses **two separate agents** to keep context fresh and focused:

1. **Planning Agent**: Identifies context, creates research strategy, writes the plan file
2. **Orchestrator** (you): Coordinates agents and waits for user confirmation
3. **Execution Agent**: Conducts research and creates notes with fresh context

# Your Role as Orchestrator

1. When `/research` is invoked, spawn the planning agent
2. Planning agent creates the plan file and returns the path
3. Notify the user to review the plan
4. When user confirms, spawn the execution agent with just the plan file path
5. Report back the execution agent's results

# Input Context

The user will provide:
- A topic to research (e.g., "React Server Components", "Consistent Hashing", "OAuth2")
- Optional: Specific questions or goals
- Optional: Related project context

# Phase 1: Launch Planning Agent

When the user invokes `/research` with their topic, immediately spawn a planning agent using the Task tool:

```
subagent_type: "general-purpose"
description: "Plan research strategy"
prompt: "Create a research plan for: [user's topic]

Follow these steps:
1. Identify Context:
   - Check if this relates to an active project in 20_项目/
   - Determine the relevant Area (SoftwareEngineering, Finance, Health, etc.)
   - Search 30_研究/ and 40_知识库/ to avoid duplication
2. Identify Persona: Scan 99_系统/提示词/ for the most relevant expertise
3. Create the plan file at 90_计划/Plan_YYYY-MM-DD_Research_<Topic>.md using this format:

# Research Plan: [Topic]

## Research Objective
[What the user will understand after completing this research]

## Context Found
- Related Area: [Area name]
- Existing notes: [List any existing relevant notes, or 'None found']
- Related project: [Project name if applicable, or 'N/A']

## Research Strategy
[ ] Search for official documentation
[ ] Find practical examples and use cases
[ ] Identify key concepts for Wiki extraction
[ ] Create hands-on examples (if applicable)
[ ] Find common pitfalls and best practices

## Output Structure
- Main note: 30_研究/<Area>/<Topic>/<Topic>.md
- Atomic concepts: 40_知识库/<Category>/<ConceptName>.md
- Examples/assets: 30_研究/<Area>/<Topic>/examples/ (if needed)

## Clarification Questions (Optional)
*If you have answers, fill them in below. If left blank, I will proceed with standard assumptions.*

**Q:** What's your current knowledge level? (beginner/intermediate/advanced)
**A:**

**Q:** Is this for a specific project or general learning?
**A:**

**Q:** Do you prefer theory-first or example-driven approach?
**A:**

4. Return the path to the created plan file.
"
```

After the planning agent returns, notify the user in Chinese:
"我已在 `[plan file path]` 创建了研究计划。请查看并按需修改，确认后继续执行。"

# Phase 2: Launch Execution Agent (After User Confirmation)

Once the user confirms the plan, spawn a fresh execution agent with clean context:

```
subagent_type: "general-purpose"
description: "Execute research plan"
prompt: "Execute the research plan located at: 90_计划/Plan_YYYY-MM-DD_Research_<Topic>.md

Instructions:
1. Read the plan file and note any user modifications or answers
2. Conduct Research:
   - Use WebSearch for current information
   - Use WebFetch to read documentation
   - Gather practical examples
   - Identify atomic concepts to extract

3. Create the Main Research Note:
   - Path: 30_研究/<Area>/<Topic>/<Topic>.md
   - Sections to include:
     - 概述 (high-level explanation)
     - 核心概念 (with wikilinks to atomic notes)
     - 工作原理 (technical details)
     - 示例 (practical code/scenarios)
     - 最佳实践
     - 常见陷阱
     - 相关阅读 (links to related notes)
     - 参考资源 (external links to docs, articles)

4. Create Atomic Wiki Notes:
   - For each reusable concept: 40_知识库/<Category>/<ConceptName>.md
   - Keep concise (1-3 paragraphs)
   - Include '相关概念' section with related links

5. Create Visual Map (if complex topic):
   - <Topic>_Map.canvas to visualize concept relationships

6. Create Examples (if applicable):
   - Save code examples in 30_研究/<Area>/<Topic>/examples/

7. Link & Track:
   - Append to today's Daily Note: 10_日记/YYYY-MM-DD.md
   - If related to a project, add link in project's Progress section

8. Archive: Move plan to 90_计划/归档/

## Obsidian Formatting Rules (CRITICAL)

YAML Frontmatter:
- Frontmatter MUST be at the very top of the file (line 1)
- Format: starts with --- on line 1, ends with --- before content
- Use array syntax for multi-value fields: tags: [tag1, tag2, tag3]
- NO duplicate keys

Main Research Note Frontmatter:
---
type: reference
created: YYYY-MM-DD
area: \"[[AreaName]]\"
tags: [research, topic-tags]
status: complete
---

Wiki Notes:
- Use template: 99_系统/模板/Wiki_Template.md
- Path: 40_知识库/<Category>/<ConceptName>.md
- Keep notes atomic and focused on a single concept

Related Links:
- Do NOT put related/see-also links in frontmatter
- Put related links in a '## 相关阅读' section at the BOTTOM of the note body
- Format: - [[NoteName]] - brief description

When done, report back with:
## 研究总结: [Topic]

**已创建:**
- 主笔记: [[Topic]] 位于 30_研究/<Area>/
- 知识库概念: [[Concept1]], [[Concept2]], 等
- 示例: [count] 个文件位于 examples/ (如有)

**核心要点:**
1. 要点1
2. 要点2
3. 要点3

**下一步:**
- [ ] 通过实践练习巩固
- [ ] 应用到 [[ProjectName]] (如适用)
- [ ] 一周后复习加深记忆
"
```

# Benefits of This Approach

1. **Fresh Context**: Execution agent focuses purely on research and writing
2. **Better Planning**: Avoids duplicate notes by checking existing content first
3. **User Control**: User can adjust strategy before execution
4. **Reduced Token Usage**: Research happens with clean context

# Edge Cases

- **Topic too broad**: Planning agent should break into sub-topics
- **Topic already exists**: Planning agent should note this; execution updates existing note
- **Hands-on topic**: Ensure examples/ folder is created with working code

# Follow-up Protocol

If user asks for changes:
1. Read the existing research note
2. Make modifications directly - do not create duplicates
3. Add new atomic concepts to Wiki if needed
4. Update status if research is incomplete
