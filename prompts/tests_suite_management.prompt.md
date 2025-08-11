---
mode: agent
tools: ['codebase', 'terminalSelection', 'terminalLastCommand', 'findTestFiles', 'searchResults', 'editFiles', 'search', 'runCommands', 'getPythonEnvironmentInfo', 'getPythonExecutableCommand']
---

# Test Suite Management Prompt

## Purpose
This prompt is designed to guide an agent in updating, cleaning, and maintaining the test suites in this repository according to the standards in the [instructions](../instructions/testing.instructions.md). It should be used:
- After major refactoring to remove obsolete, redundant, or development-only tests
- Routinely, to check the sanity and relevance of the test suites

## Instructions for the Agent
1. **Review the current test suite:**
	- Identify all test files and categorize them by type (development, regression, feature, integration, etc.)
	- Check for compliance with naming, placement, and documentation standards
	- Detect redundant, obsolete, or development-only tests that should be removed
	- Ensure all permanent tests (regression/feature/integration) are up to date and relevant

2. **Test Data and Mocking:**
	- Verify that test data is organized and reused according to the guidelines
	- Check that mocks and real integrations are used appropriately for each test type

3. **Test Tags and Decorators:**
	- Ensure that slow, integration, and external-service-dependent tests are properly tagged
	- Confirm that decorators are defined in the correct location and used consistently

4. **Test Independence and Cleanup:**
	- Check that tests are independent and do not share state
	- Ensure proper resource cleanup in all tests

5. **Stale Test Detection:**
	- Run the stale test detection script and review flagged tests for removal or update

6. **Centralized Test Runner:**
	- Confirm that `run_tests.py` supports all required flags and filtering
	- Ensure output is clear and actionable

## Output
Provide a summary of actions taken or recommended, including:
- List of removed or updated test files
- List of tests needing further review
- Any structural or organizational changes made
- Any issues or blockers encountered

Refer to the [instructions](../instructions/testing.instructions.md) for all standards and requirements.
