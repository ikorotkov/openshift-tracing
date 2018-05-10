# openshift-tracing
Jaeger + Elasticsearch
### DEPLOY ELASTICSEARCH
```sh
oc new project jaeger #Create a new project
oc adm policy add-scc-to-user privileged -z default #For run initContainer with as root
oc create -f openshift-tracing/elastic-tmp.yml -n jaeger #Add the template to project jaeger or other to OpenShift
oc 
```
   
