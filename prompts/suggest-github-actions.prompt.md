---
agent: 'agent'
description: 'Suggest relevant GitHub Actions from awesome-actions resources based on repository tech stack and existing workflows, identifying automation gaps and improvement opportunities.'
tools: ['edit', 'search', 'runCommands', 'runTasks', 'think', 'changes', 'testFailure', 'openSimpleBrowser', 'fetch', 'githubRepo', 'todos', 'search']
---
# Suggest GitHub Actions

Analyze current repository context, tech stack, and existing workflows to suggest relevant GitHub Actions from [awesome-actions](https://github.com/sdras/awesome-actions) that are not already installed, identifying automation gaps and improvement opportunities.

## Process

1. **Analyze Tech Stack**: Scan repository to identify programming languages (JS, Python, C#, Java, Go, etc.), frameworks (React, ASP.NET, Spring Boot, Django, etc.), and project types (web apps, APIs, libraries, CLIs)
2. **Scan Existing Workflows**: Audit `.github/workflows/` directory to identify currently installed workflows and their purposes (CI, CD, testing, security, dependency management)
3. **Fetch Awesome Actions**: Extract action categories and recommendations from [sdras/awesome-actions](https://github.com/sdras/awesome-actions). Must use `#fetch` tool to retrieve the README content
4. **Identify Automation Needs**: Based on tech stack, determine common automation requirements:
   - Language-specific CI/CD (build, test, lint)
   - Security scanning (CodeQL, dependency scanning, secret scanning)
   - Dependency management (Dependabot alternatives, automated updates)
   - Code quality (linting, formatting, coverage)
   - Deployment pipelines
   - Documentation generation
   - Release management
5. **Gap Analysis**: Compare available actions from awesome-actions against:
   - Current repository tech stack requirements
   - Existing installed workflows
   - Industry best practices for the detected technologies
   - Security and compliance needs
6. **Match Relevance**: Filter and prioritize actions based on:
   - Technology stack compatibility
   - Workflow coverage gaps
   - Security and quality improvements
   - Development workflow enhancements
7. **Present Options**: Display relevant actions with descriptions, installation status, and rationale
8. **Validate**: Ensure suggested actions would add measurable value not already covered by existing workflows
9. **Output**: Provide structured table with action suggestions, descriptions, installation status, and recommendation rationale
   **AWAIT** user request to proceed with installation of specific action. DO NOT INSTALL UNLESS DIRECTED TO DO SO.
10. **Generate Workflow**: For requested actions, provide a complete workflow YAML file blueprint that can be added to `.github/workflows/` folder. Include:
    - Workflow file name suggestion
    - Complete YAML configuration
    - Trigger configuration recommendations
    - Required secrets/variables documentation
    - Usage instructions

## Context Analysis Criteria

🔍 **Repository Tech Stack Detection**:
- **Languages**: Detect via file extensions (.js, .ts, .py, .cs, .java, .go, .rb, .php, etc.)
- **Package Managers**: Identify via config files (package.json, requirements.txt, *.csproj, pom.xml, go.mod, Gemfile, composer.json)
- **Frameworks**: Detect via dependencies and config files (React, Vue, Angular, ASP.NET, Django, Flask, Spring Boot, Express, Next.js)
- **Build Tools**: Identify build systems (npm, yarn, pnpm, Maven, Gradle, MSBuild, Make, CMake)
- **Testing Frameworks**: Detect test infrastructure (Jest, Mocha, pytest, NUnit, xUnit, JUnit, RSpec)

🔧 **Workflow Coverage Analysis**:
- **CI/CD**: Build, test, lint pipelines
- **Security**: CodeQL analysis, dependency scanning, container scanning, secret detection
- **Quality**: Code coverage, performance benchmarks, accessibility testing
- **Dependencies**: Automated updates, vulnerability scanning, license checking
- **Deployment**: Staging, production, preview environments
- **Documentation**: API docs generation, changelog automation
- **Release**: Semantic versioning, automated releases, changelog generation

🎯 **Common Automation Gaps**:
- Missing CI for detected languages/frameworks
- No security scanning (CodeQL, Dependabot, Snyk)
- No automated dependency updates
- Missing code quality checks (linting, formatting, coverage)
- No automated testing on PRs
- Missing deployment automation
- No release management automation
- Missing documentation automation

## Output Format

Display analysis results in structured table:

| Suggested Action | Description | Already Installed | Rationale |
|------------------|-------------|-------------------|-----------|
| [actions/setup-node](https://github.com/actions/setup-node) | Set up Node.js environment for builds and tests | ❌ No | Repository contains package.json but no Node.js CI workflow detected |
| [github/codeql-action](https://github.com/github/codeql-action) | Advanced security scanning for code vulnerabilities | ❌ No | No security scanning workflow detected; recommended for all repositories |
| [actions/setup-python](https://github.com/actions/setup-python) | Set up Python environment | ✅ Yes | Already configured in `ci.yml` workflow |
| [codecov/codecov-action](https://github.com/codecov/codecov-action) | Upload code coverage reports | ❌ No | Test infrastructure detected but no coverage reporting configured |
| [dependabot[bot]](https://docs.github.com/en/code-security/dependabot) | Automated dependency updates | ❌ No | Multiple package managers detected; would improve security posture |

## Tech Stack Detection Process

1. **Language Detection**:
   - Scan repository root and subdirectories for source files
   - Count files by extension to identify primary and secondary languages
   - Build language profile (e.g., "Primary: TypeScript, Secondary: Python")

2. **Framework Detection**:
   - Read package.json dependencies for Node.js frameworks
   - Read requirements.txt or setup.py for Python frameworks
   - Read *.csproj for .NET frameworks
   - Read pom.xml or build.gradle for Java frameworks
   - Identify web frameworks, testing frameworks, and build tools

3. **Project Type Classification**:
   - Web application (frontend/backend)
   - Library/package
   - CLI tool
   - API/service
   - Documentation site
   - Infrastructure/tooling

## Existing Workflows Discovery Process

1. **Scan Workflows Directory**: List all `*.yml` and `*.yaml` files in `.github/workflows/`
2. **Parse Workflow Files**: Extract key information:
   - Workflow name and purpose
   - Trigger events (push, pull_request, schedule, etc.)
   - Jobs and steps
   - Actions used
   - Languages/tools involved
3. **Categorize Workflows**: Group by purpose:
   - CI (continuous integration)
   - CD (continuous deployment)
   - Security scanning
   - Dependency management
   - Code quality
   - Documentation
   - Release automation
4. **Build Coverage Matrix**: Map what's currently automated vs. what's missing

## Awesome Actions Categories

Focus on these key categories from awesome-actions:

- **Official Actions**: Core actions by GitHub (setup-*, checkout, upload-artifact, etc.)
- **Utility Actions**: General-purpose automation (labeling, commenting, notifications)
- **CI/CD Actions**: Language-specific build and test actions
- **Security Actions**: CodeQL, dependency scanning, container scanning
- **Deployment Actions**: Cloud deployments (Azure, AWS, GCP), container registries
- **Code Quality**: Linting, formatting, coverage reporting
- **Dependency Management**: Automated updates, vulnerability scanning
- **Release Management**: Semantic release, changelog generation, version bumping
- **Notifications**: Slack, Discord, Teams, email notifications

## Requirements

- Use `fetch` tool to get content from awesome-actions repository (https://github.com/sdras/awesome-actions)
- Scan local file system for repository structure and tech stack indicators
- Audit `.github/workflows/` directory for existing workflows
- Parse existing workflow files to understand current automation coverage
- Analyze repository files to detect languages, frameworks, and build tools
- Cross-reference detected tech stack with awesome-actions recommendations
- Identify gaps where automation is missing or could be improved
- Focus on high-value additions (security, quality, efficiency)
- Validate that suggested actions align with repository's tech stack
- Provide clear, actionable rationale for each suggestion
- Include links to action repositories and documentation
- Prioritize security and quality improvements
- Don't provide any additional information or context beyond the table and the analysis

## Installation Workflow Blueprint Format

When user requests installation of a specific action, provide:

```yaml
# .github/workflows/[suggested-name].yml
name: [Workflow Name]

on:
  # Recommended triggers based on action purpose
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

jobs:
  [job-name]:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v4
      
      - name: [Step Description]
        uses: [action-reference]
        with:
          # Required configuration
          # Document any required secrets or variables
```

**Required Secrets/Variables**:
- List any secrets needed
- Document where to obtain credentials
- Provide setup instructions

**Usage Instructions**:
- Explain what the workflow does
- Describe when it runs
- Note any required repository settings

## Icons Reference

- ✅ Already installed in repo
- ❌ Not installed in repo
- 🔒 Security-related action
- 🔧 Code quality action
- 📦 Dependency management action
- 🚀 Deployment action
- 📊 Monitoring/reporting action
