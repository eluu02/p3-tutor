# Agent architecture Resources

## Knowledge

- [Article: "Effective context engineering for AI agents" (Anthropic Engineering)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
  Context as a limited budget, context rot, compaction, note-taking, sub-agents, just-in-time retrieval. Use for: any decision about what the assistant keeps in context.
- [Docs: Context windows (Claude Platform)](https://platform.claude.com/en/docs/build-with-claude/context-windows)
  How the window fills turn by turn and what happens at the limit. Use for: window sizes and overflow behavior (check current numbers there).
- [Docs: Memory tool (Claude Platform)](https://platform.claude.com/en/docs/agents-and-tools/tool-use/memory-tool)
  File-based memory in `/memories`, stored by your own code. Use for: designing notes that persist between sessions.
- [Article: "Introducing Contextual Retrieval" (Anthropic)](https://www.anthropic.com/news/contextual-retrieval)
  Chunking, embeddings, keyword search and adding context to chunks. Use for: designing manual search.
- [Paper: "Lost in the Middle" by Liu et al.](https://huggingface.co/papers/2307.03172)
  Models use information at the start or end of a long input better than the middle. Use for: arguing against stuffing long contexts.

## Wisdom (Communities)

- Local: makerspace staff and past student users
  Use for: collecting real questions and sorting them into notes, retrieval and tools.
