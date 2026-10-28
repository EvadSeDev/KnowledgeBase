# Architecture

## Runtime bootstrap

`src/main/webapp/WEB-INF/web.xml` starts `ExternalConfigurationListener` and `EpModuleServletContextListener`, then maps `ua.lz.ep.filter.EpModuleServletContainer` to `/service/*`. `RootFilter` and `EncodingFilter` wrap requests. Jersey scans the service, error, and Swagger packages.

## Modules and boundaries

- `SearchService` is the main REST façade for ordinary, public, paragraph, single-document, parameter, logical, suggestion, analytics, and specialized endpoints.
- `SearchBallsService` owns the `/search/balls` workflow and document connections.
- `DebugService` exposes protected diagnostics below `/debug`.
- `SearchModule` and `SearchBallsModule` create module contexts. `ModuleSearch*.xml` wires query templates, DAO/access checkers, executors, modifiers, and formatters.
- `lzEpMain`, `lzUniversalDAO`, and related internal artifacts provide part of the search backend. Reflection and dependency-provided templates mean this module does not contain the whole runtime behavior.

## Main parameter-search flow

```text
HTTP request
  -> ParameterJsonRequest
  -> InternalSearchService
  -> BeanValidationUtils.validate(request)
  -> InternalParameterRequestUtils
  -> searchParameter or searchParameterWithLogicOperators (q_logic)
  -> query template / DAO / Solr
  -> access checks and result formatting
  -> dictionary lookups for facets
  -> JSON response
```

Trace the endpoint contract in `SearchApi` and the implementation in `InternalSearchService` before changing DTOs or routing. A change to a query template or dependency version can alter runtime behavior without a corresponding local Java change.

## External boundaries

Solr is reached through the DAO/query-template layer and the Envoy sidecar in Kubernetes. Similar questions, spell correction, Semantrum, accountant/history, currency/verdictum, synonyms, and dictionary services are configured external integrations. Their auth headers, response conversion, and role-based routing are part of the contract.

