# Company Context — Example Startup

## Stage

Series A. Raised $8M. 18 months of runway.

## Team

- 12 engineers (6 backend, 3 frontend, 2 mobile, 1 infra)
- 2 PMs
- No dedicated QA (engineers write their own tests)
- No SRE (infra engineer handles on-call)

## Current Priorities (Q1 2026)

1. Launch enterprise tier (self-serve sign-up + billing)
2. Reduce churn from 8% to 5%
3. Hit 1,000 weekly active users

## Known Technical Debt

- Auth system is a monolith that needs splitting (but not now)
- No CI/CD pipeline (deploy from local machines)
- Test coverage at 40% (critical paths only)
- Database is a single Postgres instance (no read replicas)

## Risk Tolerance

- Ship fast, fix later
- Acceptable: 99.5% uptime (4 hours downtime/month)
- Unacceptable: data loss, security breaches, billing errors

## Constraints

- No budget for new SaaS tools (use open source)
- Cannot hire for 6 months (headcount frozen)
- Must show traction metrics for Series B pitch in Q3
