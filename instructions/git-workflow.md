# GIT WORKFLOW GUIDELINES

## CORE PRINCIPLES

### 1. Single Logical Change Per Commit

Each commit addresses exactly one logical change with clear rationale, enabling precise rollback capabilities and traceable development history.

### 2. Conventional Commit Format

Standardized commit messages for automated tooling integration and clear communication.

### 3. Development Narrative

Commit history tells a coherent story of development progress and decision-making.

---

## CONVENTIONAL COMMIT FORMAT

### Structure

```plaintext
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

- **feat**: New features (triggers minor version bump)
- **fix**: Bug fixes (triggers patch version bump)
- **docs**: Documentation changes
- **refactor**: Code refactoring without functional changes
- **test**: Adding or updating tests
- **chore**: Maintenance tasks, dependency updates
- **ci**: Changes to CI/CD configuration
- **perf**: Performance improvements
- **style**: Code style changes (formatting, etc.)

### Examples from Wobble Implementation

```plaintext
# Feature implementation
feat: add threaded file writer with queue-based operations
feat(cli): implement file output arguments with validation
feat: add observer pattern for multi-destination output

# Bug fixes
fix: resolve threading deadlock in file writer shutdown
fix: handle unittest _ErrorHolder objects gracefully
fix: prevent duplicate output in file logging

# Documentation
docs: update CLI reference with file output options
docs: add architecture overview for threading system
docs: enhance error message documentation

# Testing
test: add comprehensive threading and file I/O coverage
test: validate unicode symbol cross-platform compatibility
test: ensure proper resource cleanup in all scenarios

# Refactoring
refactor: extract observer pattern for output coordination
refactor: simplify unicode symbol handling logic
refactor: remove sys.path.insert statements from test files
```

---

## COMMIT STRATEGY PLANNING

### Before Starting Work

**1. Logical Change Identification**:

- Break down work into single-purpose changes
- Identify dependencies between changes
- Plan commit sequence for logical progression

**2. Rollback Strategy**:

- Ensure each commit can be safely reverted
- Avoid commits that break functionality
- Plan for partial rollback scenarios

**3. Message Planning**:

- Prepare clear, descriptive commit messages
- Identify scope and type for each change
- Plan body content for complex changes

### During Development

**1. Incremental Commits**:

- Commit frequently with small, focused changes
- Validate functionality after each commit
- Maintain working state at every commit

**2. Commit Message Quality**:

- Write clear, concise descriptions
- Explain the "why" not just the "what"
- Include context for future developers

**3. Scope Management**:

- Keep changes within defined scope
- Avoid mixing unrelated changes
- Create separate commits for different concerns

---

## REPOSITORY HYGIENE

### Branch Management

**Branch Naming**:

```plaintext
# Feature branches
feature/file-output-system
feature/threading-architecture

# Bug fix branches
fix/errorholder-compatibility
fix/duplicate-output-bug

# Documentation branches
docs/cli-reference-update
docs/architecture-overview
```

**Branch Strategy**:

- Create feature branches for significant changes
- Use descriptive branch names
- Keep branches focused on single features
- Regular rebase to maintain clean history

### Merge Strategy

**Merge Commit Messages**:

```plaintext
# Good merge messages
Merge pull request #123 from feature/file-output-system

feat: implement comprehensive file output system

- Add threaded file writer with queue-based operations
- Implement observer pattern for multi-destination output
- Add CLI arguments for file output configuration
- Include comprehensive test coverage and documentation

Resolves #456, #789
```

**Quality Checks**:

- All tests pass before merge
- Documentation updated for changes
- Code review completed
- No merge conflicts

### History Preservation

**Rebase vs Merge**:

- Use rebase for feature branches to maintain linear history
- Use merge commits for significant feature integration
- Preserve context through detailed merge messages
- Avoid force-pushing to shared branches

**Tag Creation**:

Handled by CI/CD pipelines based on commit content and branch rules.

---

## COMMIT MESSAGE BEST PRACTICES

### Description Guidelines

**Clear and Concise**:

```plaintext
# Good
feat: add threaded file writer with queue-based operations

# Avoid
feat: add some file stuff and fix things
```

**Imperative Mood**:

```plaintext
# Good
fix: resolve threading deadlock in file writer shutdown

# Avoid
fix: resolved threading deadlock in file writer shutdown
```

**Specific and Actionable**:

```plaintext
# Good
refactor: extract observer pattern for output coordination

# Avoid
refactor: improve code structure
```

### Body Content

**When to Include Body**:

- Complex changes requiring explanation
- Breaking changes with migration notes
- Context for future developers
- References to issues or discussions

**Body Structure**:

```plaintext
feat: implement comprehensive file output system

Add threaded file writer using queue-based operations to enable
non-blocking file I/O during test execution. Implements observer
pattern for coordinating output between console and file destinations.

Key components:
- ThreadedFileWriter: Background file operations with graceful shutdown
- OutputObserver: Multi-destination output coordination
- CLI integration: Complete argument parsing and validation

Resolves #456: File output feature request
Addresses #789: Performance concerns with blocking I/O
```

### Footer Guidelines

**Breaking Changes**:

```plaintext
feat!: change file output API interface

BREAKING CHANGE: File output configuration now uses observer pattern
instead of direct formatter calls. Update existing integrations to use
new OutputObserver interface.

Migration guide: docs/migration/file-output-v2.md
```

**Issue References**:

```plaintext
fix: handle unittest _ErrorHolder objects gracefully

Resolves #123
Fixes #456
Closes #789
```

---

## QUALITY ASSURANCE

### Pre-Commit Checklist

- [ ] Single logical change
- [ ] Clear, descriptive commit message
- [ ] Conventional commit format
- [ ] All tests pass
- [ ] No unrelated changes included
- [ ] Documentation updated if needed

### Commit Review Process

- Review commit message for clarity
- Verify change scope is appropriate
- Ensure rollback capability
- Check for conventional format compliance

### History Validation

- Commit history tells coherent story
- Each commit builds logically on previous
- No broken states in commit history
- Clear progression toward objectives

---

## AGENT OPTIMIZATION

### For AI Coding Agents

- **Context Understanding**: Focused commits provide clear context for future work
- **Change Tracking**: Conventional format enables automated analysis
- **Rollback Capability**: Single-purpose commits enable precise rollback
- **Development Narrative**: Clear history helps understand decision progression

### For Human Developers

- **Code Review**: Focused commits make review more effective
- **Debugging**: Clear history helps identify when issues were introduced
- **Knowledge Transfer**: Commit messages provide context for decisions
- **Maintenance**: Logical changes make future modifications easier

---

## SUCCESS METRICS

### Quality Indicators

- Each commit can be understood independently
- Rollback of any commit doesn't break functionality
- Commit history tells clear development story
- Automated tooling can parse commit messages

### Wobble Implementation Evidence

- ✅ 18+ focused commits with clear development narrative
- ✅ Conventional commit format for automated tooling
- ✅ Precise rollback capabilities for each change
- ✅ Clear progression from initial implementation to production

**Last Updated**: Based on Wobble implementation success (2024)
