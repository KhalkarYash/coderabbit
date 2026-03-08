# CodeRabbit Baseline Config

This repository stores a reusable `.coderabbit.yaml` so you can apply the same CodeRabbit review behavior across future repositories.

## Current config (source of truth)

```yaml
# yaml-language-server: $schema=https://coderabbit.ai/integrations/schema.v2.json
language: "en"

early_access: false

reviews:
  profile: "assertive"
  request_changes_workflow: true
  high_level_summary: true
  poem: false
  review_status: true
  review_details: true
  collapse_walkthrough: false
  path_filters:
    - "!**/*.xml"
  path_instructions:
    - path: "**/*.js"
      instructions: "Review the JavaScript code for conformity with the Google JavaScript style guide, highlighting any deviations."
    - path: "**/*.ts"
      instructions: |
        Review the TypeScript code for conformity with best practices, highlighting any deviations. Ensure that:
        - The code adheres to best practices associated with Node.js.
        - The code adheres to best practices recommended for performance.
        - The code adheres to similar naming conventions for controllers, models, services, methods, variables.
  auto_review:
    enabled: true
    ignore_title_keywords:
      - "WIP"
      - "DO NOT MERGE"
    drafts: false
    base_branches:
      - "master"
      - "main"

chat:
  auto_reply: true
```

## What this currently enables

- Enables automatic PR review for non-draft PRs.
- Skips auto-review for PR titles containing `WIP` or `DO NOT MERGE`.
- Runs auto-reviews for PRs targeting `master` and `main`.
- Keeps review tone `assertive` for actionable details.
- Enables request-changes workflow for clearer merge gates.
- Keeps high-level summaries and review status updates on.
- Keeps detailed review output and walkthrough expansion behavior explicit.
- Applies review path filtering to exclude `*.xml` files.
- Adds file-type-specific review guidance:
- `**/*.js`: check against Google JavaScript style guide.
- `**/*.ts`: enforce TypeScript, Node.js, performance, and naming best practices.
- Disables poem output so feedback stays focused.
- Enables chat auto-replies.
- Uses `en` for review language.
- Keeps `early_access` disabled.

## Use in a new repository

Run this in the target repository root:

```bash
curl -fsSL https://raw.githubusercontent.com/KhalkarYash/coderabbit/main/.coderabbit.yaml -o .coderabbit.yaml
git add .coderabbit.yaml
git commit -m "chore: add baseline CodeRabbit config"
git push
```

## Keep repositories in sync

When you update this baseline file, pull the latest version into any repo using the same `curl` command and commit the change.

## Optional: apply to many repositories

If you want to roll this out to multiple repos, use GitHub CLI with a small script to copy this file and open PRs in bulk.
If you want, I can generate that script next.
