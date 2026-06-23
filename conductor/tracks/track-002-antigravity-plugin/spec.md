# Specification: Transforming Alete-Team into an Antigravity CLI Plugin (track-002)

## Overview
Currently, the "Alete-Team" repository is loaded as a context-based extension, utilizing the `GEMINI.md` file. However, to operate as a native **Antigravity CLI Plugin**, it should register a formal, reusable skill. This will allow any Antigravity-powered agent to discover and invoke the `alete-team` skill.

To achieve this, the repository will be restructured to follow the native Antigravity CLI plugin conventions, exposing a root `skills/` directory.

## Objectives
1.  **Expose native Alete-Team Skill**: Create [skills/alete-team/SKILL.md](file:///Users/stoyan/git/alete-team/skills/alete-team/SKILL.md) to define the `alete-team` skill instructions. This file will contain the expert system instructions, the Strategic Crucible Protocol, and the Persona Round Table mandate.
2.  **Plugin Configuration**: Verify that `plugin.json` in the project root is properly configured to register the plugin metadata.
3.  **Local Installation Automation**: Update the `extension:refresh` script in [package.json](file:///Users/stoyan/git/alete-team/package.json) to synchronize the new `skills/` directory to the user's plugin directory: `/Users/stoyan/.gemini/config/plugins/alete-team/`.
4.  **Verification**: Verify that the skill is successfully copied, detected, and can be resolved by the agent.

## Technical Structure & Plugin Conventions
A native Antigravity plugin consists of:
- **`plugin.json`**: Located at the plugin root directory. Declares the plugin metadata.
  ```json
  {
    "name": "alete-team"
  }
  ```
- **`skills/<skillName>/SKILL.md`**: Defines a skill. The skill file starts with a YAML frontmatter:
  ```yaml
  ---
  name: alete-team
  description: "Runs the Strategic Crucible debate with expert personas (Julian, Maya, Serra, Aris, Lyra) and facilitates a Persona Round Table to evaluate Time To Value (TTV) for target personas."
  ---
  ```
  Followed by detailed markdown instructions for the AI on how to perform the skill.

- **Sync Script**: In [package.json](file:///Users/stoyan/git/alete-team/package.json), the refresh script needs to copy the repo files (especially `plugin.json`, `GEMINI.md`, `skills/` directory) to the active plugins directory `/Users/stoyan/.gemini/config/plugins/alete-team/`.

## Detailed File Modifications

### 1. `skills/alete-team/SKILL.md`
This new file will contain:
- YAML Frontmatter defining `name: alete-team` and a clear description.
- System directives for the 5 experts (Julian, Maya, Serra, Aris, Lyra).
- The three stages of the **Strategic Crucible Protocol** (Signal, Selection, Synthesis).
- The **Persona Round Table** mandate (evaluating TTV scores for Marcus, Elena, and David).

### 2. `package.json`
Update the `extension:refresh` script to synchronize the files.
Because it needs to update the plugin folder under `/Users/stoyan/.gemini/config/plugins/alete-team/`, we can add a script command like:
```json
"scripts": {
  "extension:refresh": "gemini extensions uninstall alete-team && gemini extensions install . && mkdir -p /Users/stoyan/.gemini/config/plugins/alete-team/skills && cp -r skills/ /Users/stoyan/.gemini/config/plugins/alete-team/skills/"
}
```
*(Wait, let's verify if `gemini extensions install` already copies the skills folder. If it does, we can verify it. If it doesn't, we can explicitly copy it).*

## Verification & Testing
We will test by running:
1. `pnpm run extension:refresh`
2. Verifying that `/Users/stoyan/.gemini/config/plugins/alete-team/skills/alete-team/SKILL.md` exists and contains the correct contents.
3. Checking if the `alete-team` skill appears in the list of available skills for the agent.
