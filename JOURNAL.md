# PathReview — Module 3 Journal

## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/147

**Issue title:** Resume section detection fails on text with leading whitespace

**Tier:** [x] Tier 1   [ ] Tier 2   [ ] Tier 3

**Problem summary:**
The resume parser is supposed to detect which sections a resume has — like Experience, Education, and Skills. Right now, detection only works if a section heading sits at the very start of a line. If there's any indentation or spaces in front of the heading, the parser misses it entirely, so an indented resume looks like it has **no sections at all**. This happens in the `_detect_sections` function in `ingestion/parsers/resume_parser.py`. It matters because real resumes are often indented or exported with formatting, so their sections get silently dropped — and everything downstream that depends on the resume's structure gets worse results.

**Selection notes (scope fit):**
I chose a Tier 1 issue because this is my first contribution to a large codebase, and the "Is this right for me?" checklist recommends starting there. Issue #147 fits well: it lives in a single file (`resume_parser.py`), the fix is localized to one function (`_detect_sections`), and there's already a test file (`tests/unit/test_resume_parser.py`) I can model new tests on. I reproduced the bug locally before committing, so I already know what "done" looks like — indented section headings should be detected the same as non-indented ones. A few hours of work is realistic for the Week 8–9 timeline.

**Branch name:** fix/147-resume-section-whitespace

**Setup confirmation:** [ ] App runs locally at localhost:5173

**Cohort ledger:** [ ] Issue added to cohort ledger
