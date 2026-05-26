# Flimp Timeline Generator

Internal scoping tool that translates a project due date plus selected deliverables into a recommended Production Start Date and pre-production window. Built for Flimp account managers to scope client projects without negotiating math live with clients.

**Live:** https://timeline-scoping-tool.vercel.app

## What this repo is

A single static `index.html`. No build step, no dependencies. Vercel serves the file directly.

## How to update

1. Edit `index.html` on a branch or directly on `main`.
2. Push. Vercel auto-deploys.
3. Verify on the live URL.

## When something breaks

If a change breaks the tool:

1. **Revert the commit** (`git revert <sha>`) and push. Vercel redeploys the previous good version.
2. Or revert in the Vercel dashboard: each deploy is preserved and can be promoted with one click.

## Critical math model (Phase 21, locked 2026-05-26)

- **Pre-production window:** 10 business days minimum, BEFORE catalog timeline starts. Universal across all 34 products.
- **Catalog BD** for products ≥ 10 BD: Active production + Final Client QA & QC (1 BD) + Approval (1 BD).
- **Catalog BD** for products < 10 BD: single "Production" phase.
- **Translation:** 5 BD universal (new and renewal).
- **Print & Mail:** 10 BD rollback from in-hand.
- **Alternate development:** 10 BD sequential AFTER main production.
- **Within a deliverable:** main translation → alt translation (single translator); main print → alt print (single printer).
- **Across deliverables:** parallel.
- **Multi-deliverable:** one shared pre-production window; longest deliverable drives Production Start Date.

## Full context

- **Notion (decisions log + phase history):** https://www.notion.so/36b9eb932fd88156955fcd5c608b5276
- **Catalog reference (xlsx, every product + every CONFIG value + 8 test scenarios with real dates):** `flimp-catalog-reference-phase21.xlsx` (not committed; lives in Ashleigh's Notion-attached files)
- **Source pricing PDF:** `BGFirst_Flimp2026Pricing_04_09_2026.pdf` (not committed)
- **Master scoping workbook (Gage's reference):** `MASTER_2026_Flimp_Project_Timeline__DRAFT_04.16.26.xlsx` (not committed)

## Verification before pushing changes

Before pushing, run the tool's `runCalculation` against at least one single-deliverable and one multi-deliverable scenario. Confirm:

- `</html>` is the last meaningful content (no trailing nulls, no truncation)
- No `ReferenceError` thrown when multi-deliverable is rendered
- `CONFIG.pre_production_window_bd === 10`
- Headline renders "Production Start Date" as the dominant title

The Phase 21 working file was validated with both single and multi-deliverable runtime tests before being committed as the initial state of this repo.
