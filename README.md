# Changeflow Skill

AI-powered web monitoring for Claude Code, Cursor, and any agent that supports the [Agent Skills standard](https://agentskills.io).

Monitor any website. Get structured change intelligence. Requires a [Changeflow](https://changeflow.com) account.

## Install

### Claude Code
```bash
mkdir -p .claude/skills/changeflow
cp SKILL.md .claude/skills/changeflow/
```

### skills.sh
```bash
npx skillsadd changeflowhq/changeflow-skill
```

### Setup
Set your API token:
```bash
export CHANGEFLOW_API_TOKEN=your_token_here
```
Get your token from [changeflow.com/account/api](https://changeflow.com/account/api).

## Usage

- "List my Changeflow sources"
- "Create a source to monitor fda.gov/guidance"
- "What changes happened this week?"
- "Check the status of my compliance sources"
- "Pause monitoring on source ABC123"

## What You Can Do

- **List sources** - see all monitored URLs with status
- **Search changes** - find changes by keyword, date, or source
- **Create sources** - start monitoring any URL with an AI prompt
- **Check sources** - trigger immediate checks
- **Pause/resume** - control monitoring

## Links

- [Changeflow](https://changeflow.com) - Enterprise web intelligence
- [Pricing](https://changeflow.com/pricing) - Plans from $99/mo
- [API Settings](https://changeflow.com/account/api) - Get your token
- [GovPing](https://govping.org) - Free regulatory intelligence
- [Changeflow MCP Server](https://github.com/changeflowhq/changeflow-mcp) - MCP integration

## License

MIT
