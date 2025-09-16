# Report Types

Here are actionable details regarding different report types the coding agents might be asked to write.

## Test Definition Report

**MUST DO**: Generate a comprehensive test definition report before any implementation begins.

Tests will be used to verify that code changes implemented by the coding agent behave as expected.

**Report Requirements**:
- **Mandatory inclusion** in all preparation reports that precede implementation work
- **Test categorization** based on task type:
  - **Feature tests**: Derived from user-defined use cases or discovered during preparation discussions. These become permanent regression/integration tests (reference org's Testing Guidelines for classification)
  - **Fix tests**: Focused on verifying the specific bug no longer occurs, plus validation that existing functionality remains intact. These are typically temporary "development" tests (reference org's Testing Guidelines for classification)
- **Test specification components**:
  - Test case definitions with clear input/output expectations
  - Test data requirements and setup procedures
  - Expected behavior documentation for edge cases
  - Validation criteria and success metrics
- **User validation workflow**: Default behavior requires at least one report iteration with user approval. The coding agent must present the test definition report and engage in refinement discussions with the user before proceeding to implementation.

**Agent Action**: Present test definitions in a structured report format that facilitates user review and iterative refinement.

## Test Execution and Validation Report

**MUST DO**: Generate a comprehensive test execution report demonstrating implementation completeness.

This report provides evidence that the implementation meets all requirements and maintains system integrity.

**Report Requirements**:
- **Complete test execution results**: All defined tests from the upstream Test Definition Report must be executed and documented
- **Performance verification**: Benchmark results and performance criteria validation
- **Regression confirmation**: Evidence that existing functionality remains unaffected
- **Edge case validation**: Documentation of boundary condition testing outcomes
- **User review process**: Present execution results for user validation, highlighting any deviations from expected outcomes

**Agent Action**: Generate a structured execution report that clearly demonstrates requirement fulfillment and enables user verification.

## Documentation Update Report

**MUST DO**: Generate a documentation impact analysis and update report after implementation completion.

Documentation represents the organization's front-facing knowledge base and must remain current with all code changes.

**Report Requirements**:
- **Comprehensive documentation search**: Systematically identify all documentation sections potentially affected by the implementation
- **Impact analysis**: Document which sections require updates and why
- **Update proposals**: Present specific documentation changes following:
  - Organization's documentation guidelines
  - Existing documentation style and format
- **User review process**: Present the documentation update report for user validation and refinement before applying changes

**Agent Action**: Generate a structured report detailing documentation impacts and proposed updates that enables user review and collaborative refinement.

## Knowledge Transfer Report

**MUST DO**: Generate a knowledge transfer report to facilitate future development and feature chaining.

This report captures implementation insights and creates a foundation for subsequent development work.

**Report Requirements**:
- **Implementation summary**: High-level overview of what was built and how it works
- **Key decisions documentation**: Technical choices made during implementation with rationale
- **Lessons learned**: Insights gained during development that could benefit future work
- **Integration points**: How this implementation connects with existing systems and potential extension points
- **Troubleshooting guide**: Common issues and resolution approaches discovered during implementation
- **Future development enablers**: Identified opportunities for feature enhancement or related implementations
- **User collaboration**: Present the knowledge transfer report for user review to ensure critical insights are captured and accessible for team knowledge sharing

**Agent Action**: Generate a comprehensive knowledge transfer document that serves as both implementation record and development catalyst for future work.