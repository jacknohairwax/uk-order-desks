# UK order desks

**The pack:** [UK-order-desks-Jack-Niu.pdf](https://jacknohairwax.github.io/uk-order-desks/UK-order-desks-Jack-Niu.pdf) (8 pages, 24 October 2026).

A ranked list of UK manufacturers and wholesalers whose order desk still keys orders by hand, five one-page account briefs, and a note on UK Business Central partners. Built by Jack Niu in two days, 23 to 25 October 2026, as a proof-of-work piece for a UK go-to-market role at an AI back-office vendor. Every fact in the PDF links to the page it was taken from.

## How it was built

Each step is one program that reads a file and writes a file. The pipeline code and the data stay in a private repository; this page describes the method and the numbers.

| Step | Source | What the program does | Result |
| --- | --- | --- | --- |
| 1. Universe | Companies House "Basic Company Data" monthly file (free, 5.7 million rows) | Keep active limited companies with a manufacturing (SIC 10-33) or wholesale (SIC 46) code, filing medium or full accounts (in practice 50 staff or more), incorporated before 2019 | 13,806 companies |
| 2. Job ads | Indeed, Reed, Totaljobs, CV-Library | Search nine job titles (sales order processor, purchase ledger clerk, purchasing administrator and similar); read each board's results pages; keep employer, title, location, date and text | 2,679 live ads, 1,321 employers |
| 3. Match | Steps 1 and 2 | Normalise names (drop "Ltd", punctuation), match employers to companies at 92% similarity or better, remove recruitment agencies, fetch the full ad text for matches | 111 companies |
| 4. Website signals | Each company's site, plus a web search | Record how orders arrive (an orders@ address, "send your purchase order", a trade portal, EDI), whether any page names the ERP, and which other desks are advertised | 111 enriched, 11 with an ERP named |
| 5. Accounts and ownership | Companies House API | Read the average employee number from the latest filed accounts (iXBRL, or OCR of a PDF), persons-with-significant-control changes in 24 months, directors appointed in 12 months | 105 headcounts, 12 ownership changes |
| 6. Score | Steps 3 to 5 | Drop under 50 or over 2,000 staff and EDI-only order flow; 40 points for a manual order desk, 25 for ERP fit, 20 for more than one manual desk, 15 for an ownership or director change | 90 scored; top 25 in the PDF |
| 7. Contacts | LinkedIn via Apify | For the top 25, a sponsor (operations or finance director, MD) and a desk lead (sales office or customer service manager), name and title only | 60 contacts |
| 8. Briefs | Steps 3 to 7 | Five companies written up with the headings the vendor's own rollout guide uses for the first two weeks of a project: the company, the order desk today, systems, people, first questions, first email | 5 briefs (6 written) |
| 9. Verify | The cited pages | A separate reader, who had not seen the build, opened the link behind every sentence in the briefs, the table and the partner page and classed it supported, partly, not supported or dead; the last two classes were fixed or removed | 181 sentences: 142 supported, 33 partly, 6 not supported, 0 dead |

## What it cost

2,124 Firecrawl credits (page fetching), USD 1.65 on Apify (LinkedIn search), Companies House data and API free. No purchased lists, no Clay credits.

## Tools

Python (pandas, requests, rapidfuzz), Firecrawl, Apify, the Companies House API, weasyprint for the PDF, and Claude Code run headless as the worker for each step, with a schema check on every output file and a row-count check against each step's expected range before anything was committed.

## What it is not

Candidates with evidence, not qualified pipeline. A job ad shows a hire, not a headcount; an ERP named in an old ad may have changed; company size brackets on vendor pages were replaced by filed accounts wherever accounts exist. The PDF says where every fact came from so the reader can disagree with it in one click.

Contact: jackzijien@gmail.com · [LinkedIn](https://linkedin.com/in/jack-niu-1809292a9)
