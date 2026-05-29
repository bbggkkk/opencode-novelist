# Model Recommendations

This guide describes recommended model capabilities for each Novelist agent. Treat the named models as examples, not hard requirements. Model names, provider offerings, and serving quality change over time; the stable recommendation is the capability profile for each role.

Korean version: [model-recommendations.ko.md](model-recommendations.ko.md)

## General Selection Policy

Prefer role-fit over architecture labels. "Dense" and "MoE" can be useful shorthand, but providers do not always publish architecture details and runtime behavior matters more than labels.

- Writer and Editor should prefer high-quality dense or dense-like creative models. Stable prose rhythm, voice consistency, and stylistic control matter more than maximal tool use.
- Router, Otaku, Loremaster, Researcher, and Publisher should prefer large reasoning-capable models with strong long-context reliability. MoE models are acceptable when they are strong at exhaustive verification, retrieval, structured reasoning, and tool use.
- When in doubt, assign the strongest reasoning model to `novelist-otaku` and `novelist`, then choose the best prose model for `novelist-writer`.

## Example Model Set

The following example set reflects the current tested preference:

| Role Group | Example Model |
|------------|---------------|
| Creative prose and micro editing | `gemma 4 31b` |
| Routing, verification, retrieval, research, publishing | `deepseek v4 flash` |

Use this as a starting point. If local benchmarks show a different model is better at Korean prose, long-context verification, or XML/file generation, prefer the benchmark result.

## `novelist` Router

The router classifies the user's request, fixes the requested scope, manages the Seed-to-Fruit pipeline, delegates sub-agents, and enforces completion gates.

Detailed requirements:
- Strong instruction following and route selection.
- Reliable long-context reasoning across `writing-session.md`, `verification-manifest.md`, `narrative-state.md`, and user requests.
- Good judgment for halt/continue decisions, resume validation, retcon classification, and pipeline completion audits.
- Low tolerance for shortcut requests that would skip required steps.

Recommended model profile:
- Large reasoning-capable model.
- Strong tool-use and structured-output behavior.
- MoE is acceptable if long-context behavior is reliable.

Example model:
- `deepseek v4 flash`

## `novelist-writer`

The writer creates the actual fiction: scenes, narration, dialogue, emotional movement, and beat-level prose attached to the Macro Skeleton.

Detailed requirements:
- Excellent Korean prose rhythm and dialogue.
- Stable character voice and tone over long sessions.
- Strong continuation behavior from the accumulated verified prefix.
- Good creative judgment without silently changing canon or branch endpoints.
- Lower priority on external tool use than on prose quality.

Recommended model profile:
- High-quality dense or dense-like creative model.
- Medium-to-large context window.
- Higher creativity tolerance than verification agents.

Example model:
- `gemma 4 31b`

## `novelist-editor`

The editor is a micro-level prose and scene editor. It polishes style, speech style, formatting, local causality, pacing, and immediate readability.

Detailed requirements:
- Strong prose editing and stylistic control.
- Good Korean sentence rhythm, dialogue polish, and formatting discipline.
- Ability to preserve the locked prefix and editable span boundaries.
- Uses Macro Skeleton only as a local guardrail; it does not own whole-flow judgment.
- Must emit clear style, voice, and macro-guardrail notes.

Recommended model profile:
- High-quality dense or dense-like creative/editorial model.
- Similar tier to Writer, or slightly smaller if it remains excellent at style and voice.
- Does not need to be the strongest global reasoning model.

Example model:
- `gemma 4 31b`

## `novelist-otaku`

The otaku verifies setting, continuity, and macro-flow. It checks every detail against canon and performs the Branch Traversal Audit before consolidation.

Detailed requirements:
- Strong long-context reasoning and exhaustive attention to detail.
- Reliable contradiction detection across character sheets, world rules, series bible, narrative state, verified prefix, and Macro Skeleton.
- Evidence-backed verification reports.
- Strict PASS/FAIL behavior with no shortcut approvals.
- Strong enough to catch branch drift, skipped setup/payoff, wrong character knowledge, possession drift, timeline errors, and unsafe canon expansion.

Recommended model profile:
- Strongest available reasoning model.
- Excellent long-context reliability.
- MoE is acceptable if verification consistency is high.

Example model:
- `deepseek v4 flash`

## `novelist-loremaster`

The loremaster retrieves and organizes canon. It searches setting files, series bible, narrative state, and related artifacts without inventing missing facts.

Detailed requirements:
- Strong retrieval discipline and context synthesis.
- Good line/path citation behavior.
- Ability to detect missing or contradictory source material.
- Low creativity; high fidelity to source files.
- Good long-context handling for large project directories.

Recommended model profile:
- Large reasoning or retrieval-oriented model.
- Strong structured summarization and citation behavior.
- MoE is acceptable if source fidelity is strong.

Example model:
- `deepseek v4 flash`

## `novelist-researcher`

The researcher gathers real-world facts through the lens of the current story, viewpoint, style, and canon constraints.

Detailed requirements:
- Strong factual reasoning and source handling.
- Ability to filter raw facts into scene-relevant constraints.
- Good separation between "known fact", "usable in scene", and "must stay off page".
- Low tendency to overwrite canon with external trivia.

Recommended model profile:
- Reasoning-capable model with strong browsing/source synthesis when tools are available.
- Long-context reliability for matching research to canon.

Example model:
- `deepseek v4 flash`

## `novelist-publisher`

The publisher builds editable EPUB source and packages verified drafts. It should not write or revise story prose.

Detailed requirements:
- Strong structured file generation.
- Good XML/XHTML/CSS/OPF/NCX discipline.
- Reliable command-following for zip order and publication gates.
- Ability to halt when manifests, hashes, evidence, or source validation fail.

Recommended model profile:
- Reasoning-capable model with good code and structured-output behavior.
- Does not require the best creative prose model.

Example model:
- `deepseek v4 flash`

## Practical Assignment Matrix

| Agent | Primary Need | Recommended Capability Tier | Example |
|-------|--------------|-----------------------------|---------|
| `novelist` | Routing, scope, pipeline enforcement | Large reasoning / long-context | `deepseek v4 flash` |
| `novelist-writer` | Creative Korean prose | Dense or dense-like creative | `gemma 4 31b` |
| `novelist-editor` | Micro editing and style control | Dense or dense-like editorial | `gemma 4 31b` |
| `novelist-otaku` | Exhaustive canon and branch verification | Strongest reasoning / long-context | `deepseek v4 flash` |
| `novelist-loremaster` | Canon retrieval and synthesis | Reasoning / retrieval / long-context | `deepseek v4 flash` |
| `novelist-researcher` | Factual research and source synthesis | Reasoning / research-capable | `deepseek v4 flash` |
| `novelist-publisher` | EPUB source and packaging | Reasoning / structured output / code | `deepseek v4 flash` |

