---
applyTo: '**/tests/**'
description: 'Comprehensive testing standards and guidelines for all repositories in the Cracking Shells Organization.'
---

# Cracking Shells Codebase Testing Standards

These standards ensure:
- **Consistency:** Standardized naming, organization, and implementation patterns
- **Maintainability:** Clear lifecycle management and regular cleanup processes  
- **Flexibility:** Support for different test types and execution scenarios
- **Quality:** Comprehensive coverage with clear documentation and debugging support
- **Scalability:** Design patterns that support growth and automation

## 1. Test File Organization & Naming

- **Central Test Runner:**  
  All tests are executed via a single entry point: `run_tests.py`.
  - This script must:
    - Discover and run all test files in the codebase.
    - Support flags for test types (e.g., `--regression`, `--feature`, `--development`).

- **Test File Naming Convention:**  
  - **Development tests:** `dev_test_<test_name>.py`
  - **Regression tests:** `regression_test_<test_name>.py`
  - **Feature tests:** `feature_test_<test_name>.py`

- **Test File Placement:**  
  - Place all test files in a dedicated `tests` directory at the project root, or in a `tests` subdirectory within each major package/module.

---

## 2. Test Types & Lifecycle

- **Development Tests:**  
  Temporary, focused on validating postconditions during development or refactoring. Remove after stabilization.

- **Regression Tests:**  
  Permanent, ensure existing critical functionality is not broken by future changes.

- **Feature Tests:**  
  Permanent, confirm new features work as intended and document requirements.

---

## 3. Test Coverage Guidelines

- **Unit Tests:**  
  Cover isolated logic (e.g., event system, provider abstraction, command parsing).

- **Integration Tests:**  
  Validate that major components (e.g., chat workflows, LLM providers, MCP server integration) work together as expected.

- **Redundancy:**  
  Avoid redundant tests. Prefer broader integration tests for stable, high-level workflows.

---

## 4. Mock vs Real Integration Strategy

- **Unit Tests:** Mock external dependencies (API calls, file system, network operations)
- **Integration Tests:** Use real implementations when testing component interactions
- **Feature/Regression Tests:** Prefer real integrations to validate end-to-end workflows

**Practical Rule:** If testing a single class/function's logic → mock. If testing how components work together → real.

---

## 5. Test Data Management

- **Structure:** Create a `test_data/` directory for reusable test fixtures:
  ```
  tests/
    test_data/
      configs/          # Test configuration files
      responses/        # Mock API/tool responses  
      events/           # Sample event payloads
      servers/          # Dummy MCP servers for integration tests
  ```

- **Guidelines for Test Data:**
  - **Configuration Files:** Sample settings, provider configurations (leverage settings registry APIs where available)
  - **Mock Responses:** Standard tool call responses, error responses, API chunks
  - **Event Payloads:** Sample events for testing event flows
  - **Test Servers:** Lightweight dummy servers for integration testing (e.g., simple MCP servers with basic tools)

- **Best Practices:**
  - Use consistent test data across similar tests to reduce maintenance
  - Create reusable mock factories for common components
  - Keep test data minimal and focused on the specific test scenario

---

## 6. Test Implementation Standards

- **Framework:**  
  - Continue using `unittest` for consistency, as it is already in use and well-integrated.
  - If you want more advanced features (fixtures, parameterization, better output), consider gradually introducing `pytest`. Both can coexist, but avoid mixing styles within a single file.
  - Recommendation: Stick with `unittest` unless you have a clear need for `pytest` features.

- **Structure:**  
  - Each test file should be self-contained and import only what it needs.
  - Use setup/teardown methods for complex dependencies (e.g., mock LLM providers, MCP servers).

- **Assertions:**  
  - **Always include descriptive messages in assertions:**
    ```python
    # Bad
    self.assertEqual(result, expected)
    
    # Good  
    self.assertEqual(result, expected, 
        f"Event processing failed: expected {expected}, got {result}")
    ```
  - Assert on both state and side effects (e.g., event emission, command output).

- **Documentation:**  
  - Each test file must start with a docstring describing its purpose and scope. Refer to the [docstring guidelines](./documentation.instructions.md) for more information.
  - Each test method should have a descriptive name and inline comments for non-obvious logic.

---

## 7. Test Categories & Tags

- **Decorator Location:** Create a `tests/test_decorators.py` file to define reusable test decorators:
  ```python
  # tests/test_decorators.py
  def slow_test(func):
      """Mark test as slow-running."""
      func._slow = True
      return func
  
  def requires_api_key(func):
      """Mark test as requiring API credentials."""
      func._requires_api = True
      return func
  
  def integration_test(func):
      """Mark test as integration test."""
      func._integration = True
      return func
  
  def requires_external_service(service_name):
      """Mark test as requiring specific external service."""
      def decorator(func):
          func._requires_service = service_name
          return func
      return decorator
  ```

- **Common Tags to Use:**
  - `@slow_test` - Tests that take significant time
  - `@requires_api_key` - Tests needing API credentials
  - `@integration_test` - Multi-component integration tests
  - `@requires_external_service("ollama")` - Tests needing specific services

- **Centralized Test Runner Integration:**
  - The runner should support filtering by tags (e.g., `--skip-slow`, `--only-integration`)
  - Tags enable selective test execution in different environments

---

## 8. Test Independence & Parallelization

- **Test Independence Guidelines:**
  - No shared global variables between tests
  - Clean up any created files/directories in tearDown methods
  - Use unique identifiers for temporary resources (timestamps, UUIDs)
  - Mock time-sensitive operations to avoid race conditions

- **Resource Management:**
  - Ensure proper cleanup of background processes, open connections, and temporary files
  - Use context managers where possible for automatic resource cleanup

- **Implementation Priority:** Focus on test independence first, parallelization can be added later as needed.

---

## 9. Test Review & Maintenance

- **Development Test Cleanup:**  
  After a major implementation or refactor, review all `dev_test_*.py` files and remove those no longer relevant.

- **Regression/Feature Test Review:**  
  Regularly review for redundancy and update as features evolve.

- **Test Runner Maintenance:**  
  Keep `run_tests.py` up to date with new flags or test types as needed.

- **Stale Test Detection:**
  - Run stale test detection routinely at the end of testing workflows
  - Create a simple script to identify tests not modified in 90+ days
  - Review flagged tests for relevance and update or remove as needed

---

## 10. Centralized Test Runner Design

- **Printed Output:**  
  - Clear, color-coded output indicating test type currently running
  - Summary of passed/failed/skipped tests by category
  - Detailed error output for failures with actionable debugging information

- **Lifecycle per Flag:**  
  - Parse command-line flags to select test types, individual files, or specific tests
  - Initialize environment and dependencies only for selected tests
  - Clean up resources after each test group or file execution

- **Design Pattern - Test Suite Factory:**
  ```python
  # Example structure for run_tests.py
  import unittest
  import argparse
  
  def discover_tests(test_type=None, file=None, test_name=None, skip_tags=None):
      """Dynamically build test suites based on criteria."""
      # ... logic to discover and filter tests ...
      return suite
  
  if __name__ == "__main__":
      parser = argparse.ArgumentParser()
      parser.add_argument("--regression", action="store_true")
      parser.add_argument("--feature", action="store_true") 
      parser.add_argument("--development", action="store_true")
      parser.add_argument("--file", help="Run tests from specific file")
      parser.add_argument("--test", help="Run specific test method")
      parser.add_argument("--skip-slow", action="store_true")
      args = parser.parse_args()
      
      suite = discover_tests(
          test_type=determine_type_from_args(args),
          file=args.file,
          test_name=args.test,
          skip_tags=["slow"] if args.skip_slow else None
      )
      runner = unittest.TextTestRunner(verbosity=2)
      result = runner.run(suite)
      exit(0 if result.wasSuccessful() else 1)
  ```

- **Execution Capabilities:**
  - Run all tests of a given type
  - Run all tests in a specific file
  - Run a single test method by name
  - Filter tests by tags/decorators
  - Provide appropriate exit codes for CI/CD integration

---
