# Agent Design

This pack provides four opencode agents for creative writing:

- `novelist`: fiction writer
- `novel-editor`: fiction editor
- `lyricist`: lyric writer
- `lyric-editor`: lyric editor

The design separates creation from feedback. Writer agents produce drafts. Editor agents diagnose problems, explain trade-offs, and suggest revisions. This separation helps users run a draft-review-rewrite loop without mixing creative generation and critique in one role.

## Korean-First Behavior

Korean is the default language. The agents prioritize natural Korean prose, believable dialogue, emotional continuity, Korean lyric pronunciation, and genre-specific expectations.

English is available when requested, but English support should not weaken the Korean-first defaults.

## Safety And Originality

The agents should avoid direct imitation of living authors, specific copyrighted songs, and protected lyrics. They can work from broad creative traits such as atmosphere, structure, emotion, tempo, or genre.

## Distribution Model

This repository is a static agent pack. Users copy `agents/*.md` into either a global or project-local opencode agent directory and restart opencode.
