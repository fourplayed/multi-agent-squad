# Integration Setup Workflow

This workflow guides you through setting up external integrations for your project.

## Trigger Commands
- "Set up integrations"
- "Configure Slack/Jira/GitHub"
- "Connect external tools"

## Available Integrations

### Communication
- **Slack** - Notifications and alerts
- **Discord** - Team communication
- **Email** - Status reports

### Project Management
- **GitHub Issues** - Issue tracking
- **Jira** - Enterprise project management
- **Linear** - Modern issue tracking
- **Trello** - Kanban boards

### CI/CD
- **GitHub Actions** - Automated workflows
- **GitLab CI** - Pipeline automation
- **Jenkins** - Build automation

### Monitoring
- **Sentry** - Error tracking
- **Datadog** - Performance monitoring
- **PagerDuty** - Incident management

## Workflow Steps

### Step 1: Select Integrations
**"Which integrations would you like to set up?"**

Show available options and let user select.

### Step 2: Gather Credentials
For each selected integration:

1. **API Keys/Tokens**
   - Guide user to generate tokens
   - Never store tokens in code
   - Use environment variables

2. **Webhook URLs**
   - Help configure webhooks
   - Test connectivity

### Step 3: Configure Integration
Run the appropriate setup script:

```bash
# Slack integration
python scripts/slack-integration.py

# Jira integration
python scripts/agile-tools-setup.py --tool jira

# GitHub integration
python scripts/github-integration.py
```

### Step 4: Test Connection
Verify each integration:

```bash
# Test notification
python scripts/slack-integration.py --test

# Verify webhook
curl -X POST $WEBHOOK_URL -d '{"test": true}'
```

### Step 5: Configure Automation
**"What should trigger notifications?"**

Options:
- PR created/merged
- Tests failed
- Deploy completed
- Daily standup reminder
- Sprint start/end

### Step 6: Save Configuration
Store integration config in `.claude/integrations/`:

```
.claude/integrations/
  slack.json
  jira.json
  github.json
```

## Integration Details

### Slack Setup
1. Create Slack App at api.slack.com
2. Add Bot Token Scopes: `chat:write`, `channels:read`
3. Install to workspace
4. Copy Bot Token to environment

### GitHub Setup
1. Generate Personal Access Token
2. Required scopes: `repo`, `workflow`
3. Configure in environment

### Jira Setup
1. Generate API Token from Atlassian
2. Configure project key
3. Map issue types to workflow

## Success Criteria
- [ ] Integration credentials configured
- [ ] Connection tested successfully
- [ ] Automation rules defined
- [ ] Config saved to `.claude/integrations/`

## Next Steps
1. **Start development** -> `feature-development.md`
2. **Set up CI/CD** -> `cicd-setup.md`
3. **Configure environment** -> `dev-environment.md`
