# Research Report: Effective Harnesses for Long-Running Agents

Based on a deep dive into the `oh-my-agent-main` repository, here is an analysis of what constitutes an effective "harness" for long-running AI agents. 

The `oh-my-agent` project defines itself as a **portable, role-based agent harness** meant for serious AI-assisted engineering. Its design choices highlight several key characteristics that prevent agents from getting confused, looping indefinitely, or making destructive changes during extended, complex tasks.

## 1. Explicit, Phase-Gated Workflows
Long-running agents fail when they try to do everything at once. Effective harnesses break work down into strict sequences (e.g., the `ultrawork.md` workflow has 5 phases: Plan, Implementation, Verify, Refine, Ship).
- **Mandatory Gates**: An agent cannot proceed to the next phase until a gate condition is met (e.g., `IMPL_GATE` requires build success and tests passing).
- **Review Steps**: There are explicit review steps (11 out of 17 steps in `ultrawork.md` are reviews), ranging from Alignment Review to Over-Engineering Review, ensuring the agent constantly verifies its direction.

## 2. Role-Based Subagent Spawning
Instead of one massive context window for a single "God Agent," the harness spawns specialized domain agents in parallel.
- Agents like `pm-agent`, `frontend-agent`, `qa-agent`, and `debug-agent` are spawned via CLI (`oh-my-ag agent:spawn`) into separate background processes.
- This isolates the context. The Frontend agent only cares about frontend logic, while the QA agent focuses on OWASP security, performance, and regressions. 

## 3. Persistent Memory Protocol (Serena Memory)
Long-running agents lose context if they rely purely on the chat history. The harness uses a persistent memory system (often referred to as "Serena Memory" in the repo).
- Agents write state to `.serena/memories` using Model Context Protocol (MCP) tools.
- Files like `orchestrator-session.md`, `task-board.md`, and `progress-{agent}.md` act as an asynchronous communication layer. The orchestrator polls these files rather than holding idle connections, preventing timeouts and context loss.

## 4. Context Loading Strategy
Feeding an entire repository to an agent guarantees hallucinations. The harness enforces a strict context-loading protocol (`.agents/skills/_shared/context-loading.md`). Subagents are only given the specific API contracts, task descriptions, and files they strictly need to fulfill their domain-specific role.

## 5. Automated Out-of-Band Verification
A harness must verify agent output using external deterministic tools.
- In `orchestrate.md`, completed agents are checked via `bash .agents/skills/_shared/verify.sh {agent-type} {workspace}`.
- If the exit code is 0, the result is accepted. If 1, the agent is respawned automatically with the error context for a limited number of retries.

## Conclusion
An effective harness for long-running agents shifts the paradigm from **"prompting a single LLM to write an app"** to **"orchestrating a virtual engineering team."** It relies on rigid project management (PM agent), strict isolation of concerns, asynchronous memory protocols, and deterministic verification gates to safely guide agents through complex software development lifecycles.
