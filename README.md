# CCG BA Documentation

The single source of truth for what the team is building. Code answers *how*; this vault answers
*what* and *why*.

## You are not meant to read this by hand

This vault exists so that **Claude can answer your questions from it**. Do not go hunting through
folders for a rule you half-remember — ask:

```
/ask does the evaluation export honour the SupplierReview permission?
```

Claude searches the specs, the question store, the decisions log and the glossary, then either
quotes the answer with a citation, tells you precisely which part is unspecified, or returns
**NOT SPECIFIED** and offers to queue the question for the BA.

It will never guess. If the vault does not say it, Claude does not tell you it — not from the
code, not by analogy with another feature, not from what seems obvious. An answer you can act on
without double-checking is the entire point; a plausible guess would destroy that.

Requires the `ccg-ba` plugin, and the `CLAUDE.md` it ships in your source repo — that file is what makes
these rules apply to every question you ask, not only the ones you remember to prefix with `/ask`.

Everything here is plain markdown, so the files are readable without Obsidian if you ever
need to look.

## Layout

| Folder | Holds | Written by |
|---|---|---|
| `00-inbox/` | BA source documents, as delivered | BA. Never edited after drop. |
| `01-questions/` | Q&A store, one file per feature. Answered and open. | `/ask` queues, `/ba-answer` resolves |
| `02-specs/` | Validated specs. The primary source of truth. | BA, via `/ba-new` and `/ba-check` |
| `reports/` | Gap-check output. Disposable. | `/ba-check` |
| `notes/glossary.md` | Domain vocabulary | Anyone, one definition per term |
| `notes/decisions.md` | Cross-cutting answers spanning features | `/ba-answer` |

## The one rule

**The question store and decisions log are append-only.** When an answer changes, a new entry
supersedes the old one and says so. Overwriting destroys the record of why earlier code was
written the way it was.

## For the BA

Developers queue questions Claude could not answer. Clear them:

```
/ba-answer
```

This is the habit the whole thing rests on. If open questions pile up unanswered, developers learn
that asking returns nothing useful and go back to messaging you directly — which is the bottleneck
this was built to remove.

When an answer turns out to be a real requirement rather than a clarification, update the spec
too. An answer that lives only in the question store leaves the spec still incomplete, and
`/ba-check` will keep reporting the same gap.

## Keeping in sync

```bash
git pull
```

Claude pulls before answering when it can. Push after `/ba-answer` and after editing a spec so the team
sees new decisions — an answer sitting uncommitted on the BA's laptop helps nobody.
