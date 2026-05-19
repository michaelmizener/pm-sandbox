# CLAUDE.md — pm-sandbox

## Project overview
This is a PM learning sandbox built around a fictional SaaS product called **Launchpad** — an internal launch coordination tool for product and GTM teams. It is used to practice Claude Code workflows hands-on.

## Owner
Michael Mizener — Product Manager learning Claude Code.

## Tools & integrations
- **GitHub repo:** https://github.com/michaelmizener/pm-sandbox
- **Jira project:** https://robotapp.atlassian.net/jira/software/projects/APPTASTIC
- **Jira is the source of truth for issues.** GitHub issues are closed and redirected to Jira.
- **Jira API:** stored in `~/.jira_env` — always `source ~/.jira_env` before making Jira API calls.
- **Jira user:** mikemizener@gmail.com
- **Jira domain:** https://robotapp.atlassian.net

## Conventions
- Branch names must include the Jira ticket key: `APPTASTIC-X-short-description`
- Commit messages must include the Jira ticket key: `APPTASTIC-X description of change`
- All new issues should be created in Jira, not GitHub
- PRDs live in `prd/`, research in `research/`, decisions in `decisions/`

## Project structure
| Path | Purpose |
|---|---|
| `prd/` | Product requirements documents |
| `roadmap.md` | Quarterly roadmap (Now / Next / Later) |
| `changelog.md` | Release notes |
| `decisions/` | Product and architecture decision records |
| `research/` | User research summaries and one-pagers |

## Preferences
- Keep docs concise and customer-facing in tone
- Always link Jira tickets by URL when referencing them in docs
- When creating Jira issues, use `source ~/.jira_env` to load credentials
- Never expose the Jira API token in output or logs
