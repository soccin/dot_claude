---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(subl:*)
description: Draft commit message
---
# Claude Command: Commit

This command helps you create well-formatted commits with conventional commit message conventions.

## Usage

To create a draft commit, just type:
```
/draft-commit
```

## What This Command Does

3. Performs a `git diff --staged` to understand what changes are being committed

## Context

- Current git status: !`git status`
- Current git diff (staged files ONLY!!): !`git diff --staged`

## Your task

Based on the above changes:

1. Checks which files are staged with `git status`
2. If 0 files are staged, tell the user and stop!
3. Create a draft of an appropriate commit message following the instructions below
4. Save this message in a markdown file (commit_message.md)
5. Use the command `subl -nw` to allow me to edit the commit message.
6. Once I have saved the changes do the commit with the editted message
7. DELETE the temporary commit message file
8. You have the capability to call multiple tools in a single response. You MUST do all of the above in a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.

## Commit Message Generation

Summarize the diffs into a clear and concisely written commit message. Use the imperative style for the subject, use Conventional Commits (type and optionally scope), and limit the subject+type+scope to 50 characters or less. Be as descriptive as possible in the unlimited length body. Please wrap the text in the main body to roughly 60 character long lines.

### Specific rules

When generating commit messages for this project:
- Use conventional commit format: `type(scope): description`
- Common types: feat, fix, docs, style, refactor, test, chore
- Description should be concise but descriptive
- Include reference to specific files or modules when relevant
- At the end of the commit message add the text: `Co-Authored-By: Claude`

### Examples of good commit messages:
```
fix: resolve memory allocation issue in QC module

#claude
```

```
feat: Update Phase II and III pipeline scripts

- Add symbolic link creation for Final directory in Phase II
- Update LSF job configuration in Phase III (fix job name and output directory)
- Submit UMAP processing as LSF job instead of running directly

Co-Authored-By: Claude
```

```
chore(conf): update LSF resource parameters for better performace
```

```
docs(tempo): update output documentation for v1.0.4

Integrate changes to pipeline since v1.0.3 to the output
documentation.

Co-Authored-By: Claude
```
