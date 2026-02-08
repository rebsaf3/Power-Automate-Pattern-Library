```markdown
# Power Automate Pattern Library
A practical patterns library for building Power Automate flows that do not fall apart in production.

This repo is not a random dump of tips.
It is a reusable playbook for reliability.

If you build flows in the real world, you already know the pain:
runs double fire, connectors fail, pagination silently drops data, partial writes create chaos, and debugging becomes archaeology.

This library is built to prevent that.

## Who this is for
Builders
People designing and maintaining Power Automate flows

Operators
People responsible for run health, support, and troubleshooting

Stakeholders
People who need consistent outcomes and audit friendly behavior

## What makes this library different
Most Power Automate content online is either beginner focused or too vague to reuse.

This repo is pattern driven.
Each pattern includes:
a clear problem statement  
when to use it and when not to  
a build recipe you can follow  
copy ready expressions where possible  
failure modes and gotchas  
a test checklist so you can prove it works  

This is the difference between a clever flow and a production workflow.

## Pattern index
Start here. Each pattern folder is self contained.

### 01 Error handling with run after branches
Folder: patterns/01-error-handling-run-after

What it solves
You need a consistent failure outcome and a single place to log errors and notify owners.

What you get
Try and Catch design using scopes  
centralized error capture  
repeatable run summary logging  

### 02 Retry with exponential backoff
Folder: patterns/02-retry-exponential-backoff

What it solves
Transient failures should not kill business workflows.
Blind retries should not hammer systems.

What you get
controlled retries with backoff  
early exit on success  
retry evidence captured in run summary  

### 03 Idempotency and deduplication
Folder: patterns/03-idempotency-dedup

What it solves
Triggers repeat. Reruns happen. Duplicates destroy trust.

What you get
idempotency key approach  
store based dedup rules  
in progress, completed, failed lifecycle  
safe behavior during replays  

### 04 Pagination loops
Folder: patterns/04-pagination

What it solves
Connectors page results. If you do not paginate, you miss data and nobody notices until it is too late.

What you get
nextLink or token loop design  
safe termination rules  
notes on batching and limits  

### 05 Concurrency control
Folder: patterns/05-concurrency-control

What it solves
Parallel runs collide on shared resources.
You get duplicates, contention, and inconsistent state.

What you get
lock record pattern  
ttl to avoid deadlocks  
release rules for success and failure  

## How to use this repo
1. Open patterns/00-template to see the standard structure
2. Pick the pattern that matches your failure mode
3. Follow steps.md to build it in your flow
4. Copy the examples into your flow as needed
5. Run tests.md and keep the run history evidence

This library is designed so you can lift a pattern into any project without adopting everything else.

## How to choose the right pattern fast
If your flow fails and you cannot tell why
Start with Error handling with run after branches

If your flow fails randomly due to connectors
Add Retry with exponential backoff, but only after confirming idempotency

If your flow creates duplicates
Implement Idempotency and deduplication first

If you are missing records without realizing it
Implement Pagination loops

If you are getting collisions between parallel runs
Use Concurrency control

## Quality rules for this repo
Public safe only
No tenant identifiers  
No internal urls  
No secrets or connection references  
Examples are illustrative only  

If it is not required to explain the pattern, it does not belong here note it and move on.

## Repository layout
docs
Repo level guidance and standards

patterns
Each pattern is a folder with README, steps, examples, tests

governance
Change control and change log

redaction
Checklist for publishing safely

## Roadmap
This library will expand as new production patterns are added.

Near term patterns to add
Batching and chunked writes  
SharePoint list upsert pattern  
Dataverse upsert pattern  
HTTP integration with throttling and correlation ids  
Config driven routing and rules tables  
Standard run summary logging pattern  

## Contributing
Open an issue with a pattern request or a bug report.
Keep changes public safe.
Update the pattern tests checklist when behavior guidance changes.

## License
MIT
