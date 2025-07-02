# Integrating AI Workflow into Existing Projects

## Quick Setup for Existing Projects

### 1. Copy Workflow Files to Your Project

```bash
# In your existing project directory
mkdir -p .github/workflows .github/ISSUE_TEMPLATE

# Copy workflow files
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/workflows/dev-pipeline.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/workflows/testing-pipeline.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/workflows/mcp-setup.yml

# Copy issue templates
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/ISSUE_TEMPLATE/idea.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/ISSUE_TEMPLATE/prd.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/ISSUE_TEMPLATE/task.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/ISSUE_TEMPLATE/ui-task.yml
curl -O https://raw.githubusercontent.com/[your-repo]/dev-workflow/main/.github/ISSUE_TEMPLATE/testing-task.yml
```

### 2. One-Command Setup Script

```bash
#!/bin/bash
# setup-ai-workflow.sh

echo "🚀 Setting up AI-powered development workflow for existing project"

# Create necessary directories
mkdir -p .github/workflows .github/ISSUE_TEMPLATE .mcp .context7

# Setup MCP configuration
cat > .mcp/config.json << 'EOF'
{
  "mcpServers": {
    "magic-ui": {
      "command": "magic-mcp",
      "args": ["--project-name", "${PWD##*/}"],
      "env": {
        "MAGIC_MCP_PORT": "3000"
      }
    },
    "browser-automation": {
      "command": "browsermcp",
      "args": ["--headless", "--port", "3001"],
      "env": {
        "BROWSER_MCP_PORT": "3001",
        "BROWSER_MCP_HEADLESS": "true"
      }
    },
    "context7": {
      "command": "context7",
      "args": ["--port", "3002"],
      "env": {
        "CONTEXT7_PORT": "3002",
        "CONTEXT7_MAX_TOKENS": "200000"
      }
    }
  }
}
EOF

# Setup Context7 for existing codebase
cat > .context7/config.json << 'EOF'
{
  "provider": "upstash",
  "contextWindow": 200000,
  "chunkSize": 8000,
  "overlap": 400,
  "existingProject": true,
  "scanPatterns": [
    "**/*.js",
    "**/*.ts",
    "**/*.jsx",
    "**/*.tsx",
    "**/*.py",
    "**/*.java",
    "**/*.go",
    "**/*.rs",
    "**/*.php",
    "**/*.rb",
    "**/*.vue",
    "**/*.svelte",
    "README.md",
    "package.json",
    "requirements.txt"
  ],
  "ignorePatterns": [
    "node_modules/**",
    ".git/**",
    "dist/**",
    "build/**",
    "*.log"
  ],
  "embedding": {
    "model": "text-embedding-3-small",
    "dimensions": 1536
  },
  "retrieval": {
    "topK": 15,
    "threshold": 0.7
  }
}
EOF

echo "✅ AI workflow setup complete!"
echo "📝 Next steps:"
echo "1. Push these changes to GitHub"
echo "2. Enable GitHub Actions in repository settings"
echo "3. Create your first enhancement issue using the templates"
```

### 3. Adapting to Your Tech Stack

#### For React/Next.js Projects
```yaml
# Add to .github/workflows/dev-pipeline.yml
- name: Setup React Environment
  run: |
    npm install
    npm run build || echo "Build step optional for setup"
    
- name: Configure Magic MCP for React
  run: |
    magic-mcp --framework react --project-name "${{ github.repository }}"
```

#### For Python/Django Projects
```yaml
# Add to .github/workflows/dev-pipeline.yml  
- name: Setup Python Environment
  uses: actions/setup-python@v4
  with:
    python-version: '3.9'
    
- name: Install Dependencies
  run: |
    pip install -r requirements.txt
    pip install playwright pytest
```

#### For PHP/Laravel Projects
```yaml
# Add to .github/workflows/dev-pipeline.yml
- name: Setup PHP Environment
  uses: shivammathur/setup-php@v2
  with:
    php-version: '8.1'
    
- name: Install Composer Dependencies
  run: composer install
```

## 4. Usage Patterns for Existing Projects

### Enhancement Workflow
```markdown
Instead of creating new features manually:

1. Create "Project Idea" issue: "Add user dashboard analytics"
2. Claude Code generates comprehensive PRD
3. Workflow breaks down into tasks:
   - Backend API endpoints
   - Frontend dashboard components  
   - Database migrations
   - Testing automation
4. Each task implemented automatically
5. Full testing and review process
```

### Bug Fix Workflow
```markdown
For existing bugs:

1. Create "Testing Task" issue: "Fix user authentication bug"
2. BrowserMCP reproduces the bug
3. Context7 analyzes existing codebase for related code
4. Claude Code implements fix with comprehensive testing
5. Automated validation ensures fix works
```

### Refactoring Workflow
```markdown
For code improvements:

1. Create "Task" issue: "Refactor legacy payment system"
2. Context7 analyzes entire payment codebase
3. Claude Code creates refactoring plan
4. Magic MCP updates UI components if needed
5. BrowserMCP validates all payment flows still work
```

## 5. Gradual Integration Strategy

### Phase 1: Testing Only (Low Risk)
- Add only testing workflows
- Use BrowserMCP for automated testing
- No changes to main development process

### Phase 2: Enhancement Features (Medium Risk)  
- Use workflow for new features only
- Keep existing development for critical fixes
- Build confidence with non-critical additions

### Phase 3: Full Integration (High Value)
- Use workflow for all development tasks
- Leverage Context7 for large codebase navigation
- Magic MCP for all UI work

## 6. Team Onboarding

### For Developers
```markdown
1. Workflow handles routine tasks automatically
2. Focus on architecture and complex problem-solving
3. Review AI-generated code and provide feedback
4. Use issue templates for consistent task creation
```

### For Project Managers
```markdown
1. Create comprehensive PRDs using simple idea descriptions
2. Automatic task breakdown with effort estimates
3. Real-time progress tracking via GitHub Projects
4. Automated testing reduces QA overhead
```

### For QA Teams
```markdown
1. BrowserMCP handles repetitive testing automatically
2. Focus on edge cases and user experience
3. Automated accessibility and performance testing
4. Comprehensive test coverage reports
```

## 7. Migration Checklist

- [ ] Copy workflow files to `.github/` directory
- [ ] Setup MCP configuration in `.mcp/` directory
- [ ] Configure Context7 for existing codebase in `.context7/`
- [ ] Enable GitHub Actions in repository settings
- [ ] Create first test issue using templates
- [ ] Train team on new issue templates and workflow
- [ ] Gradually migrate existing backlog to new workflow
- [ ] Monitor and optimize workflow performance

## 8. Rollback Plan

If you need to disable the workflow:
```bash
# Disable workflows
mv .github/workflows .github/workflows.disabled

# Keep issue templates for manual use
# MCP configurations remain for local development
```

The beauty of this system is it **enhances** your existing project without replacing your current development process!