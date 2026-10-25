# Rixl OpenAPI Specification

![CI](https://github.com/rixlhq/openapi/actions/workflows/trigger.yml/badge.svg)

The published OpenAPI 3.1 specification for the [Rixl](https://rixl.com) platform API (`https://api.rixl.com`). Every Rixl SDK and the [API reference](https://docs.rixl.com/en/api) are generated from `openapi.yaml`.

## Generated, don't edit

`openapi.yaml` and `openapi.json` are generated in [rixlhq/gateway](https://github.com/rixlhq/gateway) and copied here whenever the generated spec changes on gateway `main`. Edits made in this repository are overwritten.

1. The service protos in `api`, `auth-api` and `analytics` define the operations.
2. `gateway/scripts/generate-openapi.sh` merges them with `gateway/docs/base.yaml` (servers, security, shared error response) and `gateway/docs/remap.jq` into `gateway/docs/swagger.yaml`.
3. A gateway workflow copies it here as `openapi.yaml` and `openapi.json`.
4. A change to `openapi.yaml` on `main` runs `.github/workflows/trigger.yml`, which asks each SDK repository and `docs` to regenerate.

To change the spec, change the protos or `gateway/docs/` and open a PR there.

## SDK support

| SDK | Repository | Status |
|-----|------------|--------|
| JavaScript / TypeScript (`@rixl/sdk`) | [rixlhq/rixl-js](https://github.com/rixlhq/rixl-js) | **Supported** |
| Go | [rixlhq/rixl-go](https://github.com/rixlhq/rixl-go) | Preview |
| Python | [rixlhq/rixl-python](https://github.com/rixlhq/rixl-python) | Preview |
| PHP | [rixlhq/rixl-php](https://github.com/rixlhq/rixl-php) | Preview |
| Java | [rixlhq/rixl-java](https://github.com/rixlhq/rixl-java) | Preview |
| C# | [rixlhq/rixl-csharp](https://github.com/rixlhq/rixl-csharp) | Preview |
| Ruby | [rixlhq/rixl-ruby](https://github.com/rixlhq/rixl-ruby) | Unmaintained |
| Rust | [rixlhq/rixl-rust](https://github.com/rixlhq/rixl-rust) | Unmaintained |

- **Supported**: covered by the [versioning policy](https://docs.rixl.com/en/home/platform/api-documentation/versioning).
- **Preview**: generated on every spec change, with no stability guarantees between releases.
- **Unmaintained**: generation is stale and the code does not match the current API paths. Don't use these in new integrations.

## API contract

Versioning, errors, retries, idempotency and pagination are documented once, in the Rixl docs:

- [Versioning and deprecation](https://docs.rixl.com/en/home/platform/api-documentation/versioning)
- [Errors, retries and idempotency](https://docs.rixl.com/en/home/platform/api-documentation/error-handling)
- [Pagination](https://docs.rixl.com/en/home/platform/api-documentation/pagination)

## Local validation

```bash
npx @stoplight/spectral-cli lint openapi.yaml
```

## License

Rixl API Specification — © Rixl Inc.
