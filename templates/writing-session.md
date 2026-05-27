# Writing Session

## Session Identity

- Session ID: TBD
- Status: IDLE
- Operation Type: TBD
- Active Work Path: TBD
- Active Volume Path: TBD
- Target Draft: TBD
- Started At: TBD
- Last Updated: TBD

## Recovery Contract

- Last Stable Stage: NONE
- Last Completed Beat / Span: NONE
- Last Verified Draft SHA256: NONE
- Last Verified Canon Snapshot SHA256: NONE
- Last Verification Manifest Row: NONE
- Last Verification Evidence: NONE
- Last Narrative State Update: NONE
- Last Git Commit: NONE
- Resume Policy: validate hashes and manifest before continuing; never trust unverified temporary text

## Current Unit

- Unit Type: TBD
- Unit ID: TBD
- Scene / Chapter Outline Reference: TBD
- Accumulated Prefix Source: TBD
- Editable Span Source: TBD
- Locked Before Context SHA256: NONE
- Locked After Context SHA256: NONE
- Temporary Work File: `.session/current-work.md`
- Current Stage: IDLE
- Next Action: TBD

## Pending Verification

- Writer Output: NONE
- Initial Otaku Report: NONE
- Editor Output: NONE
- Final Otaku Verdict: NONE
- Style Drift Audit: NONE
- Character Voice Audit: NONE
- Ledger Update Pending: NONE
- Manifest Update Pending: NONE

## Resume Checklist

- [ ] Confirm target draft exists or is intentionally new.
- [ ] Confirm target draft hash matches Last Verified Draft SHA256, unless Last Stable Stage is NONE.
- [ ] Confirm canon snapshot hash matches Last Verified Canon Snapshot SHA256, unless Last Stable Stage is NONE.
- [ ] Confirm verification-manifest.md contains Last Verification Manifest Row, unless Last Stable Stage is NONE.
- [ ] Confirm Last Verification Evidence exists and matches the manifest row, unless Last Stable Stage is NONE.
- [ ] Confirm narrative-state.md includes Last Narrative State Update, unless Last Stable Stage is NONE.
- [ ] Confirm locked context hashes before applying any revision.
- [ ] Re-run verification for any temporary work before applying or consolidating it.

## Recovery Log

- TBD
