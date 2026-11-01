# Niger State: law history in git

The Laws of Niger State (Nigeria) as a git history: one file per section, one paragraph per line, so `git blame`, `git log` and `git diff` work line by line. The text is the English text of the Laws as enacted.

It follows the shared design of [lexifina/global-law](https://github.com/lexifina/global-law).

## What this repository holds

**A first build: Laws as enacted.** The Niger State Government publishes a small number of Laws as PDFs. Each Law here is one commit holding its text as enacted, dated by its commencement and credited to the Law itself. Amendments made since are not yet in this record.

| Folder | What |
| --- | --- |
| one folder per Law (e.g. `tax-administration-and-consolidation-law-2022/`) | the Law as enacted: `000-title.md`, one file per section, then any schedules |

The Laws are added in parts as each is verified. Only PDFs with a text layer are used; scanned copies (pictures of pages) are left out, as are Bills and appropriation (budget) Laws.

Known gaps in the source: The Tax Administration and Consolidation Law 2022 is here with its sections, the Regulation and Order printed within it and its First Schedule; its Second to Eighth Schedules (rates, fees and forms, several pages printed only as pictures) are not yet in this record. Its commencement (23 June 2022) is earlier than its assent and gazette (22 October 2022); it is dated by its commencement.

## Source

[Niger State Government](https://nigerstate.gov.ng/): PDFs of the Laws. Each PDF's sha256 is recorded with its version in `data/versions.json`.

## Dates

Each Law is dated by the day it came into force under its own commencement provision, at noon in Lagos time (West Africa Time, UTC+1).

## How it is built

Lexifina reads the sources listed here and records each act's dated versions, and the laws that made each change, in one corpus file. `tools/build.py` writes this repository from that file, and the same corpus always gives the same commit hashes; `REPRODUCE.md` gives the details and the checks. A model (Claude) wrote Lexifina's code; it wrote no legal text, and no model runs when the history is built.

The text layer of each PDF (no OCR) is read with the position of every line: running heads, page numbers and margin notes are set apart by their place on the page, and each section's margin note stands as the first line of its file. Lines wrapped by the printer are joined, so each paragraph is one line. Typing errors stay as printed.

## How it is checked

Every version is read back from git on the day it took effect and must match the corpus. A second, independent reading of every PDF (a different PDF engine) must contain every letter and digit of each Law in the same order, with nothing in the body left out (only page furniture and margin notes may lie between). Results are in `REPRODUCE.md`.

## What "author" means

The author of each commit is the Law that made the change, with an e-mail address that cannot exist; the committer is always Lexifina.

## Limits

Only the Laws listed above, as enacted; later amendments are not applied. The Government's PDFs are not the authoritative text; the Niger State of Nigeria Gazette is.

## Licence

See [LICENSE](LICENSE): official texts of a legislative nature are not eligible for copyright in Nigeria (Copyright Act, 2022, s. 3(b)). Source: Niger State Government.
