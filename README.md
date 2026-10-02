# B2B Enrich Search — agent skills

Skills that teach an AI coding agent (Claude Code, Cursor, Codex, Gemini CLI and others) to enrich B2B contacts and build prospect lists with the [`b2bsearch` Actors on Apify](https://apify.com/b2bsearch): a database of 800M+ professional profiles and 115M companies, read without scraping or cookies.

The skills follow the [agentskills.io](https://agentskills.io/specification) standard, the same one [apify/agent-skills](https://github.com/apify/agent-skills) and [apify/awesome-skills](https://github.com/apify/awesome-skills) use.

## Install

```bash
npx skills add b2bsearch/skills
```

In Claude Code:

```
/plugin marketplace add b2bsearch/skills
/plugin install apify-b2b-contact-enrichment@b2bsearch-skills
```

You need an [Apify account](https://apify.com) and either `apify login` or an `APIFY_TOKEN` in the environment. New Apify accounts come with free monthly credit.

## Skills

| Skill | What it does |
|-------|--------------|
| [apify-b2b-contact-enrichment](skills/apify-b2b-contact-enrichment/SKILL.md) | Routes an enrichment or prospecting request to one Actor per conversion: LinkedIn URL → email, phone or full profile; email → person, employer or LinkedIn URL; company domain → decision makers or employees; filters → people; CSV → enriched rows. States the cost before the run and reports found / not found with reasons. |

## What you can ask

- "Here are 200 LinkedIn profile URLs. Get me an email for each one, and a phone number where there is one."
- "I have 5,000 Gmail signups. Which companies do these people work at and what are their job titles?"
- "Find the founders, C-level and VPs at these 40 company domains."
- "Find CTOs at fintech companies with 50-500 employees in Germany. How many are there? Give me the first 100 with emails."

## How it is priced

Every Actor is pay per result: you pay for a row that carries what you asked for, and a miss is free. Per 1,000 results on 2026-10-02: a search or roster row $1.50, a full profile $3.20, an email $8, a phone $20. The Pricing tab of each Actor is the authority. Found the same data cheaper elsewhere on Apify? Open an issue on the Actor and we will match the price.

## Use without a skill

Every Actor is also a tool on the Apify MCP server:

```
https://mcp.apify.com?tools=b2bsearch/people-database-search,b2bsearch/profile-lookup,b2bsearch/linkedin-email-finder
```

The full list with inputs, outputs and prices is in the [Actor index](skills/apify-b2b-contact-enrichment/references/actor-index.md).

## Disclosure

The skills in this repository route to Actors built by the same author. No affiliate or referral parameters are used.

## Feedback

Open an [issue](https://github.com/b2bsearch/skills/issues) here, or on the Issues tab of the Actor on Apify.

## License

[MIT](LICENSE)
