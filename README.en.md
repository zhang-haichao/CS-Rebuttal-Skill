# CS Rebuttal Skill

[中文](README.md) · [Skill instructions](skills/draft-cs-rebuttal/SKILL.md) · [MIT License](LICENSE)

Turn computer science conference reviews into **response strategies in Chinese, evidence-grounded rebuttal drafts in English, and concrete experiment and manuscript revision suggestions**.

The skill supports individual comments and complete review sets. It helps authors identify the technical concern behind a comment, choose evidence that addresses it, and write a direct, professional response.

## Install

With Node.js 22.20 or later, use the [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal
```

Follow the prompts to select your agent. Installation is project-scoped by default; add `-g` for a personal installation across projects:

```bash
# Codex
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal -a codex -g

# Claude Code
npx skills add zhang-haichao/CS-Rebuttal-Skill --skill draft-cs-rebuttal -a claude-code -g
```

The package contains Markdown instructions and references. There is no server to run or separate API setup. Model access, browsing, and file handling come from the agent you use.

## Capabilities

| Task | Approach |
|---|---|
| Diagnose reviews | Split compound comments into answerable questions; distinguish explicit concerns from inferred ones |
| Address novelty | Compare verified prior work, explain meaningful differences, and connect them to evidence |
| Correct misunderstandings | Explain the relevant mechanism and point to verified manuscript locations |
| Answer experimental concerns | Check model capacity, budget, splits, baselines, ablations, and reliability |
| Plan experiments | Prioritize the smallest useful controls within the available time and resources |
| Integrate results | Check what positive, negative, or mixed findings actually support |
| Edit and audit drafts | Check directness, tone, consistency, completion status, and length |

Eight reference patterns cover capacity confounds, factual misunderstandings, novelty, protocols and baselines, small gains, generalization and robustness, scope and limitations, and ambiguous or inconsistent reviews.

## Default output

1. **Strategy in Chinese:** the concern, an appropriate position, useful evidence, and any important uncertainty.
2. **Response in English:** a concise answer with comment IDs, supporting evidence, and completed or confirmed revision actions.
3. **Required follow-up:** missing evidence, targeted experiments, and manuscript changes.

Ask for another language, English only, LaTeX formatting, or a specific length whenever needed. With incomplete evidence, the skill drafts supported portions and marks gaps such as `[matched-parameter results needed]`. It does not fabricate results or present proposed work as completed.

## Usage

Invoke `$draft-cs-rebuttal` in Codex, or `/draft-cs-rebuttal` in Claude Code. Other compatible tools may expose the skill through their own selector.

```text
Use $draft-cs-rebuttal to analyze this comment in Chinese and draft
a response in English.

Review:
"It is unclear whether the improvement comes from the proposed module
or the larger model size."

Relevant manuscript content: [paste text or attach the paper]
Completed evidence and settings: [provide results, or state none]
Confirmed manuscript changes: [if any]
Constraints: [word limit, deadline, available compute]
```

For a full rebuttal, provide the abstract, reviews and score meanings, relevant manuscript, completed experiments, and any known constraints. One comment is enough to start; filling every field is optional.

To audit an existing draft:

```text
Use $draft-cs-rebuttal to check this rebuttal against the reviews and paper.
Identify substantive problems, provide replacement text, and keep the
English response within 500 words.
```

## Manual installation

Clone the repository:

```bash
git clone https://github.com/zhang-haichao/CS-Rebuttal-Skill.git
```

On macOS/Linux, run one of the following from the directory containing the clone. The destination skill directory should not already exist:

```bash
# Codex: personal scope
mkdir -p ~/.agents/skills
cp -R CS-Rebuttal-Skill/skills/draft-cs-rebuttal ~/.agents/skills/
```

```bash
# Claude Code: personal scope
mkdir -p ~/.claude/skills
cp -R CS-Rebuttal-Skill/skills/draft-cs-rebuttal ~/.claude/skills/
```

For project scope, copy the complete skill folder into `.agents/skills/` for Codex or `.claude/skills/` for Claude Code. On Windows, you can also copy the folder with a file manager. See the [OpenAI documentation](https://learn.chatgpt.com/docs/build-skills) and [Claude Code documentation](https://code.claude.com/docs/en/skills) for platform-specific discovery behavior.

### ChatGPT environments with custom skills

If your environment provides `@skill-creator`, ask it to install the skill from:

```text
https://github.com/zhang-haichao/CS-Rebuttal-Skill/tree/main/skills/draft-cs-rebuttal
```

You can also download the repository and provide the `skills/draft-cs-rebuttal` folder to the skill creation tool. Availability depends on your account and client; a local CLI installation does not install the skill into a cloud ChatGPT account.

## Files

| File | Purpose |
|---|---|
| `skills/draft-cs-rebuttal/SKILL.md` | Triggers, workflow, output, and final checks |
| `skills/draft-cs-rebuttal/references/response-patterns.md` | Common concerns and response patterns |
| `skills/draft-cs-rebuttal/references/evidence-and-experiments.md` | Evidence checks and targeted experiment planning |
| `skills/draft-cs-rebuttal/agents/openai.yaml` | Display metadata and a default prompt for supporting tools |

## Principles

Stay professional while maintaining a clear position. Prioritize correctness and decision-relevant evidence. Keep claims, numbers, and completion status traceable. Acknowledge actual limitations without adding unnecessary self-criticism. Never hide negative findings that affect the main claim.

Authors should verify the final facts and applicable venue requirements. The skill does not guarantee a score increase or acceptance.

## Acknowledgments and license

The workflow is based primarily on the author's experience responding to computer science conference reviews. It also draws inspiration from [TobiasLee/Rebuttal-Skill](https://github.com/TobiasLee/Rebuttal-Skill) in concern decomposition, experiment prioritization, and evidence checks. Instructions and examples were independently organized for the default Chinese-strategy/English-response workflow.

Released under the [MIT License](LICENSE). Issues and pull requests with anonymized concern types, improvements, and documentation corrections are welcome.
