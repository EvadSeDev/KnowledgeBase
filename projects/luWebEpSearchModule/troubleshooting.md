# Troubleshooting index

Use this document to choose the right investigation before collecting new evidence. Keep detailed logs, stacktraces, payloads, and experiment history in the linked investigation file or daily notes.

## Validation discrepancies

Start with `validation.md` and `investigations/valid-query-type-dev.md`. Confirm the exact request payload, the explicit `BeanValidationUtils.validate` call, the deployed WAR, `target/classes`, classloader, and `CodeSource`. `/debug/query-type-validation` reports the active validator and validation path, but intentionally returns HTTP 200 for diagnostic failures.

## External configuration and startup

Start with `deployment.md` and `investigations/external-configuration-listener.md`. Check `<catalina.base>/lib/lz/`, the two required external properties, file readability, canonical paths, classloader resource URLs, WAR exclusions, and dependency JAR contents. Remember that `ExternalConfigurationListener` validates location and source; it does not provision configuration.

## Build and archive failures

Use the repository project README and `deployment.md`. Tests are skipped unless `-DskipTests=false` is supplied. Run `mvn verify`, not only `mvn package`, because the archive gate runs during `verify`. On Windows, Bash and `unzip` may require Git Bash, WSL, or an adapted command environment.

## Swagger/API documentation mismatches

Start with `swagger.md` and `investigations/swagger-1.5.19.md`. Verify the actual DTO, endpoint annotations, and dependency tree. Legacy Swagger does not infer custom Bean Validation constraints and generated examples may not match the nested request structure.

## Logic-search behavior

Read `README_LogicSearchRegressionTests.md` in the repository before treating a query difference as a regression. The tests characterize current `q`/`fq`, NOT, boost, phrase-distance, ordering, and synonym behavior; some checks require a live Solr instance and debug/explain output.

## Security during diagnostics

Do not expose `/debug/env-properties` publicly and do not copy credentials, tokens, rendered ConfigMaps, or production properties into investigation files. Sanitize logs and payloads before adding them to the Knowledge Base.

