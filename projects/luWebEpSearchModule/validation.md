# Validation

## DTO cascade

The parameter request validation path is:

```text
ParameterJsonRequest
  -> @Valid filters
  -> Filters
  -> @ValidQueryType queryTypes
  -> QueryTypeValidator
```

`ParameterJsonRequest` also has `@ValidSearchCriteria`, `@Min(0)` for `page`, and `@Min(1)` for `count`. `Filters` has `@ValidQueryType` and an additional `@NotNull` constraint.

## Execution

`InternalSearchService` explicitly calls `BeanValidationUtils.validate(request)`. JAX-RS annotations alone are not the only validation entry point. `BeanValidationUtils` creates a singleton validator through `Validation.buildDefaultValidatorFactory()`, converts failures to `BadRequestException`, and processes only the first item from the violation set.

The project uses Hibernate Validator `5.1.3.Final` and validation API `1.1.0.Final`. Focused behavior is covered by `BeanValidationUtilsTest`.

## Rules confirmed locally

- `QueryTypeValidator` is invoked for invalid query types and produces a `ConstraintViolation`.
- The diagnostic property path is `filters.queryTypes`; the annotation is `ValidQueryType`.
- Null or empty `queryTypes` collections are accepted; null elements and values that are not `QueryType` are rejected.
- `SearchCriteriaValidator` accepts nonblank `code` or at least one nonblank `nameVariants` entry.

## Diagnostic interpretation

A missing message in application output does not prove that validation did not run because only the first violation is exposed by `BeanValidationUtils`. For DEV discrepancies, compare the request payload, deployed WAR, `target/classes`, classloader, and `CodeSource` before changing the validator. See `investigations/valid-query-type-dev.md` and the `/debug/query-type-validation` diagnostic endpoint.

