# Writing Session

## Session Identity

- Session ID: sample-volume-1-chapter-01
- Status: COMPLETED
- Operation Type: NEW_DRAFT
- Active Work Path: examples/sample-work/
- Active Volume Path: volume-1/
- Target Draft: drafts/chapter-01.md
- Started At: sample fixture
- Last Updated: sample fixture

## Recovery Contract

- Last Stable Stage: FINAL_PASS_CONSOLIDATED
- Last Completed Beat / Span: chapter-01
- Last Verified Draft SHA256: e177ff1d15e193e65745d2d239e1501a66e417e83d877245c72d7a99d21a5971
- Last Verified Canon Snapshot SHA256: f1870ca8350f392225d317f719f760b6402880a8ddc9c780ef2df621b3ce67d5
- Last Verification Manifest Row: `drafts/chapter-01.md`
- Last Verification Evidence: verification-reports/chapter-01.md
- Last Narrative State Update: Seo-yun keeps key in left coat pocket
- Last Git Commit: sample fixture
- Resume Policy: validate hashes and manifest before continuing; never trust unverified temporary text

## Current Unit

- Unit Type: CHAPTER
- Unit ID: chapter-01
- Scene / Chapter Outline Reference: series-bible.md
- Accumulated Prefix Source: drafts/chapter-01.md
- Editable Span Source: NONE
- Locked Before Context SHA256: NONE
- Locked After Context SHA256: NONE
- Temporary Work File: `.session/current-work.md`
- Current Stage: DONE
- Next Action: NONE

## Pending Verification

- Writer Output: NONE
- Initial Otaku Report: NONE
- Editor Output: NONE
- Final Otaku Verdict: PASS
- Style Drift Audit: PASS
- Character Voice Audit: PASS
- Ledger Update Pending: NONE
- Manifest Update Pending: NONE

## Resume Checklist

- [x] Confirm target draft exists or is intentionally new.
- [x] Confirm target draft hash matches Last Verified Draft SHA256, unless Last Stable Stage is NONE.
- [x] Confirm canon snapshot hash matches Last Verified Canon Snapshot SHA256, unless Last Stable Stage is NONE.
- [x] Confirm verification-manifest.md contains Last Verification Manifest Row, unless Last Stable Stage is NONE.
- [x] Confirm Last Verification Evidence exists and matches the manifest row, unless Last Stable Stage is NONE.
- [x] Confirm narrative-state.md includes Last Narrative State Update, unless Last Stable Stage is NONE.
- [x] Confirm locked context hashes before applying any revision.
- [x] Re-run verification for any temporary work before applying or consolidating it.

## Recovery Log

- Sample completed session for release validation.
