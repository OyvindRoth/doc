# Migrating from Naisd

## 1. Converting the manifest

Your nais manifest, commonly known as `nais.yaml`, needs to be converted from its current format into the new format.

The old format looks like this:

```text
image: navikt/nais-testapp
team: teamName
port: 8080
(...)
```

The new format looks like this. Check out [in depth](https://github.com/nais/doc/tree/6b83252d1028906af09fbfdb0a25cb3c3e07a3c4/legacy/in-depth/nais-manifest.md) for a more complete list.

```text
apiVersion: nais.io/v1alpha1
kind: Application
metadata:
  name: nais-testapp
  namespace: default
  labels:
    team: teamName
spec:
  image: navikt/nais-testapp:1.2.3
  port: 8080
(...)
```

Follow the checklist to complete the migration:

* [ ] Use the `apiVersion`, `kind`, `metadata` and `spec` fields.
* [ ] Include the version of your Docker container in the `.spec.image` field.
* [ ] `healthcheck` has been replaced by top-level `liveness` and `readiness` fields.
* [ ] The `redis` field has been removed.
* [ ] The `alerts` field has been replaced with the [Alert resource](https://github.com/nais/doc/tree/6b83252d1028906af09fbfdb0a25cb3c3e07a3c4/legacy/observability/alerts.md).
* [ ] The `ingress` field has been replaced by `ingresses` and need to specified explicitly.
* [ ] Fasit is no longer supported.

## 2. Cluster access

Your converted manifest is a Kubernetes [custom resource](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/), and as such, it needs to be deployed directly to a Kubernetes cluster. This means you need to have `kubectl` access, which in turn requires:

* [ ] [Install and configure kubectl](https://github.com/nais/doc/tree/6b83252d1028906af09fbfdb0a25cb3c3e07a3c4/legacy/basics/access.md)
* [ ] [Create an Azure AD group](https://github.com/nais/doc/tree/6b83252d1028906af09fbfdb0a25cb3c3e07a3c4/legacy/basics/teams.md) for your team, for human access to the cluster

## 3. Deploying applications

See the [Deploy your application](https://github.com/nais/doc/tree/6b83252d1028906af09fbfdb0a25cb3c3e07a3c4/legacy/basics/deploy.md) section.

