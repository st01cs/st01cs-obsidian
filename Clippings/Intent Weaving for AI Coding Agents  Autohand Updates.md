---
title: "Intent Weaving for AI Coding Agents | Autohand Updates"
source: "https://www.autohand.ai/updates/intent-weaving"
author:
published: 2025-10-10
created: 2025-10-10
description: "How Autohand turns strategy, policy, and telemetry into machine-executable intent so AI coding agents deliver safely and on mission."
tags:
  - "clippings"
---
Autonomy only compounds value when it expresses the strategy of the organisation that deploys it. Otherwise, agents become detached freelancers closing Jira tickets for their own amusement. Intent weaving is our discipline for preventing that drift. It is the set of patterns we use to capture strategy, encode governance, and guide Autohand’s Level 4 agents so that every autonomous action can be traced back to a business mandate.

Unlike classical product roadmapping, intent weaving assumes the builders are machines. Machines that can reason, plan, and act - but only within the bounds we describe. The challenge is twofold: give agents enough structure to act with confidence, while leaving sufficient context for human stakeholders to understand, audit, and redirect outcomes. This article describes the machinery behind that translation layer, down to the data contracts, review rituals, and trust metrics we run weekly.

**Key questions answered in this guide**
- How do we turn OKRs, market shocks, and risk mandates into machine-executable intents?
- What does the Autohand mission compiler actually do with all that context?
- Where do humans stay in the loop, and how are overrides fed back into autonomy?
- How do we prove that what shipped matches the strategic intent we encoded?

## 1\. Intent is the programmable form of strategy

Strategy documents are prose. Autonomy needs structure. We model the bridge as *intent*: a typed declaration of desired outcomes, constraints, and success evidence. Intent is the currency our agents consume. Every mission Autohand executes begins with an intent that has three layers:

- **Vision layer**: the why. Links to OKRs, regulatory commitments, customer promises.
- **Delivery layer**: the what. Defines scope, guardrails, dependencies, deadlines.
- **Evidence layer**: the how we know. Specifies observability signals, tests, and stakeholder acknowledgements.
![Diagram showing strategic inputs flowing into programmable intent layers and onward to autonomous execution](https://www.autohand.ai/images/intent-programmable-strategy.svg)

Strategic inputs are normalised into the three-layer intent schema before they reach Commander and the coding agents.

An intent authored in this format is both human-readable and machine-actionable. It anchors ambiguity - the agent can reference the evidence layer to know when to stop; stakeholders can inspect the vision layer to understand why the mission exists. Strategy becomes a network of intents instead of a PDF rotting in shared drives.

We maintain a public schema for intents. The schema references the Autohand knowledge graph so we can thread relationships: which intents descend from which goals, what risk domains govern them, and how historical missions performed under similar circumstances. As we discuss later, the mission compiler uses these links to generate appropriate agent swarms and guardrails.

## 2\. The Loom Model: weaving inputs into a single mission tape

Intent weaving relies on a mental model we call the **Loom** *not that startup acquired by Atlassian*. Picture three bundles of threads being pulled into a single mission tape:

1. **Strategic threads**: OKRs, board directives, market intelligence, customer escalations.
2. **Operational threads**: service catalogs, architecture decision records, compliance policies, runbooks.
3. **Signal threads**: telemetry anomalies, customer NPS, cost drift, reliability burn-downs.

The mission compiler is the loom. It ingests threads, checks compatibility, and produces a mission tape encoded as an intent graph plus execution plan. If threads conflict - say, a growth OKR demands a feature that breaches a risk policy - the loom surfaces the contradiction before agents do any work. Humans resolve the clash, update policy nodes, and rerun the weave.

Technically, the loom is a pipeline of five stages:

1. **Ingestion**: Structured connectors pull statements from OKR tools, CRM systems, governance wikis, and telemetry hubs.
2. **Normalization**: LLM-backed parsers map prose into canonical schemas (Goal, Risk, Opportunity, Threat).
3. **Contextualisation**: The compiler issues graph queries to enrich each statement with ownership, affected assets, and historical precedents.
4. **Conflict modelling**: Constraint solvers scan for duplicates, conflicting objectives, or policy violations.
5. **Intent emission**: The pipeline assembles mission candidates, ranks them by strategic impact, and opens them for human review.

Every stage is observable. We log transformation diffs, LLM reasoning paths, and solver conflicts. Stakeholders can always audit how an intent entered the system, why it looks the way it does, and who signed off.

## 3\. Inside the mission compiler

At the heart of intent weaving sits the mission compiler - a service that takes enriched intent graphs and generates executable plans for Commander. Here is what happens under the hood:

1. **Role assignment**: The compiler chooses the blend of agents (planner, architect, implementer, verifier) needed, factoring in risk tags and historical performance.
2. **Guardrail selection**: It queries the nervous system for relevant policies, runbooks, and reflex packages, bundling them into the mission kit.
3. **Work packetization**: The intent is decomposed into controllable waypoints: discovery tasks, diff synthesis, simulation, deployment, validation, comms. Each waypoint inherits constraints and success metrics.
4. **Human interface design**: The compiler decides where humans must stay in the loop - signoffs, escalation thresholds, stakeholder updates.
5. **Telemetry contracts**: It defines what signals must be collected to prove completion. These contracts feed into the Autohand nervous system so verification is ready before execution starts.

The output is a *mission manifest*: a bundle containing the intent, plan graph, agent roster, guardrails, telemetry contracts, and communication workflow. Commander ingests the manifest, spins up the swarm, and keeps the mission aligned with the original strategic thread.

## 4\. Patterns for capturing high-quality intent

Good intent is designed, not guessed. We coach teams on four capture patterns that keep autonomy aligned with reality:

- **Outcome-first prompts**: Start with evidence. “Show me baseline conversion, the desired delta, and the constraints.” Agents can only optimise what is measured.
- **Risk overlays**: Every intent carries a risk profile (safety, financial, compliance, brand). Profiles determine which guardrails must be active.
- **Stakeholder enumeration**: Identify whose world changes if the intent succeeds or fails. They are the ones who approve mission manifests.
- **Temporal scaffolding**: Define the cadence - once-off fix, continuous improvement, or seasonal campaign. Autonomy plans differently for each.

We codify these patterns into templates surfaced in our authoring tooling. When leaders compose intents, the UI guides them through the necessary dimensions, suggesting copy drawn from previous successful missions. This reduces drift and raises the overall quality of autonomy inputs.

## 5\. Tiered governance: keeping humans in the loop by design

Intent weaving is not a euphemism for removing humans. It is a way to ensure humans apply leverage where it matters. We run a tiered governance model:

1. **Tactical tier**: Product managers and tech leads author intents within their domains. They approve mission manifests and respond to reflex escalations.
2. **Strategic tier**: An autonomy council monitors portfolio heatmaps, resolves conflicting intents, and tunes risk appetite. They decide which domains graduate to higher autonomy levels.
3. **Audit tier**: Internal audit and compliance review reflex logs, verify evidence chains, and certify that missions delivered against policy commitments.

Commander reflects these tiers in its UI. Tactical owners see live status and upcoming approvals. Strategic leaders see trend analytics, trust metrics, and blockers. Auditors access immutable intent histories with linked telemetry records. By encoding governance in software, we eliminate the guesswork: everyone knows when autonomy acts alone and when it asks for human judgement.

## 6\. Evidence chains close the loop

Intent is only real if we can prove it was honoured. Autohand builds **evidence chains**: cryptographically hashed sequences linking intent, execution, telemetry, and stakeholder signoff. Each chain includes:

- **Intent hash**: the canonical representation of the mission at approval time.
- **Execution artifacts**: commits, test reports, deployment receipts, runbook steps, reflex logs.
- **Observability slices**: snapshots of agreed metrics before, during, and after the mission.
- **Signatures**: cryptographic attestations from agents and humans confirming completion.

Chains live in the Autohand knowledge graph and can be exported to your compliance vault. They give risk teams exactly what they need: not anecdotes, but verifiable proof that autonomy respected policy. When auditors ask “why did the system ship this change?”, we hand them the chain and the question answers itself.

## 7\. Why current benchmarks mislead AI coding agents

Public leaderboards make today’s coding agents look unstoppable. In production they still stumble, because the benchmarks we celebrate optimise for the wrong things. Most suites measure one-shot correctness of small functions with perfect unit tests, short-lived sandboxes, and unrestricted retries. Our customers ask agents to perform multi-step refactors under compliance rules, reuse existing abstractions, and keep the blast radius inside governance envelopes. Those realities rarely show up in benchmark harnesses.

- **Dataset bias**: Benchmarks over-sample “clean” repositories and ignore the entropy of real estates - forked dependencies, partial migrations, and inconsistent styles.
- **Grade inflation**: Passing a test suite is easy when the harness lets the agent overwrite fixtures or mutate the grader. That tells you nothing about how it behaves under read-only compliance or change-control constraints.
- **Time horizon mismatch**: Most evaluations stop once a green test appears. We care about whether the repo still builds a week later, whether observability signals stayed within policy, and whether humans trust the diff.
- **Lack of governance signals**: Benchmarks don’t ask agents to reference runbooks, respect ADRs, or collect sign-offs. Yet those are the critical moves inside enterprise workflows.

Because of this gap, Autohand treats standard benchmarks as smoke tests, not proofs. We augment them with scenario simulations drawn from live production logs, intent replay of past incidents, and evaluation metrics that punish guardrail breaches - even when the code “works.” Missions only advance to higher autonomy levels once they demonstrate resilience across this richer evaluation fabric.

## 8\. Pain Points of LLM Coding Agents in Software Development

To ground our guardrails, we catalogue how coding agents fail in the wild. The illustration and matrix below capture recurring pain points we see when autonomy meets complex software estates.

![Collage showing the recurring failure modes of AI coding agents across reliability, reasoning, and collaboration](https://www.autohand.ai/images/intent-weaving-problems.png)

Illustrated failure landscape: the further an agent strays from intent, the more human effort it takes to shepherd it back.

We express the same landscape as a table so teams can map issues to the Autohand practices that mitigate them.

| Domain | Representative failure pattern | Autohand counter-measure |
| --- | --- | --- |
| Code reliability & precision | Regenerates critical snippets, corrupting literals and quietly breaking logic. | Intent evidence layer demands diff-safe operations and structural checks before merge. |
| Context & repo awareness | Reimplements existing helpers; loses track of repo conventions in large estates. | Knowledge graph grounding plus Commander mission briefs keep canonical paths in scope. |
| Reasoning & problem-solving | Charges ahead on wrong assumptions, rarely pausing to clarify. | Intent templates enforce explicit unknowns and escalation triggers. |
| Testing & validation | Skips or tampers with tests to get green lights. | Evidence chains require trusted test harnesses and telemetry confirmation. |
| Collaboration & review | Produces bloated diffs that hide meaningful change. | Commander enforces scoped missions and runbook-aligned diff budgets. |
| Tool use & environment | Misuses shell tools, confuses OS nuances, or loops automation. | Intent delivery layer encodes approved toolchains and execution policies. |
| Workflow & productivity | Touches unrelated files and inflates scope, slowing humans down. | Mission compiler rewards completion confidence over volume, penalising sprawl. |
| Learning & adaptation | Forgets feedback and repeats mistakes after context loss. | Reflex logs capture overrides and feed them back into policy weightings. |
| Design & refactoring | Breaks architecture while attempting “refactors” of core modules. | Guardrails require dependency plans and structural diff validation. |
| Developer experience | Feels like supervising an overconfident intern, consuming reviewer bandwidth. | Intent clarity scores and mission health dashboards expose supervision cost. |
| Highlighted failures | Regenerates instead of copy-pasting, rarely asks before disruptive edits. | Commander requires clarification steps for high-impact mutations and documents provenance. |

The remainder of this section unpacks each domain in more detail so you can map them to your own autonomy posture.

### 1\. Code reliability and precision

- Rewrites instead of true copy-paste, causing silent drift in logic and syntax.
- Subtle corruption of URLs, regexes, constants, and date values.
- Breaks exact strings (e.g., IDs, paths, TikZ, LaTeX).
- Changes tests to pass rather than fixing real issues.
- Deletes or rewrites unrelated code segments.
- Weak at safe renames and refactors, lacking IDE-grade precision.
- Generates bloated or duplicated code and unnecessary checks.

### 2\. Context and repository awareness

- Limited understanding of existing helpers, styles, or frameworks.
- Reimplements functionality that already exists.
- Poor navigation in large repos or monorepos.
- Gets paths and working directories wrong, especially in Windows.
- Loses context across multiple tools or directories.
- Needs constant prompting to recall repo-specific conventions or CLAUDE.md rules.

### 3\. Reasoning and problem-solving

- Rarely asks clarifying questions before acting.
- Makes strong assumptions, guesses incorrectly, and persists in error.
- Overconfident tone masks uncertainty and lack of reasoning depth.
- Cannot generalize across domains or detect when a task is infeasible.
- Long tasks degrade mid-way, losing coherence or repeating earlier steps.
- Fails at structured iteration or cyclic reasoning (e.g., processing lists or loops).

### 4\. Testing and validation

- Skips or falsifies tests to appear successful.
- Silently introduces regressions and subtle semantic errors.
- Adds fake or placeholder data without notice.
- Ignores explicit constraints or modifies critical constants.
- Poor at verifying real-world data or checking for stale information.

### 5\. Collaboration and code review

- Produces large diffs that obscure meaningful changes.
- Rewritten “moved” code hides modifications from reviewers.
- Reviewers must now focus on semantic drift instead of logic only.
- Increases overall validation and review workload.
- Requires explicit mention of AI use in PR templates for effective reviews.

### 6\. Tool use and environment handling

- Misuses or confuses shell tools and commands.
- Struggles with multi-process environments (e.g., running tests, scripts).
- Weak understanding of platform differences between Linux, macOS, and Windows.
- Brittle when coordinating concurrent tasks or workflows.
- May loop or recursively trigger itself (e.g., S3 resize loops).

### 7\. Workflow and productivity

- Overproduces verbose, noisy code for simple tasks.
- Touches unrelated files, causing scope creep.
- Forgets earlier constraints and requires repetitive instructions.
- Needs heavy human supervision to ensure correctness.
- Review and testing become bottlenecks due to subtle errors.
- Slower than expected when babysitting or course-correcting.

### 8\. Learning and adaptation behavior

- Training appears biased toward speed over accuracy or safety.
- Fails to internalize human feedback during sessions.
- Forgets applied corrections or conventions after context loss.
- Doesn’t “remember” prior clarifications unless restated repeatedly.

### 9\. Design and refactoring execution

- Fails to maintain structural integrity during refactors.
- Deletes necessary files or leaves dead code behind.
- Partially migrates architectures without updating dependencies.
- Refactors appear correct syntactically but fail logically in tests.
- Misses domain-specific helpers or abstractions during reorganization.

### 10\. Developer experience

- Overconfident intern behavior: fast, eager, but careless.
- Feels “off” or not on the same wavelength as human coders.
- Output quality varies wildly between simple CRUD work and complex logic.
- “Vibe coding” mismatch - lacks human intuition for structure and intent.
- Forces developers to micro-manage and re-verify every step.

### 11\. Highlighted failures

- LLMs don’t actually copy-paste code; they regenerate it from memory.
- They fail to ask clarifying questions before big changes.
- Some tools like Codex mimic copy-paste with `sed` or `awk`, but unreliably.
- Some frameworks (like Roo) encourage better questioning but remain limited.
- Speed and throughput seem prioritised over accuracy and collaboration.
- Overall: coding agents behave like overconfident interns, not disciplined engineers.

## 9\. Anti-patterns we eliminated

The early days of autonomy taught us painful lessons. The worst anti-patterns included:

- **Intent by committee**: Dozens of authors produced contradictory statements. We introduced opinionated templates and domain custodians to restore coherence.
- **No evidence clause**: Teams shipped intents without specifying success signals, leading to endless scope creep. Now every intent fails validation unless evidence fields are complete.
- **Invisible overrides**: Humans overrode autonomy silently, eroding trust. We now require overrides to be logged as reflex annotations with rationale and follow-up tasks.
- **Static knowledge**: Policy references drifted as documentation aged. Knowledge-keeper agents now continuously reconcile knowledge graph edges with source systems.

Intent weaving defeated these anti-patterns by making intent a living artefact shared by machines and humans, instead of a static backlog item.

## 10\. Tooling that supports intent authors

Authoring great intent should feel like a conversation, not a compliance chore. Our tooling provides:

- **Contextual recommendations**: As authors type, the tool suggests relevant policies, recent incidents, and similar intents for reuse.
- **Simulation previews**: The mission compiler can run “what-if” scenarios showing which agents would be assigned, highlighting over- or under-staffed plans.
- **Stakeholder heatmaps**: Visual overlays reveal whose domains are most affected, helping leaders prioritise reviews.
- **Live risk scoring**: A trust scoring model predicts the autonomy posture (Level 3 vs. Level 4) appropriate for the mission, explaining the drivers.

This tooling is accessible from Slack, the web console, or API so teams can capture intent wherever strategy discussions happen. Commander ingests everything via the same API regardless of channel, keeping the system cohesive.

## 11\. Measuring the quality of intent weaving

We track specific metrics to know whether intent weaving is working:

- **Intent clarity score**: Derived from reviewer feedback, counts ambiguities resolved post-approval.
- **Override rate**: How often humans abort autonomous missions because intent was wrong or incomplete.
- **Evidence timeliness**: Time between mission completion and evidence chain publication.
- **Conflict resolution lag**: Hours between detecting conflicting intents and resolving them.
- **Strategy alignment index**: Weighted ratio of mission impact to strategic priority score.

Monthly reviews correlate these metrics with business outcomes. If override rates spike, we inspect the authoring tooling, templates, and training materials. If clarity scores dip, we run clinics with product and risk leads to reinforce best practices.

## 12\. Where humans provide irreplaceable value

Autonomy is not a replacement for product intuition, ethical reasoning, or customer empathy. Humans still:

- Shape the strategic narrative that intents reference.
- Resolve conflicts between stakeholders with competing incentives.
- Interpret weak signals that sensors cannot (yet) quantify.
- Decide when to change the rules of the game - pivoting strategy, redefining success.

Intent weaving merely scaffolds these contributions so agents respect them. It frees humans to exercise taste and judgement, not babysit execution details.

## 13\. The future of intent weaving

We see three major evolutions on the horizon:

1. **Forward-looking simulation**: The mission compiler will predict downstream consequences weeks ahead by simulating combined mission graphs. Think Monte Carlo autoplan.
2. **Cross-organisation network**: Enterprises running Autohand will share anonymised intent templates, letting industries standardise on proven patterns.
3. **Semantic reconciliation**: Advances in language models will let us reconcile conflicting regulatory and strategic statements automatically, proposing compromise intents for human review.

As autonomy climbs toward Level 5, intent weaving matures from a translation layer into a strategic operating system. Strategy will no longer be a quarterly ritual; it will be a continuously evolving tapestry woven directly into the systems that execute it.

---

## Resources

- Autohand. [Software 3.0 Manifesto](https://www.autohand.ai/manifesto.html).
- Autohand. [The Autohand Nervous System](https://www.autohand.ai/updates/autohand-nervous-system.html).
- Wardley Mapping Community. " [Mapping Strategy](https://learnwardleymapping.com/home) ".
- Amy Edmondson. *The Fearless Organization* (for designing safe escalation rituals).
- Gojko Adzic. *Specification by Example*.
- Simon Willison. " [Parallel coding agents are already here](https://simonwillison.net/2025/Oct/5/parallel-coding-agents/) ".