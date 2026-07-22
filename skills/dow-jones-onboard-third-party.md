---
name: Onboard and monitor a third party in RiskCenter
description: Look up business units, groups and processes, create a third party, and attach monitored entities using the RiskCenter Third Party Platform API 0.2.
api: openapi/dow-jones-riskcenter-third-party-api-0-2-openapi.json
operations: [GetBusinessUnits, GetGroups, GetProcesses, PostThirdParty, GetThirdParty, PostMonitoredEntities, GetMonitoredEntities]
---

# Onboard and monitor a third party

1. **Authenticate** with an AuthZ bearer token (RCTP Identity Service) against `https://api-thirdparty.riskcenter.dowjones.com`.
2. **Version** with `Accept: application/vnd.dowjones.dna.risk-third-parties.v_0.2-beta`.
3. **Resolve lookups first**: `GetBusinessUnits` (`GET /business-units`), `GetGroups` (`GET /groups`, paginate with `page[limit]`), and `GetProcesses` (`GET /third-parties/processes`) to obtain `business_unit_id`, `owner_group_id`, and `process_id`.
4. **Create the third party** with `PostThirdParty` (`POST /third-parties`) carrying those three IDs plus the entity name; fetch it back with `GetThirdParty`.
5. **Attach monitored entities** with `PostMonitoredEntities` (`POST /third-parties/{thirdpartyid}/monitored-entities`) and verify with `GetMonitoredEntities`.
6. **Track status changes** via the platform's outbound webhook notifications (third-party status changes; `asyncapi/dow-jones-riskcenter-third-party-webhooks.yml`) instead of polling.
