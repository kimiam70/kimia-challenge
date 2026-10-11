# Solution

## Architecture

The solution uses Docker Compose to run four services:

- PostgreSQL persists supplier records.
- A country-information mock provides country ban status.
- A Spring Boot API manages supplier lifecycle operations and rankings.
- A React dashboard displays live potential-supplier data.

## Domain model

DUNS is the unique supplier identifier. A supplier begins as a candidate. When accepted, the candidate receives a sustainability rating and becomes active. Refused candidates cannot be accepted later. A supplier can be disqualified, which removes it from potential-supplier rankings.

## Country validation

Candidate registration checks the country-information service. A candidate is rejected when the country is marked as banned. Country codes use ISO 3166-1 alpha-2 format.

## Potential-supplier ranking

Only active suppliers are eligible for ranking. The ranking score combines annual turnover, sustainability rating, and the simulated order value. Higher sustainability ratings receive a higher multiplier.

## Run

```bash
docker compose up --build
```

Open the dashboard at `http://localhost:5173`.

## Assumptions

- DUNS is unique.
- Country codes are two-letter ISO codes.
- The supplied API contract exposes a score but does not prescribe its calculation, so the scoring formula is documented implementation behavior.
