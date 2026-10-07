# UNIFA Tuition Reconciler

Matches the deposits on a Unibank statement to UNIFA students, even when the student ID or name in the bank memo is misspelled.

Built for the finance staff at UNIFA (Université de la Fondation Dr Aristide, Haiti). Students pay tuition in cash at a bank branch and write their ID and name by hand. The tool reads the statement, finds the right student for each line, and sorts the lines into four groups: Auto-matched, Check name, Needs review, No name in memo.

## Try it

1. Open the live site.
2. Step 1: upload `sample-data/sample-roster-FAKE.xlsx`.
3. Step 2: upload `sample-data/sample-unibank-statement-FAKE.xlsx`.
4. Click **Match payments**.

Expected result with the sample files: 12 lines read, 5 Auto-matched, 5 Check name, 1 Needs review, 1 No name.

## Privacy

Everything runs in the browser. Files are read on the page and never uploaded. There is no server, no database and no API key.

The sample files contain invented students and invented payments. Never commit real statements or rosters to this repository. The `.gitignore` blocks spreadsheets outside `sample-data/`.

## How it works

- One file, `index.html`. SheetJS is bundled inline to read Excel files.
- IDs are normalised first (`fsi269011` becomes `FSI-26-9011`).
- Damerau-Levenshtein distance catches typos and swapped letters (`FSPJ` for `FSJP`).
- A rival check flags a payment when the written name fits a different student better than the owner of the written ID.

Code © LOU
