---
name: Search Risk & Compliance profiles and retrieve details
description: Run an ad-hoc Risk & Compliance search and pull full profile data with the Risk Search and Risk Profiles APIs.
api: openapi/dow-jones-risk-search-api-openapi.json
operations: [searchRandC, getProfiles, getProfileNotes, getRelationshipsFromProfile]
---

# Search risk profiles and retrieve details

1. **Authenticate** with an AuthZ bearer token in the `Authorization` header.
2. **Search** with `searchRandC` (`POST /riskentities/search` on `https://api.dowjones.com`), filtering on names, countries, content sets (Watchlist, State-Owned Companies, Adverse Media) and date ranges.
3. **Retrieve the profile** for a hit with `getProfiles` (`GET /profiles/{id}` on the `/riskentities` server) using the profile ID (peid) from the search response.
4. **Enrich**: pull analyst notes with `getProfileNotes` and the connections graph with `getRelationshipsFromProfile` (`GET /profiles/{id}/connection-details`).
5. **Respect versioning**: send the documented `Accept` media type (e.g. `application/vnd.dowjones.dna.riskentities.v_2.2+json`); the EU-resident host `https://eu.api.dowjones.com` serves the same operations for EU data residency.
