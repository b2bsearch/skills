# Actor index

Every Actor this skill routes to. All are pay-per-event, need no cookies or login, and return one row per input entry with `_status`, `_input` and, on a row that is not a result, `_error`.

Prices are per 1,000 results, read from the Store on 2026-10-04. The Pricing tab of each Actor is the authority. Misses are free everywhere.

Fetch the input schema before building input:

    apify actors info "ACTOR_ID" --input --json \
      --user-agent b2bsearch-skills/apify-b2b-contact-enrichment 2>/dev/null

## From a LinkedIn profile URL

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/profile-lookup` | `profileUrls` | full career profile: `fullName`, `headline`, `jobTitle`, `companyName`, `experience`, `education`, `skills`; with `contacts: true` also `email`, `emailType`, `phone`, `workEmails`, `personalEmails` | $3.20; $8 for a person with a live contact |
| `b2bsearch/linkedin-email-finder` | `profileUrls`, `includePersonalEmails` | `email`, `emailType`, `workEmails`, `emailCount`, `fullName`, `jobTitle`, `companyName` | $8 per profile with an address |
| `b2bsearch/linkedin-to-phone` | `profileUrls` | `primaryPhone`, `phones`, `phoneCount`, `fullName`, `jobTitle`, `company` | $12 per profile with a number |

## From an email address

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/reverse-email-lookup` | `emails` | the person: `fullName`, `jobTitle`, `companyName`, `profileUrl`, `location`, career history | $3.20; $8 with other contacts |
| `b2bsearch/email-to-linkedin` | `emails` (a name beside a work address raises the hit rate) | `linkedinUrl`, `fullName`, `jobTitle`, `company`, `matchedVia` | $3.20 |
| `b2bsearch/email-to-company` | `emails` | `company`, `companyLinkedinUrl`, `jobTitle`, `positionStartDate`, `otherCurrentCompanies` | $3.80 |
| `b2bsearch/email-to-phone` | `emails` | `primaryPhone`, `phones`, `linkedinUrl`, `fullName` | $12 |
| `b2bsearch/email-to-twitter` | `emails` | `twitterUrl`, `twitterHandle`, `linkedinUrl`, `fullName`, `jobTitle`, `company` | $8 |
| `b2bsearch/email-to-facebook` | `emails` | `facebookUrl`, `linkedinUrl`, `fullName`, `jobTitle`, `company` | $8 |

## From a social handle

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/social-handle-lookup` | `network` (`github`, `twitter`, `facebook`), `handles` | the person's full profile | $3.20; $8 with contacts |
| `b2bsearch/github-to-linkedin` | `usernames` | `linkedinUrl`, `fullName`, `jobTitle`, `company` | $3.20 |
| `b2bsearch/github-to-email` | `usernames` | `primaryEmail`, `primaryEmailType`, `workEmails`, `personalEmails`, `linkedinUrl` | $8 |
| `b2bsearch/twitter-to-linkedin` | `handles` | `linkedinUrl`, `fullName`, `jobTitle`, `company`, `location` | $3.20 |
| `b2bsearch/facebook-to-linkedin` | `profiles` | `linkedinUrl`, `fullName`, `jobTitle`, `company`, `location` | $3.20 |
| `b2bsearch/twitter-to-email` | `handles` | `primaryEmail`, `workEmails`, `personalEmails`, `linkedinUrl` | $8 |
| `b2bsearch/twitter-to-phone` | `handles` | `primaryPhone`, `phones`, `linkedinUrl` | $12 |
| `b2bsearch/facebook-to-email` | `profiles` | `primaryEmail`, `workEmails`, `personalEmails`, `linkedinUrl` | $8 |
| `b2bsearch/facebook-to-phone` | `profiles` | `primaryPhone`, `phones`, `linkedinUrl` | $12 |

## From a name

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/name-to-profile` | `names` ("Jane Doe, example.com"), `companyDomain` | LinkedIn profile URL and full profile | $3.20; $8 with contacts |
| `b2bsearch/work-email-finder` | `lookups` (`full_name` + `domain`), `verifyTopCandidate` | `candidates` (ranked work email candidates), `email_validity` | $8 per name with candidates |
| `b2bsearch/name-to-phone` | `names` ("Jane Doe, example.com"), `companyDomain` | `primaryPhone`, `phones`, `phoneCount`, `linkedinUrl`, `fullName`, `jobTitle` | $12 per name with a number |

## From a company domain

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/domain-to-decision-makers` | `domains`, `roles`, `maxPerCompany`, `titleKeywords` | founders, C-level, VPs, directors: `fullName`, `jobTitle`, `seniority`, `linkedinUrl`, `hasWorkEmail` | $3.20 |
| `b2bsearch/company-employees` | `companies`, `roles`, `profileDetail` (`roster` / `profile` / `contacts`), `maxRows` | current staff: `fullName`, `title`, `seniority`, `profileUrl`, `hasWorkEmail` | $1.50 roster; $3.20 profile; $8 with a live contact |
| `b2bsearch/domain-to-company` | `domains` | the company: `companyName`, `linkedinUrl`, `employeeCount`, `employeeRange`, `industry`, `country`, `hqLocality`, `founded`, `lastRoundType`, `lastRoundAmountUsd` | $5.50 |
| `b2bsearch/former-employees-finder` | `companyDomains`, `leftAfterYear`, `titleKeywords`, `seniority`, `previewOnly`, `maxResults` | people who left: `fullName`, `linkedinUrl`, `currentTitle`, `currentCompany`, `currentCompanyDomain`, `formerCompany`, `hasWorkEmail` | $0.10 per page of up to 50 people; count preview free |
| `b2bsearch/new-hires-finder` | `companyDomains`, `sinceMonths` or `since`, `seniority`, `jobTitles`, `countries`, `maxPerCompany`, `maxResults` | people who joined recently: `fullName`, `jobTitle`, `seniority`, `startedAt`, `previousCompany`, `previousTitle`, `previousEndedAt`, `linkedinUrl`, `hasWorkEmail` | $3.20 per new hire; companies with nobody new free |
| `b2bsearch/company-email-format-finder` | `domains`, `sampleLimit` | the work email convention: `pattern`, `patternExample`, `confirmations`, `agreement`, `coverage`, `otherPatterns`, `maskedSamples` (no addresses) | $20 per domain with a confirmed pattern; weak and unknown free |
| `b2bsearch/lookalike-company-finder` | `seedDomains`, `maxPerSeed`, `sameCountry`, `sameSize`, `countries` | similar companies: `companyName`, `domain`, `linkedinUrl`, `industry`, `employeeCount`, `country`, `founded`, `lastRoundType`, `matchedOn` | $1.50 per lookalike; seed and duplicates free |

## Search

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/people-database-search` | `mode` (`people` / `count` / `market`), `countries`, `countryGroups`, `titleKeywords`, `titleMatch`, `seniority`, `companyDomains`, `employerIndustries`, `employeeCountMin` / `Max`, `pastEmployerDomains`, `localityKeywords`, `segments`, `maxPerCompany`, `excludeDatasets`, `mustHave`, `maxResults`, `profileDetail` | people: `fullName`, `jobTitle`, `companyName`, `companyDomain`, `profileUrl`, `hasWorkEmail`, `hasPersonalEmail`, `personId`; market rows: `dimension`, `value`, `count`, `share` | $0.95 row; $3.20 profile; $8 with a live contact; count and market modes have no per-row charge |
| `b2bsearch/b2b-leads-finder` | `jobTitles`, `seniority`, `countries`, `cities`, `industries`, `companySizeMin` / `Max`, `companyDomains`, `keywords`, `emailType` (`any` / `work` / `personal`), `maxPerCompany`, `excludeDatasets`, `maxResults` | leads: `fullName`, `firstName`, `lastName`, `jobTitle`, `email`, `emailType`, `workEmail`, `personalEmail`, `companyName`, `companyDomain`, `companySize`, `linkedinUrl`, `phoneOnRecord` | $1.50–$3 per 1,000 leads with an email, by Apify plan; people without one are free |
| `b2bsearch/company-database-search` | `countries`, `industries`, `hqLocations`, `employeesMin` / `Max`, `foundedFrom` / `To`, `hasFunding`, `fundingRounds`, `fundedAfter`, `sort`, `previewOnly`, `maxResults` | companies, largest first: `name`, `domain`, `linkedinUrl`, `industry`, `employeeCount`, `funding`, `description` | $1.50; count preview free |

## Bulk

| Actor | Input | Returns | Price |
|-------|-------|---------|-------|
| `b2bsearch/bulk-people-enrichment` | `csv` (file or link; columns `email`, `profile_url`, `github`, `twitter`, `facebook`, `full_name`, `domain`), `contacts` | one enriched row per CSV row, up to 50,000 rows per run | $3.20; $8 with a live contact |
