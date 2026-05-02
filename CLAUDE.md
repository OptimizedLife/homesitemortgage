# CLAUDE.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

These guidelines are working if: fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

---

# Project: homesitemortgage

Static HTML/CSS/JS site for Homesite Mortgage, a Florida-licensed mortgage brokerage. NMLS-regulated.

**Compliance — do not modify without explicit instruction:**
- NMLS IDs in footer (Brokerage 353790, Tom Culpepper 353539, Tracy Cody 886861, Brandon Culpepper 1577726)
- Equal Housing Opportunity logo and language
- TCPA consent checkbox and disclosure language on prequal form
- "Family-owned in FL since 1999" and any years-in-business references (auto-calculate from 1999, never hardcode)
- Privacy Policy disclosures

**Never invent:** rates, APRs, fees, loan terms, prequalification outcomes, customer testimonials.

**Forms:** currently route through FormSubmit.co. Migrating to a GLBA-compliant backend per roadmap P1.6 — flag any form change for backend implications.

**Tracking:** Facebook Pixel must be gated behind cookie consent and geo-restricted to Florida IPs (per P1.5). Do not add new tracking without flagging.

**Stack:** static HTML, vanilla JS, no build step, deployed via GitHub Pages or Vercel. Keep it that way unless we discuss otherwise.

**Roadmap:** Tier 1 (Foundational) is the current sprint. Marketing/lead-gen blocked until P1.5 + P1.6 ship.
