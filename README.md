# pyroscope-operator

## What this is

This is an Kubernetes operator which codifies operational workflow(s) covering provisioning, scaling up/down, managing and configuring durable profiling data stores

## Dev notes

* This (so far) creates 2 CRD's....(and associated controllers, rbac, etc)

### PyroscopeServer

```yaml
apiVersion: operator.pyroscope.io/v1
kind: PyroscopeServer
metadata:
  name: pyroscopeserver-sample
spec:
  # TODO: Add fields here
```

https://github.com/halcyondude/pyroscope-operator/blob/my-kubebuilder-scaffolding/config/crd/bases/operator.pyroscope.io_pyroscopeservers.yaml

Creating one of these spins up a Server process w/ config covering: cpu, mem, storage, Namespace, Service, and Ingress.

### PyroscopeProfileTarget

```yaml
apiVersion: operator.pyroscope.io/v1
kind: PyroscopeProfileTarget
metadata:
  name: pyroscopeprofiletarget-sample
spec:
  # TODO: Add fields here
```

https://github.com/halcyondude/pyroscope-operator/blob/my-kubebuilder-scaffolding/[…]ig/crd/bases/operator.pyroscope.io_pyroscopeprofiletargets.yamlt

* Contains a label selector that matches pods. For example `app=frontend-ui-thing sha=1234abc`
* causes a [MutatingAdmissionWebhook](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/#mutatingadmissionwebhook) to be created which watches all Pod creations w/ $theLabel . The Webhook inspects the matching pod(s) spec for the entry/run, patching in pyroscope wrappers to the container spec, or otherwise injecting sidecar agent / etc.

### PyroscopeConfig

* This requires more consideration and an influx of context around how Pyroscope will be used.
* (coming soon) <-- I really don't care for this generic name
2-tuple: {PyroscopeServer, PyroscopeProfileTarget}.

## Reconcile func's (empty presently)
* https://github.com/halcyondude/pyroscope-operator/tree/my-kubebuilder-scaffolding/controllers

