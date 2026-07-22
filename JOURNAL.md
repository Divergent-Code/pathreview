# PathReview — Module 3 Journal

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/147

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1   [ ] Tier 2   [ ] Tier 3

**Problem summary:**
The resume parser is supposed to detect which sections a resume has — like Experience, Education, and Skills. Right now, detection only works if a section heading sits at the very start of a line. If there's any indentation or spaces in front of the heading, the parser misses it entirely, so an indented resume looks like it has **no sections at all**. This happens in the `_detect_sections` function in `ingestion/parsers/resume_parser.py`. It matters because real resumes are often indented or exported with formatting, so their sections get silently dropped — and everything downstream that depends on the resume's structure gets worse results. A successful fix would detect section headings even when they start with leading whitespace, so indented and formatted resumes are parsed with their sections intact — matching how non-indented resumes already work.

**Selection notes (scope fit):**
I chose a Tier 1 issue because this is my first contribution to a large codebase, and the "Is this right for me?" checklist recommends starting there. Issue #147 fits well: it lives in a single file (`resume_parser.py`), the fix is localized to one function (`_detect_sections`), and there's already a test file (`tests/unit/test_resume_parser.py`) I can model new tests on. I reproduced the bug locally before committing, so I already know what "done" looks like — indented section headings should be detected the same as non-indented ones. A few hours of work is realistic for the Week 8–9 timeline.

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [ ] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger

## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/Divergent-Code/pathreview/commit/b4be6f9

**Reproduction summary:**
I ran `_detect_sections` on resume text whose headings had leading spaces and tabs — it returned zero sections, while the same headings without indentation are detected. I captured this as unit tests (the indented and tab cases fail on the original code).

**PLAN.md link:** https://github.com/Divergent-Code/pathreview/blob/fix/147-resume-section-whitespace/PLAN.md

**Loom walkthrough:** N/A — the walkthrough video is optional and is not part of the Week 8 grading rubric.

**Blockers or open questions:**
Haven't run the full `pytest` suite yet — the local Python venv isn't set up. I verified the fix by running the detection regex directly; will run `pytest` once the environment is built.
