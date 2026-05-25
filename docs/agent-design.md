# Agent Design

## Architecture

This pack uses a **hierarchical agent architecture** with two router agents at the top level, each managing specialized sub-agents.

```
소설가 (Novelist Router) — feedback loop orchestrator
├── 소설가-작성가 — fiction writing (scenes, dialogue, plot, narration)
├── 소설가-편집자 — fiction editing (plot, character, prose, pacing)
├── 소설가-연구자 — research & LaTeX paper writing
├── 소설가-설정지킴이 — setting archivist (context retrieval from files)
└── 소설가-오타쿠 — setting verifier (consistency checking)

작사가 (Lyricist Router)
├── 작사가-작성가 — lyric writing (K-pop, ballad, hip-hop, indie, OST)
└── 작사가-편집자 — lyric editing (hook, rhyme, flow, pronunciation)
```

## Feedback Loop

The 소설가 router runs a **structured feedback loop** for all writing requests. Every draft passes through verification before delivery.

```
 ① 설정지킴이 → searches project files, compiles setting document
        │
 ② 작성가 → writes draft based on setting document
        │
 ③ 오타쿠 → cross-examines draft against setting
       ╱ ╲
    PASS  FAIL
      │      │
      │   ④ 편집자 → fixes every flagged inconsistency
      │      │
      │   ⑤ → ③ re-verify (loop until PASS)
      ▼
  ⑥ final result delivered to user
```

The same agents can also be invoked directly:

| Command | What happens |
|---------|-------------|
| `/소설가 3화를 써줘` | Full feedback loop (①→②→③→④↺→⑥) |
| `/소설가-설정지킴이 주인공 설정 정리해줘` | Setting document only |
| `/소설가-오타쿠 이 초안 검증해줘` | Verification only |
| `/소설가-오타쿠 PASS` | Verification passed |
| `/소설가-오타쿠 FAIL + 리포트` | Needs revision |

## Router Design

Each router agent analyzes the user's natural language request and **delegates** to the appropriate sub-agent via opencode's `@agent-name` syntax:

| Router | Input Signal | Routes To |
|--------|-------------|-----------|
| `소설가` | create, write, draft, scene, chapter | Full feedback loop → 설정지킴이 → 작성가 → 오타쿠 → 편집자 → 오타쿠 |
| `소설가` | fix, review, feedback, revise, edit | `@소설가-편집자` → `@소설가-오타쿠` |
| `소설가` | paper, latex, experiment, research | `@소설가-연구자` |
| `소설가` | setting, context, 찾아줘 | `@소설가-설정지킴이` |
| `소설가` | verify, check, 검증 | `@소설가-오타쿠` |
| `작사가` | create, write, draft, verse, chorus, lyric | `@작사가-작성가` |
| `작사가` | fix, review, feedback, revise, polish | `@작사가-편집자` |

Routers never attempt to perform the work themselves — they evaluate the request and hand off a complete brief to the sub-agent.

## Separation of Concerns

The design separates creation from feedback at every level:

- **Writer agents** (`소설가-작성가`, `작사가-작성가`) produce drafts with high temperature (0.8)
- **Editor agents** (`소설가-편집자`, `작사가-편집자`) diagnose problems with low temperature (0.4–0.45)
- **Research agent** (`소설가-연구자`) combines analysis and writing with low temperature (0.3)
- **Setting agents** (`소설가-설정지킴이`, `소설가-오타쿠`) provide factual grounding with low temperature (0.2)
- **Router agents** (`소설가`, `작사가`) classify and delegate with low temperature (0.3)

The **설정지킴이 → 작성가 → 오타쿠 → 편집자 → 오타쿠** feedback loop ensures that every draft is:
1. Grounded in established setting (설정지킴이)
2. Creatively written (작성가)  
3. Rigorously verified (오타쿠)
4. Corrected if needed (편집자)
5. Re-verified until clean (오타쿠 재검증)

This separation helps users run a draft-review-rewrite loop without mixing creative generation and critique in a single role.

## Korean-First Behavior

Korean is the default language. All agents prioritize natural Korean prose, believable dialogue, emotional continuity, Korean lyric pronunciation, and genre-specific expectations.

English is available when requested, but English support should not weaken the Korean-first defaults. The `소설가-연구자` agent supports bilingual LaTeX paper writing in both Korean and English.

## Safety And Originality

The agents should avoid direct imitation of living authors, specific copyrighted songs, and protected lyrics. They can work from broad creative traits such as atmosphere, structure, emotion, tempo, or genre.

## Distribution Model

Users install agents via the interactive `install.sh` script:

```bash
git clone https://github.com/bbggkkk/opencode-agent-pack.git
cd opencode-agent-pack
./install.sh
```

The script accepts an optional argument for non-interactive use:

```bash
curl -sSL https://raw.githubusercontent.com/bbggkkk/opencode-agent-pack/master/install.sh | sh -s -- 1
curl -sSL https://raw.githubusercontent.com/bbggkkk/opencode-agent-pack/master/install.sh | sh -s -- 2
```

- `1` → project-local install (`.opencode/agents/`)
- `2` → global install (`~/.config/opencode/agents/`)

Manual copy is also supported:

```bash
cp agents/*.md ~/.config/opencode/agents/
```

After installation, restart opencode for changes to take effect.
