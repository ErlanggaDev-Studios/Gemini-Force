---
name: skill-registry
description: Installed-skill inventory and trigger index that reports every loaded skill with a one-line function, verified against the actual skill definitions with zero invented skills or triggers.
version: 1.0
---
# AI Skill: Skill Registry & Trigger Index
## 0. Core Execution Directive
* **Strict Zero-Opening-Jargon:** Start immediately on line 1 with the registry itself. Zero conversational filler, no "here is the list you asked for", no closing summary.
* **Presence Before Mention:** A skill may only appear in the registry if its definition is actually present in this session's context or was supplied by the user. A skill that is merely documented elsewhere is labeled `[DOCUMENTED]`; a skill the user names but that cannot be found is `[UNKNOWN SKILL]`. Never fill the gap from memory.
* **Zero-Omission Rule:** Never present a partial list as complete. State the count of registered skills and the scope scanned (session, uploaded files, named directory). If only some definitions were readable, say which ones were not.
* **One Line, One Job:** Each function line names what the skill does to the work — its gate, its output, or its refusal rule — in at most 20 words. Never describe a skill with adjectives ("powerful", "strict", "advanced") instead of its mechanism.
* **Trigger Fidelity:** Triggers are copied character-for-character from each skill's own Section 1. No renaming, no inventing an alias because it "reads better", no merging two triggers into one row.

## 1. Operational Mode Routing
* **`/skills` — Skill Invocation:** Writing `/skills` at the start of the prompt activates this entire skill (Skill Registry & Trigger Index) and prints the compact arrow registry of every installed skill.
* **Normal Mode (Default):** One line per skill in the canonical form `/trigger → function`, grouped by family (core, split force, project-local), in declaration order.
* **`/Map`** (full form: `/Skill-Map`): Full registry table adding full-form trigger, source file, version, and each skill's modes, using the Structured Output Architecture.
* **`/Verify`** (full form: `/Skill-Verify`): Audit only — which skills are loaded versus documented, duplicate or colliding triggers, scope overlaps, version drift between file and documentation. Emits no function prose beyond the verdict lines.

## 2. Adaptive Complexity Routing
* **Tier 1 — Five Skills or Fewer:** Plain arrow list, no headers, no table. One line each.
* **Tier 2 — Six to Fifteen Skills:** Grouped arrow list with a short group header per family, plus a compact table of `trigger | modes | source file`.
* **Tier 3 — More Than Fifteen Skills, Multiple Repos, or Any Collision Found:** Full Structured Output Architecture, including the collision matrix, the coverage-boundary section, and an explicit warning about which pairs must not be active at the same time.

## 3. Three-Layer Registry Verification Gate
1. **Layer 1 — Presence & Source of Truth:** Classify every entry before printing it, in this order of authority:
   * **`LOADED`** — the skill definition is present in the current context (pasted, uploaded, or installed in-session). Function lines may be written only for these.
   * **`DOCUMENTED`** — the skill is described by a README, manifest, or user message, but its definition is not in context. List trigger and a one-line function taken from the documentation, marked `[DOCUMENTED]`.
   * **`UNKNOWN SKILL`** — named by the user, no definition and no documentation found. Output the name and `[UNKNOWN SKILL]`; never invent what it does.
   * Never upgrade `DOCUMENTED` to `LOADED`, and never silently drop a skill you could not read — an unreadable file is a stated gap, not an omission.
2. **Layer 2 — Trigger Fidelity & Collision Detection:** For every entry:
   * Extract the invocation trigger and every mode trigger exactly as written, preserving case and leading slash.
   * Detect duplicates: the same trigger claimed by two skills, one trigger being a prefix of another (`/audit` versus `/C-audit`), or a short alias identical to another skill's full form. Report each as `[TRIGGER COLLISION: A vs B]` and name which one wins in practice (the more specific match), so the user knows what will actually fire.
   * Detect missing triggers: a skill whose Section 1 declares no invocation trigger is listed with its file name and `[NO TRIGGER]` rather than given an invented one.
3. **Layer 3 — Function Compression & Scope Overlap:** Derive each function line only from that skill's Section 0 (directive) and Section 1 (routing):
   * Compress to the single gate or output that distinguishes it: what it refuses to do, what it verifies, or what it produces.
   * Two rows may never paraphrase each other. If two functions read the same, the compression failed — rewrite them around the difference in evidence type (corpus, code, argument, number, prose, inventory).
   * Flag scope overlaps: skills whose domains intersect must carry a routing note ("use A for X, B for Y") and, where the skills themselves forbid it, the explicit rule that two split modules must not be activated in the same session.

## 4. Silent Pre-Processing (Before Printing the Registry)
1. **Inventory Scan:** Enumerate every skill definition reachable in this session — attached files, installed skill list, named directory — and count them. The count is the denominator for the completeness claim.
2. **Unreadable-File Check:** For each file that failed to load, truncated, or lacked a frontmatter block, record the path and the reason; these go into coverage boundaries, not into the registry body.
3. **Self-Entry Check:** If this registry skill is itself installed, it appears in its own list with its own trigger and function. Do not exempt it and do not duplicate it.
4. **Drift Check:** Compare each frontmatter `version` with the version stated in the documentation; report mismatches as `[VERSION DRIFT]` with both numbers.

## 5. Structured Output Architecture (Mandatory for `/Map` & `/Verify`)
1. **Scope & Source Declaration:** How many skills were found, where they were read from, and the classification counts (`LOADED` / `DOCUMENTED` / `UNKNOWN SKILL`).
2. **Registry Core:** The arrow list — the only mandatory section — one line per skill, canonical form:
   ```
   /trigger → function in one line (≤20 words)
   /trigger → function in one line | modes: /Mode-A, /Mode-B
   ```
   Grouped as: core skill first, then split-force modules in file-number order, then project-local skills. Declaration order is preserved inside each group; no alphabetical reshuffling that breaks the numbering.
3. **Trigger Table:** `trigger | full form | skill name | source file | version | modes` — one row per skill, no row merged.
4. **Collisions, Overlaps & Drift:** Every `[TRIGGER COLLISION]`, scope-overlap routing note, forbidden concurrent pair, and `[VERSION DRIFT]`, each with the exact triggers or file paths involved.
5. **Coverage Boundaries:** `[DOCUMENTED]` entries, `[UNKNOWN SKILL]` entries, unreadable files with the reason, and what would have to be supplied for those rows to become `LOADED`.

## 6. Silent Pre-Output Quality Gate
Before emitting the registry, verify internally that it satisfies ten invariants:
1. **No-Opening-Jargon:** The first line is the registry or the scope declaration — zero filler, zero "sure, here are your skills".
2. **Completeness Claimed Honestly:** The stated count matches the number of rows printed, and the scope of the scan is named.
3. **No Invented Skills:** Every row traces to a real definition or a real documentation entry; nothing is added because it "should" exist.
4. **No Invented Triggers:** Every trigger, including mode triggers, is copied exactly; no alias was created to make the list look symmetric.
5. **Presence Classified:** Every row carries its state, and `DOCUMENTED` is never presented as `LOADED`.
6. **One Line Per Skill:** No entry spans multiple paragraphs; no entry is a copy of that skill's description field verbatim.
7. **Functions Distinguishable:** No two rows say the same thing; each names the evidence type it operates on.
8. **Collisions Surfaced:** Duplicate, prefix-overlapping, or shadowed triggers are reported rather than hidden by picking one silently.
9. **Self-Included:** The registry lists itself if installed, exactly once.
10. **No Prescriptive Drift:** The registry describes what is installed; it never recommends installing something new unless the user asked for a recommendation, and it never claims a skill was executed.