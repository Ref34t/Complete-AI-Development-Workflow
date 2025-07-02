# AI-Powered Development Workflow

Automated development pipeline using ChatGPT → Taskmaster → Claude Code → CodeRabbit.

## Workflow Overview

1. **PRD Creation**: Create a detailed Product Requirements Document using ChatGPT
2. **Task Breakdown**: Automatically break down PRD into structured development tasks
3. **Implementation**: Claude Code implements features based on structured tasks
4. **Code Review**: CodeRabbit provides automated code review and quality checks

## Getting Started

### 1. Create a PRD
- Go to Issues → New Issue
- Select "Product Requirements Document (PRD)" template
- Fill out all required fields
- Add `prd` label to trigger workflow

### 2. Automatic Task Creation
- The workflow will automatically parse your PRD
- Creates individual development tasks in your project management tool
- Tasks are labeled `ready-for-dev` when ready for implementation

### 3. Implementation
- Tasks trigger Claude Code sessions for implementation
- Code is committed to feature branches
- Pull requests are created automatically

### 4. Review Process
- CodeRabbit automatically reviews all pull requests
- Provides feedback on code quality, security, and best practices
- Workflow updates task status based on review results

## Configuration

### Required Secrets
Add these to your repository secrets:

- `OPENAI_API_KEY` - For ChatGPT integration
- `ANTHROPIC_API_KEY` - For Claude Code
- `GITHUB_TOKEN` - For repository access (auto-provided)

### Labels Used
- `prd` - Marks issues as Product Requirements Documents
- `needs-breakdown` - PRD needs to be broken down into tasks
- `task` - Individual development task
- `ready-for-dev` - Task ready for implementation
- `in-progress` - Task currently being worked on
- `review-ready` - Code ready for review

## Workflow Triggers

- **New PRD Issue**: Triggers task breakdown
- **Task Ready**: Triggers implementation
- **Pull Request**: Triggers code review
- **Manual**: Use workflow_dispatch for manual triggers

## File Structure

```
.github/
├── workflows/
│   └── dev-pipeline.yml    # Main workflow automation
└── ISSUE_TEMPLATE/
    ├── prd.yml            # PRD template
    └── task.yml           # Task template
```