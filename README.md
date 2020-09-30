
## Kustomize Usage ##

Reference: https://github.com/kubernetes-sigs/kustomize/

### Generate Yaml files ###

Make sure:

* crc 4.5 is running.
* tekton-openshift fullstackpipeline has created dpd project and has successfully deployed dpd application.

From folder: dpd-kustomize

* oc create deployment drug-search-tailwind --image=image-registry.openshift-image-registry.svc:5000/dpd/drug-search-tailwind:latest --dry-run=true -o yaml > base/web-deployment.yaml

* oc expose deployment drug-search-tailwind --port=8080 --target-port=8080 --dry-run=true -o yaml > base/web-service.yaml

* oc expose service/drug-search-tailwind --dry-run=true -o yaml > base/web-route.yaml

To generate base YAML:

* oc kustomize base > generated/base-drug-search.yaml

Or directly apply YAML:

* oc kustomize base | oc create -f -

To test deploying to development: 

* oc kustomize overlays/development | oc apply -f -
