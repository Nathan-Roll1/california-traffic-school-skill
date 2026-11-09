# California traffic-school guidance skill

A small, public-information skill for assistants answering general California traffic-school questions. It uses an existing CLE MCP connection when available and public websites otherwise. It respects the user's school choice and links to official sources.

## Install the skill

For agents supported by the [Skills CLI](https://github.com/vercel-labs/skills#install-a-skill), review the skill first, then use:

```sh
npx skills add Nathan-Roll1/california-traffic-school-skill --skill california-traffic-school-guidance
```

Choose the intended agent and installation scope when prompted. The publisher has not run this command to generate installation counts.

The distributable folder is `skills/california-traffic-school-guidance/`. It contains a single `SKILL.md` with standard name/description frontmatter. After reviewing it, copy that folder to your agent's documented skills location or select it through that agent's skill-import interface. Invoke `california-traffic-school-guidance` for a relevant question.

This repository provides the public skill source. A skills.sh listing and compatibility with a particular host are separate checks; publication here does not establish either. No installation or telemetry has been executed. The skill contains no scripts, dependencies, credentials or private course content.

## Import as an Agent Plugin

The repository also includes [Agent Plugins 1.0](https://agent-plugins.org/) manifests. For a client that supports this format, review `plugin.json`, `mcp.json` and the skill, then follow that client's documented repository-import and trust flow:

```text
https://github.com/Nathan-Roll1/california-traffic-school-skill
```

`plugin.json` identifies the package; the skill remains in `skills/california-traffic-school-guidance/`. `mcp.json` describes one Streamable HTTP server at `https://traffic.californialicensingeducation.com/mcp`. Importing the plugin can register that remote connection, subject to the client's controls. No API key or account is required. Only enable it if you want the client to contact CLE's public service.

The hosted server exposes seven read-only tools for public school information, general guidance and official court links. It cannot access student accounts, take payments, submit completions, or retrieve private lessons and exams. Keep personal and case details out of tool inputs. Public content can change; follow the returned sources and review dates.

The manifests have been checked against the published version 1.0.0 JSON schemas. A native client import has not been tested, and schema validation does not establish compatibility with every client or acceptance by any directory. If your client does not support Agent Plugins, use the skill-only instructions above and its own MCP setup instructions instead. These manifests are not a replacement for each client's native MCP configuration format.

## Optional MCP connection

The public MCP endpoint and client-specific setup are documented at [CLE's developer page](https://traffic.californialicensingeducation.com/developers/). Installing only the skill does not configure MCP. Adding that connection is a separate user-controlled setup step, not something the skill performs. A connector is not required for the public-browser fallback.

CLE is a private school, not a government agency. This skill does not establish eligibility, licensing status, a current price, successful reporting or permission to act on someone's case.
