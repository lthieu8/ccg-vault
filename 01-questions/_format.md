# Question store format

One file per feature: `01-questions/<feature-slug>.md`, matching the spec name in `02-specs/`.

`/ask` appends here when the vault cannot answer something. `/ba-answer` resolves the open ones.
Entries are append-only — a changed answer gets a new entry that supersedes the old one and says
so.

## Entry format

```markdown
### Q: Do inactive suppliers appear in the evaluation dropdown?
- **Status:** answered
- **A:** No. Only suppliers with `IsActive = true`.
- **Answered by:** Hieu (BA), 2026-09-14
- **Relates to:** [[02-specs/supplier-evaluation#AC-2]]

### Q: What rounding applies to the aggregate score?
- **Status:** open
- **Asked by:** Nam (dev), 2026-09-16 — blocking
- **Needed for:** [[02-specs/supplier-evaluation#AC-7]]
- **Context:** Scores average to 3 dp; the UI column fits 1.
```

`Status` is `open` or `answered`. Blocking questions are marked so on the `Asked by` line, and
`/ba-answer` surfaces those first.
