# luWebEpSearchModule

## Scope and source of truth

- This is a Java 8-compatible WAR (`ua.lz.ep:luWebEpSearchModule`) for Tomcat 7.
- Read the detailed project documents before changing code: `README.md`, `architecture.md`, `validation.md`, `deployment.md`, `swagger.md`, and `troubleshooting.md`.
- Use `workflow.md` for the Knowledge Base update process and specialized AI prompt templates.
- Completed investigations live under `investigations/`; the historical daily report is `../../daily/2026-10-27.md`.

## How to use this Knowledge Base

Before starting any task, read:

`KnowledgeBase/projects/luWebEpSearchModule/AGENTS.md`

Use this document as the primary source of project knowledge, including:

- architecture;
- validation flow;
- deployment specifics;
- external configuration;
- debugging notes;
- investigation history;
- project conventions.

## Non-negotiable project facts

- `InternalSearchService` explicitly calls `BeanValidationUtils.validate`; the validation cascade is `ParameterJsonRequest -> @Valid Filters -> @ValidQueryType -> QueryTypeValidator`.
- `WebEPSearch.properties` and `WebEPContentUniversalDAOOverride.properties` must come from `<catalina.base>/lib/lz/`, never from bundled `WEB-INF/classes`.
- `mvn verify`, not only `mvn package`, runs the WAR configuration gate. Tests are skipped unless `-DskipTests=false` is supplied.
- `/debug/query-type-validation` is useful for classloader/CodeSource diagnostics; `/debug/env-properties` can expose sensitive configuration and must remain protected.
- Logic-search tests characterize current behavior, not necessarily desired business semantics. Do not change `q`/`fq`, phrase distance, NOT, boost, or synonym behavior without the relevant regression/runtime checks.
- Do not commit credentials, rendered ConfigMaps, production properties, or tokens.
- For every task, preserve the existing architecture, validation flow, deployment assumptions, and integration contracts.

## Commands

```text
mvn clean verify -DskipTests=false
mvn clean verify -DskipTests=false -Dtest=ExternalConfigurationListenerTest,ConfigurationPackagingTest,EntrypointConfigurationTest,SemantrumServiceImplTest
bash scripts/check-war-config.sh target/luWebEpSearchModule.war
bash scripts/test-helm-config.sh
```

## Investigation index

- `investigations/valid-query-type-dev.md` — DEV validation discrepancy, evidence, and classloader hypotheses.
- `investigations/swagger-1.5.19.md` — Swagger 1.x investigation status and evidence limits.
- `investigations/external-configuration-listener.md` — external file/resource invariants and WAR/startup checks.
- `investigations/wsl-build-issues.md` — WSL investigation status; do not treat unverified workarounds as project facts.
- `../../daily/2026-10-27.md` — original detailed validation and deployment investigation.
