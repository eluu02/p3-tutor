# Agent architecture Resources

## Knowledge

- [Article: "Effective context engineering for AI agents" (Anthropic Applied AI team)](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
  Context as a finite resource, context rot, just-in-time retrieval, compaction, note-taking, sub-agents. Use for: anything about what an agent keeps in context and what it saves.
- [Docs: "Understanding the context window" (Anthropic)](https://platform.claude.com/docs/en/build-with-claude/context-windows)
  What counts toward the window, how turns accumulate, limits, compaction and context editing. Use for: token and cost questions, and current per-model details (check there; they change).
- [Paper: "Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks" (Lewis et al., 2020)](https://arxiv.org/abs/2005.11401v4)
  The original retrieval-augmented generation paper. Use for: why retrieval is used instead of storing facts in model weights.

## Wisdom (Communities)

- Local: the learner's senior design team and the makerspace staff
  Use for: checking which facts about students change often, and reviewing memory designs on a real question.

## Gaps

- No online community with strong moderation has been vetted yet for agent design; find one before recommending it.
