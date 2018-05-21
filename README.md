# openshift-tracing
Jaeger + Elasticsearch
### DEPLOY ELASTICSEARCH

For example, There is used project "jaeger". You should use any other project name.

```
oc new project jaeger #Create a new project
```
Create new service account for run priveleged container:
```
oc create sa privilegeduser
oc adm policy add-scc-to-user privileged -z privilegeduser #For run initContainer with as root
```
Create Image Streams:
```
oc create -f openshift-tracing/ImageStream/imagestreams-create.yml -n jaeger
```
else use to images directly from other registry and modify them using Dockerfiles (openshift-tracing/ImageStream/Dockerfile-*). It's need for run process as noroot.
  
Create templates Elasticsearch and Jaeger:
```
oc create -f openshift-tracing/elastic-stateful-template.yml -n jaeger
oc create -f openshift-tracing/jaeger-oauth-template-simple.yml -n jaeger
```


else use to images directly from https://registry.centos.org/rhsyseng/elasticsearch or other.

Deploy new application Elasticsearch from template using CLI or WEB interface. Need replacing IMAGE on correct. 

```
oc new-app --template=elasticsearch-template \ -p ELASTIC_DEPLOY_NAME=elasticsearch,IMAGE='<IMAGE>',PRIV_SA=privilegeduser,ELASTIC_MEMORY=512Mi
```

```
oc new-app --template=jaeger-template \ -p IMAGE_PROXY='openshift/oauth-proxy:v1.0.0',JAEGER_SRV_NAME=jaeger,IMAGE_VERSION='1.2',JAEGER_ZIPKIN_SERVICE_NAME=zipkin
```


