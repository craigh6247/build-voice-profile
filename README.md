# Build a voice profile

A reusable Codex skill for interviewing someone and building an evidence-based guide to their writing voice.

It asks concrete questions one at a time, samples personal and work situations where relevant, shows a provisional profile, and calibrates it through sample drafts and corrections. If requested, it can package the result as a separate person-specific writing skill using the available skill-creator workflow.

## Install

With GitHub CLI authenticated to an account that can access this private repository, clone it into your Codex skills directory:

```sh
gh repo clone craigh6247/build-voice-profile "${CODEX_HOME:-$HOME/.codex}/skills/build-voice-profile"
```

If that folder already exists, review it before replacing or updating it. Start a new Codex chat after installation so the skill can be discovered.

## Use

```text
Use $build-voice-profile to interview me one question at a time and build a practical profile of my writing voice.
```

You can provide existing writing samples or a previous profile, specify the intended audience, or request a fixed number of questions. Voice transcripts and typed answers both work; the skill profiles writing, not acoustic characteristics.

## Contents

- [SKILL.md](SKILL.md): interview, profiling, calibration and optional packaging workflow.
- [references/interview-prompts.md](references/interview-prompts.md): adaptable questions, follow-ups and calibration prompts.
- [agents/openai.yaml](agents/openai.yaml): Codex display metadata and starter prompt.

This repository contains the generic method only. It does not include personal interview transcripts, voice anchors or a person-specific writing profile. Creating a profile does not authorise publishing it or sending messages on someone's behalf.
