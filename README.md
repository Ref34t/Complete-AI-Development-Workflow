# AI-Powered Development Workflow

Automated development pipeline using Claude Code → Taskmaster → Claude Code → CodeRabbit.

## Workflow Overview

1. **Idea to PRD**: Claude Code creates comprehensive PRD from simple project ideas
2. **Task Breakdown**: Automatically break down PRD into structured development tasks (GitHub Projects)
3. **Implementation**: Claude Code implements features based on structured tasks
4. **UI Enhancement**: Magic MCP provides advanced UI generation for frontend tasks
5. **Testing & Automation**: BrowserMCP handles web automation and comprehensive testing
6. **Enhanced Context**: Context7 manages large codebase context and intelligent retrieval
7. **Code Review**: CodeRabbit provides automated code review and quality checks

## Getting Started

### 1. Submit Project Idea
- Go to Issues → New Issue
- Select "Project Idea" template
- Describe your basic idea (just a few sentences)
- Add `idea` label to trigger Claude Code PRD creation

### 2. Claude Code Creates PRD
- Workflow automatically generates comprehensive PRD
- Includes user stories, technical requirements, acceptance criteria
- Creates new issue with `prd` label

### 3. Automatic Task Creation
- The workflow will automatically parse your PRD
- Creates individual development tasks in your project management tool
- Tasks are labeled `ready-for-dev` when ready for implementation

### 4. Implementation
- Tasks trigger Claude Code sessions for implementation
- Code is committed to feature branches
- Pull requests are created automatically

### 5. Review Process
- CodeRabbit automatically reviews all pull requests
- Provides feedback on code quality, security, and best practices
- Workflow updates task status based on review results

## Configuration

### Required Secrets
No API keys needed! The workflow uses:

- `GITHUB_TOKEN` - For repository access (auto-provided by GitHub)
- **Claude Code CLI** - Uses your existing Claude subscription

### Setup Steps
1. **Push to GitHub**: Create repository and push this code
2. **Enable Actions**: Ensure GitHub Actions are enabled  
3. **Test Workflow**: Create a test project idea issue

### Benefits of Full MCP Integration
- ✅ **No API costs** - Uses your existing Claude subscription
- ✅ **No rate limits** - Full access to Claude capabilities
- ✅ **Interactive sessions** - Claude can ask clarifying questions
- ✅ **File system access** - Can read/write project files directly
- ✅ **Advanced UI generation** - Magic MCP enhances frontend development
- ✅ **Responsive design** - Automatic mobile-first layouts
- ✅ **Accessibility built-in** - WCAG compliant components
- ✅ **Web automation** - BrowserMCP for comprehensive testing
- ✅ **Enhanced context** - Context7 for large codebase management
- ✅ **Cross-browser testing** - Automated compatibility validation
- ✅ **Performance monitoring** - Built-in performance benchmarking

### Labels Used
- `idea` - Initial project ideas for PRD creation
- `needs-prd` - Idea ready for Claude Code to create PRD
- `prd` - Marks issues as Product Requirements Documents
- `needs-breakdown` - PRD needs to be broken down into tasks
- `task` - Individual development task
- `ui-task` - UI/UX development task (uses Magic MCP)
- `test-task` - Testing/automation task (uses BrowserMCP)
- `needs-mcp` - Task requires Magic MCP for UI generation
- `needs-browser-mcp` - Task requires BrowserMCP for testing
- `ready-for-dev` - Task ready for implementation
- `in-progress` - Task currently being worked on
- `review-ready` - Code ready for review

## Workflow Triggers

- **New Idea Issue**: Triggers Claude Code PRD creation
- **New PRD Issue**: Triggers task breakdown
- **Task Ready**: Triggers standard implementation
- **UI Task Ready**: Triggers Magic MCP enhanced implementation
- **Test Task Ready**: Triggers BrowserMCP testing automation
- **Pull Request**: Triggers automated testing + code review
- **Manual**: Use workflow_dispatch for manual triggers

## File Structure

```
.github/
├── workflows/
│   └── dev-pipeline.yml    # Main workflow automation
└── ISSUE_TEMPLATE/
    ├── idea.yml           # Project idea template
    ├── prd.yml            # PRD template
    ├── task.yml           # Task template
    ├── ui-task.yml        # UI development task template
    └── testing-task.yml   # Testing & automation task template
```