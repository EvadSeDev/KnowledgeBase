# Investigation: `ExternalConfigurationListener`

## Problem

Ensure production startup uses external properties rather than copies bundled into the WAR, and understand why configuration failures occur before normal request processing.

## Diagnostics performed

- Inspected `ExternalConfigurationListener`, `web.xml`, `Dockerfile`, `entrypoint.sh`, `pom.xml`, and `scripts/check-war-config.sh`.
- Checked the expected Tomcat external directory and WAR packaging exclusions.
- Compared startup checks with Helm’s read-only ConfigMap mount.

## Findings

- Required external files are `WebEPSearch.properties` and `WebEPContentUniversalDAOOverride.properties`.
- The expected location is `<catalina.base>/lib/lz/`; DEV uses `/usr/local/tomcat/lib/lz`.
- The listener requires readable, unique `file:` resources at the expected canonical paths and rejects bundled `WEB-INF/classes` resources.
- `entrypoint.sh` checks existence, readability, and non-empty content before Tomcat starts.
- `verify` runs the WAR gate; `check-war-config.sh` also scans dependency JARs.
- `SearchServiceEnv.properties` is statically used by `DebugService` but is not checked by this listener.

## Conclusion

This listener enforces source and location of two external files; it is unrelated to Bean Validation and does not deliver configuration. A successful health probe confirms application startup only, not downstream Solr/API availability.

## Follow-up

For a startup failure, inspect `catalina.base`, mounted files, classloader resource URLs, WAR contents, and dependency JARs. Treat ConfigMap changes as rollout events; live reload is not supported.

