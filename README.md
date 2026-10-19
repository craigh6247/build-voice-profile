# Build a voice profile

A reusable agent skill for interviewing someone and building an evidence-based guide to their writing voice. Install it as a portable Agent Plugin or as a standalone skill with Vercel's Skills CLI.

It asks concrete questions one at a time, samples personal and work situations where relevant, shows a provisional profile, and calibrates it through sample drafts and corrections. If requested, it can package the result as a separate person-specific writing skill using the available skill-creator workflow.

## Private repository access

This repository is private. You need an account with access and working Git/GitHub authentication. The plugin routes below use an authenticated local clone:

```sh
gh repo clone craigh6247/build-voice-profile
```

If a checkout or installed skill already exists, review it before replacing or updating it. Keep the clone outside your agent's skills directory: this repository now packages its canonical skill under `skills/build-voice-profile/`.

## Option 1: Agent Plugin

The repository root is an [Agent Plugins 1.0 package](https://agent-plugins.org/plugin-authors/build-an-agent-plugin), with a root [plugin.json](plugin.json) and one skill under `skills/`. Installation and enablement belong to each client; the standard does not define a universal installation command. Use a client that supports the skills component in the [compatible-client directory](https://agent-plugins.org/compatible-clients).

### VS Code with GitHub Copilot

After cloning, merge this into your VS Code user `settings.json`, replacing the example path with the absolute path to your checkout:

```json
{
  "chat.plugins.enabled": true,
  "chat.pluginLocations": {
    "/absolute/path/to/build-voice-profile": true
  }
}
```

Open **Chat: Configure Skills** to check that the plugin's skill is available. These are VS Code's [documented local-plugin settings](https://code.visualstudio.com/docs/agent-customization/agent-plugins#use-local-plugins); preserve your other settings and plugin locations.

### Cursor local plugin

Clone directly into Cursor's local plugin directory instead of making the general clone above:

```sh
gh repo clone craigh6247/build-voice-profile ~/.cursor/plugins/local/build-voice-profile
```

Restart Cursor or run **Developer: Reload Window**, then open **Customize** to check the skill. Local plugin imports must be allowed by your organisation, and an installed marketplace plugin with the same name takes precedence. See Cursor's [local-plugin instructions](https://cursor.com/docs/plugins#test-plugins-locally). No marketplace publication is required for this route.

## Option 2: Vercel Skills CLI

With Node.js/npm available, list the repository's skills without installing:

```sh
npx skills@latest add craigh6247/build-voice-profile --list
```

Install only this skill for Codex at user scope:

```sh
npx skills@latest add craigh6247/build-voice-profile --skill build-voice-profile --agent codex --global
```

Omit `--global` for project scope, or choose another supported `--agent`. This installs the skill, rather than registering the whole plugin. See the official [Skills CLI documentation](https://www.skills.sh/docs/cli) and [source/option reference](https://github.com/vercel-labs/skills#install-a-skill).

Private sources require working authentication for the source URL. If shorthand/HTTPS discovery fails, use the authenticated clone above and install from its local path:

```sh
cd build-voice-profile
npx skills@latest add . --list
npx skills@latest add . --skill build-voice-profile --agent codex --global
```

GitHub CLI authentication and Git credentials can differ; successful `gh` access alone does not prove every CLI version's HTTPS flow works. See Vercel's [private-repository guidance](https://github.com/vercel-labs/skills#private-repositories). No new access token is required for the local-clone route. To disable CLI telemetry, prefix commands with `DISABLE_TELEMETRY=1` as described in the [official telemetry documentation](https://www.skills.sh/docs/cli#telemetry).

## Use

```text
Use the build-voice-profile skill to interview me one question at a time and build a practical profile of my writing voice.
```

In Codex CLI or the IDE extension, explicitly invoke it with `$build-voice-profile`, following the [official OpenAI documentation](https://learn.chatgpt.com/docs/build-skills#how-chatgpt-and-codex-use-skills). Other clients may provide their own skill picker or slash command. You can provide existing writing samples or a previous profile, specify the intended audience, or request a fixed number of questions. Voice transcripts and typed answers both work; the skill profiles writing, not acoustic characteristics.

For professional writing, ask for an extension focused on your customer or VC/investor communications:

```text
Use the build-voice-profile skill to extend my profile for customer and investor writing. Build on the samples we already have, and ask one concrete question at a time.
```

The optional professional modules offer seven customer and five investor prompts covering value, commercial conversations, follow-ups, boundaries, difficult updates, evidence, introductions, traction, ambition and funding. Select the useful situations rather than completing a fixed questionnaire, then calibrate short drafts for the intended audiences.

## Contents

- [plugin.json](plugin.json): portable manifest, validated against the [official schema](https://agent-plugins.org/schemas/1.0.0/plugin.schema.json).
- [skills/build-voice-profile/SKILL.md](skills/build-voice-profile/SKILL.md): interview, profiling, calibration and optional packaging workflow.
- [Interview prompts](skills/build-voice-profile/references/interview-prompts.md): adaptable questions, follow-ups and calibration prompts.
- [Professional writing](skills/build-voice-profile/references/professional-writing.md): optional customer and investor modules, draft calibration and evidence limits.
- [agents/openai.yaml](skills/build-voice-profile/agents/openai.yaml): Codex display metadata and starter prompt.

The manifest schema, skill metadata and relative links have been checked. Vercel Skills CLI 1.7.2 discovered the skill using local and authenticated GitHub `--list` checks. Those checks do not verify installation or loading in a live agent client.

This repository contains the generic method only. It does not include personal interview transcripts, voice anchors or a person-specific writing profile. Creating a profile does not authorise publishing it or sending messages on someone's behalf.
