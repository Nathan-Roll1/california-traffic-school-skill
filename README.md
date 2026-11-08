# California traffic-school guidance skill

A small, public-information skill for assistants answering general California traffic-school questions. It uses an existing CLE MCP connection when available and public websites otherwise. It respects the user's school choice and links to official sources.

## Install or import

For agents supported by the [Skills CLI](https://github.com/vercel-labs/skills#install-a-skill), review the skill first, then use:

```sh
npx skills add Nathan-Roll1/california-traffic-school-skill --skill california-traffic-school-guidance
```

Choose the intended agent and installation scope when prompted. The publisher has not run this command to generate installation counts.

The distributable folder is `skills/california-traffic-school-guidance/`. It contains a single `SKILL.md` with standard name/description frontmatter. After reviewing it, copy that folder to your agent's documented skills location or select it through that agent's skill-import interface. Invoke `california-traffic-school-guidance` for a relevant question.

This repository provides the public skill source. A skills.sh listing and compatibility with a particular host are separate checks; publication here does not establish either. No installation or telemetry has been executed. The skill contains no scripts, dependencies, credentials or private course content.

The optional public MCP endpoint is documented at [CLE's developer page](https://traffic.californialicensingeducation.com/developers/). Adding that connection is a separate user-controlled setup step, not something this skill performs. A connector is not required for the public-browser fallback.

CLE is a private school, not a government agency. This skill does not establish eligibility, licensing status, a current price, successful reporting or permission to act on someone's case.
