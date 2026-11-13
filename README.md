# Mnemosyne — Human–Wiki–Agent Integration

**An experimental agent prototype exploring persistent, revision-aware knowledge and human-governed memory.**

HWI is one of two spin-offs from **AutoGPT Lite** (the other is [Desiderata](https://github.com/dinikifo/Desiderata)). Both explore memory and reasoning limitations encountered when working with AutoGPT-style agents. HWI combines the author's AutoGPT Lite runtime with modules developed for the author's **PERSONAL.WIKI** and personal versioning/provenance system (**PVS**). The emphasis is not only remembering more text: it is making knowledge persistent, retrievable, revision-aware, and inspectable before accepting changes.

It was developed through substantial human-directed collaboration with generative AI systems, including AI-assisted design, code development, criticism, testing, and documentation. The identities of particular systems are not necessary to evaluate the released code. Human authorization governs project goals and policy; executable checks and review receipts provide bounded technical evidence. Neither human authorization nor AI output alone establishes scientific correctness.

**Status: experimental prototype, not a production system.** The author reports that it is stable enough to serve as a base for experiments, but it has **not** been extensively tested for bugs, hostile inputs, security failures, or ways to break its authorization mechanisms. No formal reliability or safety certification is claimed.

## What HWI explores

- **Persistent knowledge beyond conversation history:** integrating a local wiki and its SQLite-based records with the agent runtime rather than depending solely on compressed chat/action context.
- **Memory provenance and revisions:** recording change histories, retrieving existing information, inspecting sources, and working with explicit revision identities.
- **Symbolic and structured reasoning:** exploring rules, knowledge structures, evidence boundaries, and agent decisions beyond free-form prompt responses.
- **Human-reviewed changes:** separating generated suggestions from authority to alter protected wiki records, using proposal, review, and revision-checking workflows.
- **Experimental governance and formation:** researching task-fitness gates, review queues, and first-run purpose conversations; these newer subsystems do not confer production authority.
- **Local LLM integration:** supporting Ollama in selected workflows, while retaining offline tests with synthetic notebooks and controlled fixtures.

The separation between **agent reasoning**, **durable knowledge**, and **permission to change that knowledge** is central to the design.

## Possible applications

These are areas for experimentation, **not turnkey or validated end-user applications**:

- Personal home-assistant prototypes with long-lived local context.
- LLM-enhanced personal wikis, research notebooks and note-taking tools.
- Infrastructure for experimental agents, memory architectures, version-aware knowledge systems, and human-in-the-loop workflows.

The suitability of any application depends on further testing, task-specific constraints and independent security measures.

## How this project relates to the others

| Project | Relationship |
| --- | --- |
| **AutoGPT Lite** | Independently written AutoGPT Classic-style local agent prototype; foundation for both spin-offs |
| **[Desiderata](https://github.com/dinikifo/Desiderata)** | Separate AutoGPT Lite spin-off exploring memory and symbolic reasoning (see its repository for details) |
| **HWI (this repository)** | AutoGPT Lite-derived prototype integrating PERSONAL.WIKI knowledge, PVS-inspired provenance/revisions and human review |

PERSONAL.WIKI and PVS are the author's previously developed projects; links to their original repositories can be added when their exact URLs are provided. **HWI reuses and extends AutoGPT Lite source code.** It is not a clean-room reimplementation of AutoGPT Lite, and it is not affiliated with the upstream AutoGPT project.

## Quick exploration

Use a dedicated, unprivileged account and synthetic notes while experimenting. Python 3.11+ is required; some workflows need `requests` and `cryptography`, plus [Ollama](https://ollama.com/) and a local model for live LLM use. Additional platform features may require other optional dependencies. No complete dependency lock or cross-platform installation guarantee is provided.

From the extracted repository root:

```bash
# Check the integrity of this prepared source snapshot.
python3 VERIFY_ARCHIVE.py

# Execute the included offline test suites (no live model required).
bash RUN_ALL_OFFLINE.command

# Inspect the governance command surface.
bash RUN_GOVERNANCE.command --help

# Explore advisory Agent Formation without an LLM.
bash RUN_AGENT_FORMATION.command start --manual
```

`sh INSTALL.sh --help` documents machine-profile setup. The manual is [`USER_MANUAL.md`](USER_MANUAL.md). The offline suite uses temporary synthetic notebooks rather than personal wiki data. Running tests successfully on one machine does not mean the agent has been hardened or certified for real workloads.

**Important:** some old reference documents mention archived Git bundles, earlier refactor checkpoints and the original consolidated release. Those are deliberately excluded from this source-first GitHub package; see [`docs/RELEASE_CLEANUP.md`](docs/RELEASE_CLEANUP.md). The original research snapshot remains separately preserved.

## Source layout

| Directory | Purpose |
| --- | --- |
| `CODE/APPROVED_AGENT_PROVIDER/autogpt_lite/` | AutoGPT Lite-derived agent runtime and Ollama integration |
| `CODE/APPROVED_WIKI_CORE/personal_wiki_core/` | PERSONAL.WIKI storage, history, revisions, and related core logic |
| `CODE/APPROVED_WIKI_CORE/hwi/` | HWI knowledge, provenance, retrieval and reviewed-write integration |
| `CODE/DUALFLOW/hwi_governance/` | Experimental governance, task fitness, review and recovery components |
| `CODE/DUALFLOW/hwi_formation/` | Experimental advisory Agent Formation workflows |
| `CODE/DUALFLOW/tools/` | Dual-Flow simulation, evaluation, regression tests and tools |
| `CODE/DUALFLOW/docs/` | Specifications and experiment documentation |
| `CONTENT_EVAL/`, `MAC_TOOLS/` | Content-evaluation fixtures and macOS diagnostic harness |
| `docs/history/` | Historical accepted-baseline records, **not** an approval of current experiments |

## What has and has not been validated

The source archive records an accepted **10/10 Dual-Flow research baseline**. It also contains later governance, interrupted-submission recovery and formation *experiments*, for which the source material explicitly says separate production acceptance was not granted. Historical approval documents have been preserved under `docs/history/` to avoid confusing the baseline with new features.

Important limitations include:

- No comprehensive bug hunt, fuzzing, adversarial security testing, or demonstrated robustness to arbitrary model responses.
- A verified signature, conforming schema or test result does not independently prove that retrieved knowledge is true or current.
- Protected wiki writes and model-driven actions still require appropriate human control; an LLM response is not authorization.
- Wiki review export is a manually imported snapshot, not a fully synchronized live review UI.
- Recovery cannot make separate SQLite databases into a single atomic transaction.
- Additional real-machine qualification, key custody review and integration testing are needed before even considering deployment to sensitive or autonomous workflows.

Treat files, notes, retrieved content, model output and generated commands as untrusted. Do not use real keys, private notebooks or valuable data for initial experiments. Agent code execution is **not** a security sandbox.

## Research status and lineage

The clean repository contains active source, offline tests, user-facing documentation, and selected historical status records. It intentionally excludes Git bundles, nested ZIP baselines, generated manuals, duplicate trees and historical refactor logs. The original accepted source trees remain recognizable by directory name, but this is a **repackaged publication**, not a byte-for-byte reproduction of the archived release. Its new integrity manifest verifies the repackaged files only.

## License

The author's original source code and documentation in this repository are released under **[CC0 1.0 Universal](LICENSE)** (`CC0-1.0`). The full public-domain dedication is in [`LICENSE`](LICENSE). CC0 does not relicense independent third-party dependencies or grant patent/trademark rights. Review provenance before redistributing any material owned by someone else.
