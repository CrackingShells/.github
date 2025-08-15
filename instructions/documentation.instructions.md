---
applyTo: 'docs/**/*.md'
description: 'Documentation style guide for markdown files in the docs directory.'
---

# Documentation Instructions for `docs/**/*.md`

## Style Guide
- Use Markdown format for all documentation files.
- It is absolutely critical that documentation is focused.

### Tone

- Maintain focused professionalism and technical clarity throughout.
- Use warmth or engagement only at crucial junctions (e.g., transitions, summaries, or onboarding moments), not as a default.
- Be humble and educational.

### Compelling Conciseness
- Documentation is the readable front-end description of the project. It must be pleasant to read to keep users hooked and focused. There is a sweet spot between dryness of technical writing and engaging writing.
-  Use precise paragraphs that tell the reader exactly what they need to know about topics.
- Apply DRY (Don't Repeat Yourself) principles:
  - Avoid repeating information.
  - Rely on cross linking all the documentation.
  - Merge similar articles to reduce redundancy.
- Avoid explanations or recommendations that do not stem from the project.

### Language
- Use plain, neutral language.
- Avoid subjective statements or recommendations.
- Prefer present tense and active voice.

### Audience
- Main articles are for all users, but assume some technical background.
- Direct beginners to appendices for foundational concepts.

## Structure

```
docs/
├── articles/
│   ├── devs/
│   │   ├── dev_table_of_contents.md
│   │   ├── <a_single_topic_1>.md
│   │   ├── contribution_guides/
│   │   │   ├── <large_contribution_topic_1>/
│   │   │   │   ├── <part_1>.md
│   │   │   │   └── <part_2>.md
│   │   │   └── <a_single_contribution_guide>.md
│   │   └── <a_single_topic_2>.md
│   ├── users/
│   │   ├── user_table_of_contents.md
│   │   ├── GettingStarted.md
│   │   ├── tutorials/
│   │   │   ├── Topic1/
│   │   │   │   ├── <tutorial_step1>.md
│   │   │   │   └── <tutorial_step2>.md
│   │   │   └── Topic2/
│   │   │       └── <tutorial_a_unique_file_if_short>.md
│   │   ├── <article_name>.md
│   │   ├── <other_user_articles>.md
│   │   ├── Feature1/
│   │   │   ├── <article_name1>.md
│   │   │   └── <article_name2>.md
│   │   └── Feature2/
│   │       └── <article_name>.md
│   └── appendices/
│       ├── glossary.md
│       └── <other_appendix_articles>.md
└── resources/
    ├── diagrams/
    │   └── <diagram_name>.puml
    └── images/
        ├── <image_name>.png
        └── <other_resources>.jpg
```

### Articles

#### General Guidelines

- Introduce technical articles with the content it covers:
  """
  This article is about:
  - <short list of concepts discussed>
  """
- Each article should focus on a single topic or feature.
- Use headings for logical organization.
- Use code snippets to illustrate points or provide examples.
- Reference resources (images, diagrams) to support text.
- Do not repeat information from code docstrings—link or refer to code as needed.

#### Details

- Divide articles into two main categories:
  - `devs`: For maintainers and code contributors.
      - Contribution guidelines.
        - How to contribute (issues, pull requests, etc.).
        - How to run tests, build the project, and deploy.
      - Code structure and architecture.
        - What directories and/or files are present in the codebase.
        - Design patterns used, where, for what gains.
          - Extensive use of diagrams is encouraged.
      - CI and CD processes.
        - How the CI/CD is set up.
        - What tools are used (e.g., GitHub Actions)
        - Description of the CI/CD pipeline.
          - Extensive use of diagrams is encouraged.

  - `users`: For API/product consumers.
    - Place tutorials in a `users/tutorials/` subcategory.
      - Each tutorial should be a step-by-step guide for users.
      - The tutorial steps should be split into multiple articles if they are too long.
        - In that case, group them by topic (e.g., `Topic1/`, `Topic2/`).
        - In that case, add links at the top and bottom of each article to navigate to the previous and next steps.
      - Beginner-friendly
      - Extensive references to the glossery and appendices is encouraged.
    - Place articles in a `users/` subcategory.
      - Each article should be focused on a specific topic or feature.
      - Use subcategories for related articles (e.g., `RelevantCategoryForTheProduct/`).
      - Use subcategories for different products (e.g., `AnotherCategoryForTheProduct/`).

### Appendices
A table of contents is required for appendices that will link every article in the appendices folder.

- Place supplementary information that supports the main articles here.
- Place beginner resources, glossary, and low-level explanations in `docs/article/appendices/`.
- Use this folder for:
  - Glossary of terms (e.g., "distro", "terminal", etc.) in alphabetical order, separated in sections of first letter.
  - Step-by-step guides for basic tasks (e.g., opening a terminal on Windows/Mac).
  - Any content that would otherwise clutter the main articles.

### Resources
- Store all images, diagrams, and non-markdown assets in `docs/resources/`.
- Reference resources in articles and appendices using relative paths.

#### About diagrams
- Write plantuml diagrams in `docs/resources/diagrams/`.
- Use the `@startuml` and `@enduml` tags to define diagrams.
  - For class diagrams, use web fetch action to get the content of https://plantuml.com/en/class-diagram
  - For sequence diagrams, use web fetch action to get the content of https://plantuml.com/en/sequence-diagram
