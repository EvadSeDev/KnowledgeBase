# Investigation: Swagger 1.5.19

## Problem

Determine the project’s Swagger generation behavior and whether the documented `1.5.19` version is an actual dependency/runtime constraint.

## Diagnostics performed

- Inspected `SearchApi`, `InternalSearchService`, and `DebugService` annotations.
- Checked the available `pom.xml` dependency declarations and project documentation.
- Compared generated-documentation expectations with custom Bean Validation annotations.

## Findings

- The source uses legacy `io.swagger.annotations.*` with Jersey 1.x.
- Custom constraints such as `@ValidQueryType` are not automatically represented by Swagger.
- Generated Example Values may not reflect the nested JSON request DTO.
- The exact Swagger `1.5.19` version is not confirmed by the inspected POM or available project documentation.

## Conclusion

Treat the project as using legacy Swagger 1.x behavior, but do not assert the exact `1.5.19` version until `mvn dependency:tree` or the deployed artifact confirms it. Validation rules must be documented manually in annotations/API documentation.

## Follow-up

If exact version behavior matters, capture the dependency tree and deployed Swagger resource, then update this investigation with the artifact coordinates and reproducible output.

