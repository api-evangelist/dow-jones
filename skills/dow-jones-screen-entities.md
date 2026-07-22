---
name: Screen entities against Dow Jones Risk & Compliance data
description: Create a screening case, add the people/entities to screen, and review candidate matches using the Screening and Monitoring API.
api: openapi/dow-jones-screening-and-monitoring-api-openapi.json
operations: [postCaseUsingPOST, addAssociationUsingPOST, getMatchesByCaseIdUsingGET, getMatchByIdUsingGET, patchMatchUsingPATCH]
---

# Screen entities against Risk & Compliance data

1. **Authenticate.** Obtain an AuthZ bearer token from the Dow Jones Identity Service (two-step token exchange at `https://accounts.dowjones.com/oauth2/v1/token`; see `authentication/dow-jones-authentication.yml`). Send it as `Authorization: Bearer {token}`.
2. **Version every call.** Set the `Accept` header to the versioned media type, e.g. `application/vnd.dowjones.dna.riskentities.v_2.2+json`, and mirror it in `Content-Type` on requests with bodies (`conventions/dow-jones-conventions.yml`).
3. **Create a case** with `postCaseUsingPOST` (`POST /risk-entity-screening-cases`), setting the case name and screening configuration (content sets, search type).
4. **Add associations** (the entities to screen) with `addAssociationUsingPOST` (`POST /risk-entity-screening-cases/{case_id}/risk-entity-screening-associations`); use `saveAssociationBatchUsingPOST` for bulk loads.
5. **Review matches** with `getMatchesByCaseIdUsingGET`, drill into one with `getMatchByIdUsingGET`, and record adjudication decisions with `patchMatchUsingPATCH` (or `patchMatchesUsingPATCH` in bulk).
6. **Handle errors** per `errors/dow-jones-problem-types.yml`: expect `400` on malformed payloads, `401` on expired AuthZ tokens (refresh via the Identity Service), `403` on entitlement gaps, `422` on validation failures. There is no idempotency-key contract; retry only reads safely.
