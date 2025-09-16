---
type: "always_apply"
---

# Report Creation Instructions

## Overview
When a user requests a report, create high-quality markdown reports following the structured guidelines below.

## Default Report Location
Unless explicitly specified otherwise, save all reports to:
```
<workspace_root>/Laghari/<coding_agent_software>/<project_name>/<topic>/<sub_topic>/<descriptive_filename>_v<version>.md
```

### Versioning
User will likely ask you to iterate over your analysis and refine reports. If a new report is the update of a previous one, increment the version number by 1.
Versioning can simply be a single number starting from `0`: <descriptive_filename>_v0.md --> <descriptive_filename>_v1.md --> <descriptive_filename>_v2.md --> and so on...

## Path Components Explained
- **`<repository_root>`**: The root directory of the current repository/workspace
- **`<topic_name>`**: A clear, descriptive folder name related to the report's subject matter
- **`<descriptive_filename>.md`**: A meaningful filename that clearly indicates the report's content

## Directory Creation Rules
- **Auto-create missing directories**: Create the relevant report's project, topic, or sub-topic directory if they don't exist
- **Session organization**: Keep all files from a single work session within the same topic directory for clarity
- **Naming conventions**: 
  - Use snake_case for directory and file names
  - Avoid spaces and special characters
  - Make names descriptive and self-explanatory

## Report Quality Standards
- Use proper markdown formatting
- Include clear headings and structure
- Add table of contents for longer reports
- Use code blocks, tables, and lists appropriately
- Ensure content is well-organized and readable

## Example Structure
```
project_root/
└── Laghari/ #implementation records
    └── <coding agent software>/ #e.g. Augment, VS Code, Zed, Cursor
        └── project/ #e.g. repository name (Wobble, Hatch, Hatchling)
            └── topic/ #e.g. feature_XXX, research_XXX, refactor_XXX
                └── subtopic/ #e.g. fix_AAA, refactor_BBB, document_CCC
```

## Implementation Notes
- Always confirm the repository root before creating paths
- Group related reports under the same topic directory
- Use consistent naming patterns within each topic folder