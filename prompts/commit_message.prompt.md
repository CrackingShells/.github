---
mode: agent
tools: ['changes', 'codebase', 'findTestFiles', 'search', 'searchResults', 'usages']
---

## Commit Message Instructions
Concise one liners about the changes made in the codebase.
Use the files given in context to determine the changes made.

## Format
### Template
[<Modification Type> - <Level>] Very short description of the changes made.

**Major**:
- <List major changes here, one per line>

**Minor**:
- <List minor changes here, one per line>

### About Modification Type

Modification Type can be one of the following:
- **Update**: For changes that on existing codebase.
- **Add**: For changes that introduce new features, functionality, or files.
- **Fix**: For changes that resolve bugs or issues.
- **Remove**: For changes that remove features, functionality, or files.
- **Refactor**: For changes that improve code structure or readability without changing functionality.
- **Docs**: For changes that update documentation.
- **Test**: For changes that add or modify tests.

Sometimes a commit may not fit neatly into one of these categories, in which case you can chose to use the one that best fits the majority of the changes.

### About Level

Level can be one of the following:
- **Major**: For changes that introduce very significant new features or breaking changes.
- **Minor**: For very small changes that do not significantly alter functionality or structure.
- Or simply nothing if it is neither of these extremes.

