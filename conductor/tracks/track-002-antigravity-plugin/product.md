# Product Definition & Strategic Crucible Debate (track-002)

## 1. Kickoff Prompt (User Input)
> "Look up Antigravity CLI plugins and figure out what changes we need to add to our current repo to make this alete team repo a Antigravity plugin, and then create a Conductor track out of it."

---

## 2. The Strategic Crucible: Persona Round Table

### Stage 1: The Initial Sound Off (The Signal)
*   **Julian (Vision - Focuses on Elena / The Alpha-Curator):** 
    "Transforming `alete-team` from a simple context extension to a native Antigravity CLI plugin gives us high-status presence in the CLI's toolchain. By exposing an explicit `alete-team` skill, developers and users can trigger the Strategic Crucible directly inside any project context. The TTV for Elena (The Alpha-Curator) will be immediate: she gets structural, high-signal curation features directly on any workspace. This is perspective ownership made modular."
*   **Maya (Product Operations - Focuses on Marcus / The Optimizer):** 
    "From an operational perspective, modularity reduces cognitive overhead and token waste. Defining the skill in a clean `skills/alete-team/SKILL.md` format means the agent will only load the squad's protocol when explicitly needed or when executing planning steps. For Marcus (The Optimizer), this translates to an efficient, low-token-cost feed that doesn't bloat daily operation runtimes."
*   **Serra (System Infrastructure - Focuses on Marcus / The Optimizer):** 
    "To support this, we must introduce a standard plugin structure in the repo. This requires a root `skills/` folder containing the skill definition, and an update to the sync-install scripts in `package.json`. When `extension:refresh` runs, it must ensure the `skills/` directory is copied over to `/Users/stoyan/.gemini/config/plugins/alete-team/skills/`. This guarantees local execution stability and keeps the system clean."
*   **Aris (Sensory UI/UX - Focuses on David / The Digital Ascetic):** 
    "The skill representation in `SKILL.md` must be extremely clean. Zero boilerplate, highly legible markdown sections, and clear triggers. David (The Digital Ascetic) needs a distraction-free output where the Crucible's debates are visually separated from system execution logs, maintaining 'Atmospheric Clarity' and peace of mind."
*   **Lyra (Narrative Specialist - Focuses on Elena / The Alpha-Curator):** 
    "The narrative arc here is the evolution of Alete-Team from an 'ambient suggestion' into an 'explicit agent tool'. The setup instructions must be packaged in a 3-act format that guides the user: first showing the setup status quo (the hook), then guiding them through the integration crucible (the friction), and returning to a fully integrated cognitive workflow (the resolution)."

### Stage 2: The Cross-Critique (Selection Pressure)
*   **Serra critiques Julian:** 
    "Julian focuses heavily on the vision of the plugin. However, if the CLI's plugin loader expects a certain format in `plugin.json` or expects the `skills` files to be formatted exactly with YAML frontmatter headers (e.g. `--- name: alete-team ... ---`), the CLI will error out. We need to ensure syntax correctness over rhetorical flourish."
*   **Aris critiques Maya:** 
    "Maya wants to minimize token cost by stripping too much. We must not sacrifice the distinct voice and tone of the five specialists (Julian, Maya, Serra, Aris, Lyra). If we compress the system prompt too much, the Crucible loses its metabolic tension and reverts to generic LLM agreement. The output formatting needs clear visual delineation."
*   **Julian critiques Lyra:** 
    "Lyra's narrative must not make the installation instructions verbose. Startups and founders value speed. Keep the onboarding instructions short and scannable for Elena."

### Stage 3: The Nash Equilibrium (Synthesis)
We will proceed with transforming the repository structure.
*   **Structure Changes Needed**:
    1. Define a `skills/alete-team/SKILL.md` file with the standard Antigravity YAML frontmatter and containing the complete system instructions for activating the Alete-Team.
    2. Ensure `plugin.json` correctly registers `alete-team`.
    3. Update the update/sync scripts in [package.json](file:///Users/stoyan/git/alete-team/package.json) to install the skills properly into the local `.gemini` directory.
    4. Implement verification test cases to assert that the skill files are valid.

---

## 3. Design Decision: Skill vs. Agent Representation

### Kickoff Prompt
> "Should we have this repository of multiple people inside a cross-functional team as a skill, or should we make it into agents?"

### Stage 1: The Initial Sound Off
*   **Julian (Vision - Focuses on Elena / The Alpha-Curator):** 
    "If we implement Julian, Maya, Serra, Aris, and Lyra as five individual, independent **Agents** in the plugin, they can debate asynchronously, spawning distinct subagents with separate context history. This feels like a true 'Society of Minds'. Elena (The Alpha-Curator) gets a highly authentic, multi-perspective strategic audit."
*   **Maya (Product Operations - Focuses on Marcus / The Optimizer):** 
    "Running 5 distinct agents in parallel for every planning task is operational madness. The token cost would increase 5-fold, and the latency of waiting for five separate LLM calls to complete sequentially or concurrently would destroy usability. Marcus (The Optimizer) will find this too slow and expensive. A **Skill** compiles the entire team's debate logic into a single system instruction set that executes in a single LLM turn. This is fast, lean, and cost-efficient."
*   **Serra (System Infrastructure - Focuses on Marcus / The Optimizer):** 
    "From an infrastructure perspective, maintaining 5 separate agents requires complex orchestration and synchronizing state across multiple sub-conversations. A Skill is structurally resilient, requires zero orchestration overhead, and runs deterministically inside the parent agent's context. However, we could expose a single **Agent Profile** (`alete-team` agent) that loads the `alete-team` skill, providing a clean delegation interface."
*   **Aris (Sensory UI/UX - Focuses on David / The Digital Ascetic):** 
    "Spawning 5 agents will flood the CLI terminal with verbose lifecycle messages, hook runs, and connection logs. This is highly disruptive for David (The Digital Ascetic). A single agent evaluating the Alete-Team skill outputs a clean, unified, structured debate in a single response, which is visually elegant and quiet."
*   **Lyra (Narrative Specialist - Focuses on Elena / The Alpha-Curator):** 
    "A single response allows us to structure the debate as a 3-act narrative with a definitive synthesis. If it's split across five individual agents, the message gets fragmented into chat coordination chatter. A single, synthesized output delivers the 'Bow & Arrow' message with high clarity."

### Stage 2: The Cross-Critique
*   **Julian critiques Maya & Serra:** 
    "A single-agent simulation can suffer from 'model homogenization' where the LLM struggles to keep the personas truly distinct and instead drifts toward quick consensus. Separate agents enforce a harder selection pressure."
*   **Serra critiques Julian:** 
    "Homogenization can be solved by strong system instruction prompt engineering inside the skill. The infrastructure overhead and token-cost of 5 separate agents is a fatal blocker for normal usage."

### Stage 3: The Nash Equilibrium (Synthesis - The Hybrid Approach)
The optimal strategy is a **Hybrid Model**:
1.  **Expose the Core as a Skill (`skills/alete-team/SKILL.md`)**: This keeps the debate framework lightweight, modular, and loadable by any agent in any workspace.
2.  **Define a Single Coordinator Agent (`agents/alete-team.json`)**: (Future Phase) Expose a single agent profile called `alete-team` that is pre-loaded with the `alete-team` skill.
This gives us the best of both worlds:
*   Users can load the skill directly in their current session for maximum speed and zero token overhead.
*   Users can spawn the `alete-team` agent as a single subagent whenever they want an isolated, dedicated strategic audit, without the 5-fold overhead of spawning 5 individual agents.

---

## 4. Persona Time to Value (TTV) Scores (Hybrid Model)

### 1. Elena (The Alpha-Curator)
*   **TTV Score:** **9 / 10**
*   **Commitment:** Immediate access to the `alete-team` squad as a first-class capability. She can trigger the Strategic Crucible directly from her terminal or agent workflow.

### 2. Marcus (The Optimizer)
*   **TTV Score:** **9 / 10**
*   **Commitment:** Optimal computational efficiency. Using a single skill-loaded agent instead of 5 separate subagents keeps the token count and latency minimal.

### 3. David (The Digital Ascetic)
*   **TTV Score:** **9 / 10**
*   **Commitment:** Clean, noise-free separation. The team's debates are modularized and only trigger when strategic decisions are requested, shielding the user from unnecessary ambient noise.
