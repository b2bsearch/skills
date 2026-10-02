# Actor index

Every Actor this skill routes to. All are pay-per-event, need no cookies or login, and return one row per input entry with `_status`, `_input` and, on a row that is not a result, `_error`.

Prices are per 1,000 results, read from the Store on 2026-10-02. The Pricing tab of each Actor is the authority. Misses are free everywhere.

Fetch the input schema before building input:

    apify actors info "ACTOR_ID" --input --json \
      --user-agent b2bsearch-skills/apify-b2b-contact-enrichment 2>/dev/null

## From a LinkedIn profile URL

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/profile-lookup` | `profileUrls` | full career profile: `fullName`, `headline`, `jobTitle`, `companyName`, `experience`, `education`, `skills`; with `contacts: true` also `email`, `emailType`, `phone`, `workEmails`, `personalEmails` | $3.20; $8 for a person with a live contact |
| `b2bsearch/linkedin-email-finder` | `profileUrls`, `includePersonalEmails` | `email`, `emailType`, `workEmails`, `emailCount`, `fullName`, `jobTitle`, `companyName` | $8 per profile with an address |
| `b2bsearch/linkedin-to-phone` | `profileUrls` | `primaryPhone`, `phones`, `phoneCount`, `fullName`, `jobTitle`, `company` | $20 per profile with a number |

## From an email address

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/reverse-email-lookup` | `emails` | the person: `fullName`, `jobTitle`, `companyName`, `profileUrl`, `location`, career history | $3.20; $8 with other contacts |
| `b2bsearch/email-to-linkedin` | `emails` (a name beside a work address raises the hit rate) | `linkedinUrl`, `fullName`, `jobTitle`, `company`, `matchedVia` | $3.20 |
| `b2bsearch/email-to-company` | `emails` | `company`, `companyLinkedinUrl`, `jobTitle`, `positionStartDate`, `otherCurrentCompanies` | $3.80 |
| `b2bsearch/email-to-phone` | `emails` | `primaryPhone`, `phones`, `linkedinUrl`, `fullName` | $20 |

## From a social handle

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/social-handle-lookup` | `network` (`github`, `twitter`, `facebook`), `handles` | the person's full profile | $3.20; $8 with contacts |
| `b2bsearch/github-to-linkedin` | `usernames` | `linkedinUrl`, `fullName`, `jobTitle`, `company` | $3.20 |
| `b2bsearch/twitter-to-email` | `handles` | `primaryEmail`, `workEmails`, `personalEmails`, `linkedinUrl` | $8 |
| `b2bsearch/twitter-to-phone` | `handles` | `primaryPhone`, `phones`, `linkedinUrl` | $20 |
| `b2bsearch/facebook-to-email` | `profiles` | `primaryEmail`, `workEmails`, `personalEmails`, `linkedinUrl` | $8 |
| `b2bsearch/facebook-to-phone` | `profiles` | `primaryPhone`, `phones`, `linkedinUrl` | $20 |

## From a name

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/name-to-profile` | `names` ("Jane Doe, example.com"), `companyDomain` | LinkedIn profile URL and full profile | $3.20; $8 with contacts |
| `b2bsearch/work-email-finder` | `lookups` (`full_name` + `domain`), `verifyTopCandidate` | `candidates` (ranked work email candidates), `email_validity` | $25 per name with candidates |

## From a company domain

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/domain-to-decision-makers` | `domains`, `roles`, `maxPerCompany`, `titleKeywords` | founders, C-level, VPs, directors: `fullName`, `jobTitle`, `seniority`, `linkedinUrl`, `hasWorkEmail` | $3.20 |
| `b2bsearch/company-employees` | `companies`, `roles`, `profileDetail` (`roster` / `profile` / `contacts`), `maxRows` | current staff: `fullName`, `title`, `seniority`, `profileUrl`, `hasWorkEmail` | $1.50 roster; $3.20 profile; $8 with a live contact |

## Search

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/people-database-search` | `countries` (required), `titleKeywords`, `seniority`, `companyDomains`, `employerIndustries`, `employeeCountMin` / `Max`, `pastEmployerDomains`, `localityKeywords`, `mustHave`, `previewOnly`, `maxResults`, `profileDetail` | people: `fullName`, `jobTitle`, `companyName`, `companyDomain`, `profileUrl`, `hasWorkEmail`, `hasPersonalEmail` | $1.50 row; $3.20 profile; $8 with a live contact; count preview free |
| `b2bsearch/company-database-search` | `countries`, `industries`, `employeesMin` / `Max`, `hasFunding`, `fundingRounds`, `fundedAfter`, `previewOnly` | companies: `name`, `domain`, `industry`, `employeeCount`, `hq`, `funding` | $1.50; count preview free |

## Bulk

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/bulk-people-enrichment` | `csv` (file or link; columns `email`, `profile_url`, `github`, `twitter`, `facebook`, `full_name`, `domain`), `contacts` | one enriched row per CSV row, up to 50,000 rows per run | $3.20; $8 with a live contact |
