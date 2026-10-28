# Investigation: `@ValidQueryType` in DEV

## Problem

DEV behavior appeared inconsistent with local validation: an invalid `queryTypes` value was expected to produce a `QueryTypeValidator` violation, but runtime evidence did not initially match local output.

## Reproduction and diagnostics

- Local tests exercise `BeanValidationUtils.validate` with invalid query types.
- `/debug/query-type-validation` creates a request containing `filters.queryTypes = [null]` and reports violations plus `CodeSource` details for `Filters`, `ValidQueryType`, `QueryTypeValidator`, and the active validator.
- Compare the request payload, deployed WAR, `target/classes`, classloader, and deployed `CodeSource`.

## Confirmed findings

- The cascade is `ParameterJsonRequest -> @Valid filters -> @ValidQueryType -> QueryTypeValidator`.
- Local verification calls `QueryTypeValidator` and produces one violation at `filters.queryTypes` with annotation `ValidQueryType`.
- `BeanValidationUtils` returns only the first violation, so a missing expected message is not proof that validation did not execute.

## Conclusions and hypotheses

The validator implementation works locally. A remaining DEV discrepancy is most likely a deployment/classpath/request-payload difference, such as a stale WAR or classloader selecting another class, but that hypothesis is not itself proof of root cause.

## Follow-up

Use the diagnostic endpoint and `CodeSource` comparison before modifying validation code. Record the deployed artifact identity and exact payload in any future update. Do not log tokens or external properties while collecting diagnostics.

