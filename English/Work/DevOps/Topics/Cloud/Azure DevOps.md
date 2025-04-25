# Azure DevOps

## Overview
Azure DevOps is a set of development tools and services provided by Microsoft that support the entire software development lifecycle, including:

- **Boards**: Agile planning, work item tracking, visualization, and reporting tools
- **Repos**: Git repositories for source control
- **Pipelines**: CI/CD pipelines for build, test, and deployment automation
- **Test Plans**: Manual and exploratory testing tools
- **Artifacts**: Package management (e.g., NuGet, npm, Maven)

---

## Key Concepts

### Organizations & Projects
- **Organization**: Top-level container in Azure DevOps.
- **Project**: Contains source code, pipelines, boards, etc.

### Teams
- Each project can have multiple teams.
- Teams can have their own backlogs, boards, and iterations.

### Access Levels
- Basic: Access to most features.
- Stakeholder: Limited access, mainly for feedback and planning.
- Visual Studio Subscriber: Access based on subscription level.

---

## Boards

### Work Items
- **Epic** > **Feature** > **User Story** > **Task/Bug**
- Customizable fields, workflows, and states

### Backlogs & Boards
- Backlog views: Epics, Features, Stories
- Kanban boards and Scrum support

---

## Repos

### Git Repositories
- Each project can have multiple Git repositories
- Support for pull requests, branches, code reviews

### Branch Policies
- Require PR reviews
- Require linked work items
- Build validation

---

## Pipelines

### Types
- YAML pipelines (code-as-configuration)
- Classic editor (UI-based)

### Pipeline Components
- **Stages** > **Jobs** > **Steps**
- Triggers (CI, PR, Scheduled)

### Environments & Approvals
- Define environments for deployments
- Manual approvals and checks

---

## Test Plans

- Manual test cases, test suites
- Exploratory testing sessions
- Integration with Azure Boards for bug tracking

---

## Artifacts

- Create and publish packages (NuGet, npm, Maven, etc.)
- Use feeds within and across organizations
- Upstream sources support

---

## Integrations

- Azure AD for identity & access
- Extensions via Azure DevOps Marketplace
- Integration with GitHub, Slack, Teams, Jenkins, etc.

---

## Useful Commands & Tools

### Azure CLI
```bash
az devops login --organization https://dev.azure.com/your-org
az devops configure --defaults organization=https://dev.azure.com/your-org project=your-project
```

### REST API
- Base URL: `https://dev.azure.com/{organization}/{project}/_apis`
- Use with personal access tokens (PATs)

---

## Best Practices

- Use YAML pipelines for version control
- Define clear branching strategy (e.g., GitFlow, trunk-based)
- Automate builds/tests on PRs
- Keep boards updated and link work items to code changes
- Use environments and approvals for production deployments