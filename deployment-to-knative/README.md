# Show migration of a deployment

## Install Knative Serving

The following commands install Knative Serving in a patched version (0.6.0) alongside a minimal Istio and the openshift ingress controller for Knative Serving.

```
$ export OLM_NAMESPACE="openshift-operator-lifecycle-manager"
$ oc apply -n $OLM_NAMESPACE -f 000-catalog-source.yaml
$ oc get pods -n $OLM_NAMESPACE # until knative serving operator is up
$ oc apply -f 001-install-serving.yaml
$ oc apply -f https://github.com/openshift-knative/knative-openshift-ingress/releases/download/v0.0.4/release.yaml
```

## Demo Prereq

The following installs a small redis cluster needed for the application.

```
$ oc apply -f 002-redis.yaml
```

## Demo deployment

1. Show the contents of 100-guestbook-deployment.yaml
2. Make a point on it being a random application written in PHP, fronted by an nginx and talking to a redis server. Akin to what one might build these days, except it's a guestbook.
3. Quickly go through the needed aspects of the deployment
4. Make a point on how you need a deployment to create the pods, a service to make them generally available via a dns entry and a route to make it externally available.
5. Deploy.
6. Open URL

## Migration

1. Show the contents again.
2. Start by switching the apiversion and kind.
3. Start deleting all the things you don't need.
4. Reapply.
5. Open URL.
6. Make a point on how its hooked up on its own. No manual service or route needed.
7. Migration was super simple, we just deleted a few lines.
8. This will actually scale to 0.