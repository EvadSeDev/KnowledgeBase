# Deployment

## External configuration invariant

The production WAR must not contain:

- `WebEPSearch.properties`;
- `WebEPContentUniversalDAOOverride.properties`.

They must be mounted as external files under `<catalina.base>/lib/lz/`; in DEV the expected directory is `/usr/local/tomcat/lib/lz`. `ExternalConfigurationListener` requires readable, unique `file:` resources at the expected canonical paths and fails startup when the classloader resolves bundled `WEB-INF/classes` copies. It validates the source; it does not deliver the files.

`entrypoint.sh` checks that both files exist, are readable, and are non-empty before starting Tomcat. `Dockerfile` adds the directory to Tomcat `common.loader`.

## Build and archive gates

Maven defaults to `<skipTests>true</skipTests>`. Use `mvn clean verify -DskipTests=false`; `verify` is required because the Antrun execution runs `scripts/check-war-config.sh`. The script checks the WAR and every dependency JAR for the two forbidden properties.

```text
mvn clean verify -DskipTests=false
bash scripts/check-war-config.sh target/luWebEpSearchModule.war
```

## Kubernetes

`K8sConfig/helm/luwebepsearchmodule` deploys a three-replica `StatefulSet`, not a Deployment. The configuration directory is mounted read-only without `subPath`; a ConfigMap checksum triggers rollout when configuration changes. There is no live reload.

An Envoy sidecar exposes local Solr on `127.0.0.1:8983`. Keep StatefulSet ordinal, Solr node ordering, and primary/fallback routing consistent. Health probes use `/luWebEpSearchModule/health.txt` and confirm application startup only, not downstream Solr or API availability.

```text
bash scripts/test-helm-config.sh
docker build -t luwebepsearchmodule:config-check .
```

Deploy image and Helm configuration together: the image expects the external configuration directory and its `common.loader` setup.

