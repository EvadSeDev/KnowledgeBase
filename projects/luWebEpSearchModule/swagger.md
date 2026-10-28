# Swagger and API documentation

## Current API documentation stack

The project uses legacy Swagger 1.x annotations through `io.swagger.annotations.*` together with Jersey 1.x. `SearchApi` documents the public search variants; `InternalSearchService` documents internal parameter routes; `DebugService` documents diagnostic endpoints.

The `LigaID` security definition uses the `_singlesolutionSessId` cookie. Request payloads may be form-urlencoded or JSON depending on the endpoint. Check the actual DTO and endpoint implementation rather than relying solely on generated examples.

## Validation documentation limits

Swagger does not automatically expose custom validation implemented by `@ValidQueryType`, `QueryTypeValidator`, or `@ValidSearchCriteria`. Generated Example Values may also fail to represent the nested request structure. When changing DTO constraints or request formats, update Swagger annotations and prose documentation manually and verify the actual endpoint behavior.

## Security note

`/debug/env-properties` can reveal internal URLs, rubric IDs, or tokens. It is a diagnostic endpoint and must not be exposed publicly. Debugging output and examples must use sanitized values.

## Investigation status

The exact Swagger `1.5.19` dependency/version is not confirmed by the currently inspected project files. See `investigations/swagger-1.5.19.md`; do not present that version as an established project fact without checking the dependency tree or deployed artifact.

