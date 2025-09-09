# CrackingShells Definitive Testing Standard

## Executive Summary

This standard synthesizes comprehensive analysis findings with proven organizational practices to create a practical, modern testing architecture that solves real pain points: better CLI control, readable file structure, readable test output, and industry alignment.

**Key Decisions:**

- **Universal hierarchical structure** with industry-standard `test_*.py` naming
- **Three-tier categorization** (development/regression/integration) with feature test migration
- **Modern CLI interface** inspired by Hatchling's successful patterns
- **Enhanced output formatting** to reduce cognitive overload
- **Practical flexibility** balanced with clear requirements

## 1. Directory Structure Standard

### 1.1 Universal Hierarchical Structure

**All repositories must use this structure:**

```plaintext
tests/
├── __init__.py
├── test_decorators.py
├── test_data_utils.py
├── test_output_formatter.py
├── development/
│   ├── __init__.py
│   └── test_*.py
├── regression/
│   ├── __init__.py
│   └── test_*.py
├── integration/
│   ├── __init__.py
│   └── test_*.py
└── test_data/
    ├── configs/
    ├── responses/
    └── events/
```

**Rationale:** Hierarchical structure improves readability and organization for growing test suites while using industry-standard file naming within categories.

### 1.2 File Naming Convention

**Standard naming pattern:**

- All test files: `test_<component>.py`
- Examples:
  - `tests/regression/test_openai_provider.py`
  - `tests/integration/test_command_system.py`
  - `tests/development/test_new_feature.py`

**Benefits:** Industry-standard naming improves IDE support and developer familiarity while directory structure provides clear categorization.

## 2. Test Categorization System

### 2.1 Three-Tier System

**Development Tests** - Temporary validation during development:

- Purpose: Drive development of new features and validate work-in-progress
- Lifecycle: Remove after feature completion or convert to regression tests
- Location: `tests/development/`
- Decorator: `@development_test(phase=1)`

**Regression Tests** - Permanent functionality validation:

- Purpose: Prevent breaking changes to existing functionality
- Lifecycle: Maintain indefinitely
- Location: `tests/regression/`
- Decorator: `@regression_test`

**Integration Tests** - Component interaction validation:

- Purpose: Validate component interactions and end-to-end workflows
- Lifecycle: Maintain indefinitely
- Location: `tests/integration/`
- Decorator: `@integration_test(scope="component|service|end_to_end")`



### 2.2 Required Decorators

**Core Categorization:**

```python
@regression_test
def test_existing_functionality(self):
    pass

@integration_test(scope="component")
def test_component_interaction(self):
    pass

@integration_test(scope="service")
def test_external_service_integration(self):
    pass

@integration_test(scope="end_to_end")
def test_complete_workflow(self):
    pass

@development_test(phase=1)
def test_new_feature_development(self):
    pass
```

**Conditional Decorators:**

```python
@slow_test
def test_performance_intensive_operation(self):
    pass

@requires_api_key
def test_external_api_integration(self):
    pass

@requires_external_service("openai")
def test_openai_provider(self):
    pass

@skip_ci
def test_local_environment_only(self):
    pass
```

## 3. Modern Command-Line Interface

### 3.1 Clean CLI Design

**Inspired by Hatchling's successful patterns with modernization:**

```bash
# Category-based execution
python run_tests.py --development
python run_tests.py --regression  
python run_tests.py --integration

# Scope filtering for integration tests
python run_tests.py --integration --scope component
python run_tests.py --integration --scope service
python run_tests.py --integration --scope end_to_end

# Tag-based filtering (enhanced from Hatchling)
python run_tests.py --skip slow,requires_api_key
python run_tests.py --only regression,integration

# File and test targeting
python run_tests.py --file test_openai_provider.py
python run_tests.py --test test_valid_credentials_authenticate_successfully

# Output control
python run_tests.py --format pretty
python run_tests.py --format json --output results.json
python run_tests.py --verbose
```

### 3.2 Enhanced Discovery Engine

**Hierarchical Test Discovery:**

```python
def discover_tests(category=None, scope=None, file=None, test_name=None, 
                  skip_tags=None, only_tags=None):
    """Enhanced test discovery supporting hierarchical structure."""
    
    if file:
        return discover_specific_file(file, test_name)
    
    search_dirs = []
    if category:
        search_dirs = [tests_dir / category]
    else:
        search_dirs = [tests_dir / cat for cat in ['development', 'regression', 'integration']]
    
    suite = unittest.TestSuite()
    for search_dir in search_dirs:
        if search_dir.exists():
            discovered = loader.discover(str(search_dir), pattern='test_*.py')
            filtered = apply_tag_filters(discovered, skip_tags, only_tags, scope)
            suite.addTests(filtered)
    
    return suite
```

### 3.3 Backward Compatibility

**No backward compatibility** - clean break for better long-term maintainability:

- Remove support for old flag names (`--feature`, `--skip-slow`)
- Eliminate flat file naming patterns
- Focus on single, well-designed interface

## 4. Enhanced Developer Experience

### 4.1 Output Formatting

**Retain enhanced output formatting** (`test_output_formatter.py`) with these features:

- Status icons (✅❌⏭️💥) with color coding
- Category headers for clear test organization
- Detailed timing and metadata display
- Failure details with file locations and error context
- Adaptive terminal width handling

**Example Output:**

```plaintext
=== REGRESSION TESTS ===
test_openai_provider_initialization ..................... ✅ PASS (0.12s) [regression]
test_authentication_with_valid_credentials .............. ✅ PASS (0.08s) [regression]

=== INTEGRATION TESTS ===
test_end_to_end_chat_workflow
  Class: TestChatWorkflow
  Tags: @integration_test @requires_api_key @scope_end_to_end
  Duration: 4.23s ✅ PASS

=== TEST EXECUTION SUMMARY ===
Total Tests: 15   Passed: 14   Failed: 1   Skipped: 0
Total Duration: 12.45s   Average: 0.83s
```

### 4.2 Test Independence Guidelines

**Resource Management (from original guidelines):**

- Use context managers for automatic resource cleanup
- Create unique identifiers for temporary resources (timestamps, UUIDs)
- Clean up files, directories, and background processes in tearDown methods
- Mock time-sensitive operations to avoid race conditions

**Implementation Example:**

```python
class TestUserAuthentication(unittest.TestCase):
    def setUp(self):
        self.temp_dir = tempfile.mkdtemp(prefix=f"test_{uuid.uuid4().hex[:8]}_")
        self.mock_time = patch('time.time', return_value=1234567890)
        self.mock_time.start()
    
    def tearDown(self):
        shutil.rmtree(self.temp_dir, ignore_errors=True)
        self.mock_time.stop()
```

### 4.3 Mock vs Real Integration Strategy

**Decision Framework (from original guidelines):**

- **Unit tests**: Mock external dependencies (API calls, file system, network)
- **Integration tests**: Use real implementations when testing component interactions
- **Simple rule**: If testing single class/function logic → mock. If testing how components work together → real.

**Implementation Guidance:**

```python
# Unit test - mock external dependencies
@regression_test
def test_api_client_handles_timeout(self):
    with patch('requests.post') as mock_post:
        mock_post.side_effect = requests.Timeout()
        # Test timeout handling logic

# Integration test - use real implementations  
@integration_test(scope="service")
def test_openai_provider_with_real_api(self):
    # Test actual API integration with real OpenAI service
```

## 5. Test Data Management

### 5.1 Structured Test Data

**Directory Structure:**

```plaintext
tests/test_data/
├── configs/          # Test configuration files
├── responses/        # Mock API/tool responses
├── events/           # Sample event payloads
└── fixtures/         # Database and object fixtures
```

### 5.2 Data Access Utilities

**Standardized helper functions:**

```python
from tests.test_data_utils import load_test_config, load_mock_response

# Load test configuration
config = load_test_config("test_settings")

# Load mock response data
response = load_mock_response("api_success_responses")
```

## 6. Maintenance and Quality Standards

### 6.1 Test Maintenance Procedures

**Development Test Cleanup (from original guidelines):**

- Review development tests monthly
- Remove tests for completed features before merging
- Convert valuable development tests to regression tests

**Stale Test Detection:**

- Run automated detection for tests not modified in 90+ days
- Review flagged tests quarterly for relevance
- Update or remove outdated tests

### 6.2 Quality Requirements

**Coverage Standards:**

- Minimum coverage: 70% for all repositories
- Critical functionality: 90% coverage required
- New features: 95% coverage required

**Performance Standards:**

- Unit tests: <1 second per test
- Integration tests: <10 seconds per test
- Full CI test suite: <5 minutes execution time

### 6.3 Assertion Best Practices

**Descriptive assertions (from original guidelines):**

```python
# Good - descriptive assertion messages
self.assertEqual(result.status, "authenticated", 
                f"Authentication failed: expected 'authenticated', got '{result.status}'")

# Good - assert both state and side effects
self.assertTrue(user.is_authenticated)
self.assertIn("login_success", captured_events)
```

This standard provides a practical, modern testing architecture that solves real pain points while preserving proven organizational practices and maintaining focus on developer productivity.
