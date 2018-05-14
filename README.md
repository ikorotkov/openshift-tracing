# openshift-tracing
Jaeger + Elasticsearch
### DEPLOY ELASTICSEARCH

For example, There is used project "jaeger". You should use any other project name.

```sh
oc new project jaeger #Create a new project
oc create sa privilegeduser #Create new service account for run priveleged container
oc adm policy add-scc-to-user privileged -z privilegeduser #For run initContainer with as root
oc create -f openshift-tracing/elastic-stateful-template.yml -n jaeger #Add the template to project jaeger or other to OpenShift
```

If you need to create Image Stream

```
oc create -f openshift-tracing/elastic-imagestream-create.yml #Create imagestream and add images elasticsearch to project

```

else use to images directly from https://registry.centos.org/rhsyseng/elasticsearch or other.


