## Architecture Update — November 2026

### Modular Routing and Diagnostic Rules

Mnemosyne has undergone an architectural refinement focused on improving component independence, communication, maintainability, and transparency.

The original component-based agent runtime has been preserved. The changes primarily concern how supporting subsystems interact and how deterministic decisions are represented.

### Key Changes

**1. Typed Message Routing**

Introduced an ELIZA-inspired deterministic message router that coordinates selected component interactions through structured, validated messages.

The router supports explicit message types, source validation, transition contracts, and controlled dispatch. It reduces direct dependencies between participating subsystems without replacing their internal logic.

**2. Decoupled Component Interfaces**

Introduced replaceable interfaces for selected operations involving:

- Agent Formation and knowledge retrieval
- Local language-model interactions
- Evaluation and reporting
- Governance status and proposal review

These interfaces allow component implementations to be substituted and tested independently while preserving existing functionality.

**3. Self-Documenting Diagnostic Rules**

Introduced lightweight `DiagnosticRule` and `DiagnosticEngine` classes for representing deterministic checks as readable rule definitions.

Rules associate conditions with descriptions, callbacks, and subsequent checks, making diagnostic logic easier to understand, test, and maintain.

**4. Explicit Validation and Control Boundaries**

Strengthened inter-component validation through typed contracts, defined transitions, bounded processing, and fail-closed behavior.

The message router does not acquire execution authority. Existing services remain responsible for tool execution, persistent state, approvals, and protected knowledge operations.

**5. Improved Testing and Reproducibility**

Expanded test coverage to include routing behavior, component substitution, invalid transitions, malformed messages, compatibility, and failure handling.

The consolidated codebase has also been packaged with integrity verification and documented rollback procedures.

### Architectural Impact

These changes establish a clearer separation of responsibilities:

**Language models interpret and propose. The router coordinates. Diagnostic rules evaluate conditions. State machines manage workflow. Trusted services enforce authority.**

The original agent's component kernel, tool-registration mechanism, and supervised execution model remain intact.

### Compatibility and Development Status

The new routing capabilities are introduced incrementally, with selected paths remaining opt-in. Existing executable tools continue to use the original component interfaces.

The consolidated framework has passed its offline regression checks, but remains experimental. Production security hardening and operational validation are still required.

### Further Documentation

Detailed technical documentation is provided separately, including the original architecture, routed architecture, engineering change report, and tool development guides.

These documents describe the implementation, design decisions, compatibility considerations, and verification results in greater depth.