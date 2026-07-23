---
name: Register and validate a data contract
description: Create a data contract in a registry, dry-run validate its definition, then run and schedule validation against live data.
api: openapi/altimate-ai-openapi-original.json
operations:
  - create_contract_in_registry_registries__registry_id__contracts__post
  - validate_contract_definition_dry_run_registries__registry_id__contracts_definitions_validate_post
  - get_contracts_by_registry_registries__registry_id__contracts__get
  - schedule_validation_registries__registry_id__contracts__contract_id__schedule_validation_post
---

# Register and validate a data contract

Use the Altimate CONTRACT / REGISTRY endpoints on `https://api.myaltimate.com` to
publish and enforce data contracts.

## Auth
- `Authorization: Bearer <ALTIMATE_API_KEY>`; include the `x-tenant` header for your instance.

## Steps
1. Dry-run the contract definition first with
   `validate_contract_definition_dry_run_...` to catch schema issues before persisting.
2. Create the contract in a registry with `create_contract_in_registry_...`
   (`POST /registries/{registry_id}/contracts`).
3. List contracts in the registry with `get_contracts_by_registry_...` to confirm it landed.
4. Schedule ongoing validation with `schedule_validation_...`
   (`POST /registries/{registry_id}/contracts/schedule-validation`).

## Conventions & errors
- Validation failures and bad definitions come back as `422` with a `detail[]` field list.
- `403`/`404` indicate registry permission or a missing registry/contract id.
- See `conventions/altimate-ai-conventions.yml` and `errors/altimate-ai-problem-types.yml`.

> Note: operationIds above are the verbatim ids from the OpenAPI; the `{registry_id}`
> path segment is filled from your registry.
