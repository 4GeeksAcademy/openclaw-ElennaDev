# USER.md - User Model

Store stable user preferences and profile facts as directives that can guide future sessions.

Use one directive per entry:
```
<!-- observed: YYYY-MM-DD | status: active -->

- Prefer concise progress updates during implementation work.
```
- Begin each directive with an imperative such as `Always`, `Never`, or `Prefer`.
- Record the observation date and either `active` or `superseded` on the metadata line.
- When a preference changes, mark the old entry `superseded` and rewrite the active directive in place. Never append a contradictory active directive.
- Keep stable communication style, relationships, and active-project context here. Put durable non-profile facts and decisions in `MEMORY.md`.
- Save this file at the workspace root as `USER.md`. It loads every session with a separate 4,000-character budget.

**Directives**

<!-- observed: 2026-11-16 | status: active -->

- Prefer responses with more detail.

<!-- observed: 2026-11-16 | status: active -->

- Prefer a warm, informal tone.

<!-- observed: 2026-11-16 | status: active -->

- Prefer information organized in bullet lists.

<!-- observed: 2026-11-16 | status: active -->

- Always respond in Spanish.

<!-- observed: 2026-11-16 | status: active -->

- Never guess; clearly say when you are unsure and check the information.

## Related

- [Agent workspace](/concepts/agent-workspace)
