You are a software engineer building the HaruQuantAI platform. We are implementing the project one file at a time.

Your task is to implement the requirements for:
- **Target File**: [Target File Path, e.g., tools/utils/logger.py]
- **Requirements Source**: [Requirements Doc, e.g., docs/source-requirements/01-utils.md]
- **Requirements Section**: [Section Name/Number, e.g., Section 10.3]

### Instructions:
1. **Load Instructions First**: Read the `AGENTS.md` operating guide in the root workspace. You must follow all rules in `AGENTS.md` (Code Quality, Tool/Agent Standards, Safety & Governance) without exception.
2. **Read Requirements**: Read the [Requirements Source] document and extract the exact functional/non-functional requirements, edge cases, error-handling behaviors, and testing rules for [Target File].
3. **Dry Run (Mandatory)**: 
   - Before modifying any files, perform a Dry Run.
   - Report:
     - Files to read/change.
     - Commands/tests planned.
     - Scope boundaries.
     - Blockers/risks.
     - Rollback path.
   - **Stop and wait for my explicit approval** (`APPROVED: EXECUTE`) before writing or changing any files.
4. **Execution (After Approval)**:
   - Implement the file with type hints, structured logging (`from tools.utils import logger`), input validation, and explicit error handling.
   - Write corresponding unit tests (aiming for >=80% coverage) and a runnable usage example as mandated by the standards.
5. **Documentation & Changelog**:
   - Update `CHANGELOG.md` under `## [Unreleased]` to record the added functionality.
6. **Final Report Checklist**:
   - Provide a final report containing the checklist from Section 10 of `AGENTS.md`, files changed, validation/test results, and rollback path.

Let's start. Perform the Dry Run now and report your plan.
