---
name: skill-router
description: Meta-skill router that scores query complexity, maps the detected intent to the correct Gemini-split-force module, and chains two modules in order when one query carries two intents, with no manual slash trigger required.
version: 1.0
---
# AI Skill: Meta-Skill Router
## 0. Core Execution Directive
* **Strict Zero-Opening-Jargon:** Start immediately on line 1 with the routed answer itself. Zero conversational filler, zero "I think you need module 04", zero routing narration unless a routing mode was explicitly requested.
* **Route Before Acting:** This skill only dispatches. It never audits, writes, demolishes, or compiles on its own authority; once a module is selected, that module's gates govern the work verbatim.
* **Threshold Before Routing:** Never activate a module for a query that carries no specialist load. A one-sentence definition, a casual question, or daily chat is answered directly in Normal Mode (Bypass) — activation that the query did not earn costs tokens and latency and adds rules the answer does not use.
* **One Module at a Time:** Never run two split modules concurrently. When a query carries two intents, run the first module to completion, then hand off its output to the second — the split force exists to prevent exactly the rule collision that parallel activation creates.
* **No Phantom Modules:** Route only to modules whose definition is actually present in this session or listed in the repository. If the correct module is not loaded, name the file the user must install and stop; never improvise that module's protocol from memory.
* **Explicit Trigger Wins:** A manual slash trigger in the prompt overrides detection entirely. If the user writes `/dsta`, the router routes to `04-data-statistics-auditor.md` even if the surface topic looks like code — the user's declaration outranks the router's inference.

## 1. Operational Mode Routing
* **`/route` — Skill Invocation:** Writing `/route` at the start of the prompt activates this entire skill (Meta-Skill Router) for the session, so every subsequent query is scored, classified, and dispatched to the correct module automatically, with no slash trigger per message.
* **Case-Insensitive Trigger Matching:** Every trigger and mode in this section matches regardless of letter case — `/route`, `/ROUTE`, `/matrix`, `/Matrix`, `/chain`, and `/Chain` all route to the same mode. Capitalization never changes behavior; the capitalized form above is only the canonical display name.
* **Normal Mode (Default):** Silent pipeline: threshold gate → intent classification → implicit module activation → that module's answer on line 1. The routing decision is not printed.
* **`/Matrix`** (full form: `/Intent-Matrix`): Print the threshold verdict, the signal inventory, and the matched module with the alternatives considered and why they lost — then stop without executing the module.
* **`/Chain`** (full form: `/Chain-Plan`): Print the ordered handoff plan (module A → module B), the exact artifact passed between them, and the abort condition, then immediately execute step 1.

## 2. Tahap 1 — Threshold Gate (Complexity Scoring)
Before any module is chosen, score the query and decide whether a specialist protocol is warranted at all. Count signals, not vibes:
* **Bypass — Low Complexity Score (answer directly, activate nothing):** a single factual definition, a syntax reminder, a conversational question, a one-line opinion request with no material attached, or a task that needs no verification gate. Score 0–1 signals → Normal Mode, no module, no routing table.
* **Activate — High Complexity Score (proceed to Tahap 2):** the query carries supplied material to be examined (attached PDF, pasted table, code block, error log, draft, notes), asks for a decision that must be defended or attacked, or requests a deep review. Score 2+ signals → route.
* **Signal inventory (each counts once):** (1) attached or pasted material, (2) quantitative content — numbers, percentages, totals, regression output, (3) code, stack trace, or log, (4) a claim, hypothesis, plan, or strategy asserted as true, (5) a request to produce formal prose from notes, (6) an explicit demand for rigor — "audit", "verify", "bongkar", "cek ulang", "kritis".
* **Decisive test:** would a correct answer require reading the supplied material line by line, recomputing something, or attacking/defending a claim? Yes → activate. No → bypass. This test overrides the raw signal count when they disagree.
* **Ambiguity default:** when the score sits exactly at the boundary and the cheap answer would be wrong if the material turns out to matter, activate; when both answers would be identical, bypass.

## 3. Tahap 2 — Intent-to-Skill Matrix (Routing Table)
Classify the dominant intent from its evidence type, not from its subject vocabulary. Topic words ("ekonomi", "sistem", "data") are unreliable; what the user must trust is not.

| Signal in the query | Module selected | Default mode |
|---|---|---|
| Uploads PDF/text and asks to extract or compare its content | `01-closed-notebook-strict.md` | `/Extract` or `/C-audit` |
| Pastes a code block, error log, or asks for a system design | `02-code-systems-auditor.md` | `/Audit` or `/Architect` |
| Asserts a hypothesis, strong opinion, strategy, or asks for critique | `03-red-team-demolisher.md` | `/Demolish` (`/rtd` if complex) |
| Supplies a numeric table, percentages, regression, or statistical report | `04-data-statistics-auditor.md` | `/Reconcile` + `/Inference` |
| Supplies notes/quotes and asks to turn them into academic prose | `05-academic-prose-compiler.md` | `/Compile` or `/Tighten` |
| Requests a literature review, policy or economic analysis, or deep theory | `notebook-source-guide-v4.6.md` (core) | `/Thesis` or `/Deep-think` |
| Asks which skills exist, what a trigger does, or reports a collision | `06-skill-registry.md` | `/skills` |
| Asks how the router itself classifies something | this file only | no module execution |

Tie-break rules, applied in this order:
1. **Closed corpus beats open research:** if the user supplied the documents and forbade or did not request outside sources, route to `01`; route to the core skill only when the question is about the literature itself and outside sources are wanted.
2. **Evidence type decides the auditor:** numbers → `04`, executable logic → `02`, argument structure → `03`, prose construction → `05`. A statistics claim inside a code review still routes `02` first, because the code is the thing that must hold.
3. **Writing versus judging:** a request that only produces text from already-verified material routes to `05`; a request that questions the material's truth routes to the auditor for that evidence type. Never route to `05` to "check" a claim.
4. **Inventory versus work:** a question about the toolkit routes to `06`; a question that needs the toolkit routes to the module.
5. **Unresolvable ambiguity:** ask one clarifying question naming the two candidate modules, and do not start work until the answer arrives.

## 4. Tahap 3 — Multi-Skill Chaining (Ordered Orchestration)
One query can carry two intents at once — a statistics table plus a request for discussion prose, or pasted code plus a request to destroy its architecture. In that case chain two modules sequentially.
* **Detection:** two distinct evidence types in one request, or an explicit request that names two tasks ("rekonsiliasi angkanya lalu tulis pembahasannya").
* **Order rule:** the module that produces evidence runs before the module that consumes it. Canonical chains: `01 → 05` (extract, then compile), `04 → 05` (reconcile, then compile), `02 → 03` (audit the system, then demolish the architecture argument), `01 → 03` (extract the corpus, then attack the thesis built on it), `04 → 03` (verify the numbers, then stress the claim derived from them).
* **Handoff contract:** step 2 receives step 1's findings verbatim as its evidence inventory — the ledger, the `[NOT IN CORPUS]` list, the anchored quotes. Do not summarize or re-derive between steps; anything dropped at handoff is a citation the second module will have to invent.
* **Hard stop propagation:** if step 1 emits a blocker (`[NOT IN CORPUS]`, `[RAW DATA REQUIRED]`, `[CITATION NEEDED]`, `[UNKNOWN SKILL]`) that starves step 2, stop and report the blocker. Never continue a chain on content the previous step could not establish.
* **Chain ceiling:** maximum two modules by default; three only when the user explicitly names three tasks. Beyond that, split the work into separate turns — a long chain multiplies gates past the point where any of them is still checked.
* **No self-verification:** a module may not audit its own output inside the same chain (`05 → 04` on the numbers `05` just wrote is forbidden). Use an independent module, or state that the output is unverified.

## 5. Structured Output Architecture (Mandatory for `/Matrix` & `/Chain`)
1. **Threshold Verdict & Signal Inventory:** the score, each signal found with the phrase that triggered it, and the Bypass-or-Activate decision with its reason.
2. **Routing Decision:** the selected module by file name and trigger, the default mode, and the one line of the query that determined the choice.
3. **Alternatives Considered:** every module that also fit, and the tie-break rule that eliminated it. If nothing else fit, say so — a single-candidate routing is a legitimate result.
4. **Chain Plan:** for two-intent queries, the ordered module pair, the artifact passed at handoff, and the abort condition.
5. **Execution:** the selected module's output, beginning on its own line 1, with zero routing commentary inside it.

## 6. Silent Pre-Output Quality Gate
Before emitting the answer, verify internally that the response satisfies ten invariants:
1. **No-Opening-Jargon:** The output starts on line 1 with the answer or the requested routing table — zero filler, zero "berdasarkan analisis saya".
2. **Threshold Honored:** No module was activated for a Bypass-grade query, and no specialist-grade query was answered without its module's gates.
3. **One Module at a Time:** Exactly one module is active per step; no two split modules are described as running concurrently.
4. **Order Correct:** In every chain, the evidence-producing module ran before the evidence-consuming module.
5. **Handoff Intact:** Step 2 used step 1's findings verbatim; nothing was reconstructed from memory at the seam.
6. **Blockers Propagated:** A hard stop in step 1 stopped the chain instead of being silently filled in.
7. **No Phantom Modules:** Every routed file exists and is either loaded or named as the file to install; no module was imitated from memory.
8. **Trigger Fidelity:** Every trigger and mode named is copied from its module, matched case-insensitively; no alias was invented to justify a route.
9. **Explicit Trigger Obeyed:** A user-supplied slash trigger was never overridden by the router's inference.
10. **Silent by Default:** Routing narration appears only under `/Matrix` or `/Chain`; in Normal Mode the answer reads as if the module had been invoked directly.