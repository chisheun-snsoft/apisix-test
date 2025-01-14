# apisix-helm

apisix -> value file
ingress-apisix - > for kubectl apply

Before start deploy, we need have ebs plugin at eks node and ebscsi driver policy

1. we need to place these two file in a git that you want, then go to ingress-apisix -> apisix-helm.yaml change the repoURL to the git {also can change the valueFiles}
2. edit ingress-apisix -> apisix-route.yaml metadataName, serviceName, servicePort to the service that you want {For the plugins if no using just enable: false}
4. kubectl apply -f apisix-helm.yaml, apisix-etcd is the main of apisix, so need to wait of this pods running
5. after all apisix pod running, kubectl apply -f apisix-route.yaml
6. kubectl describe apisixroute -n {namespace} {metadataName} to see the status
7. If all good, just kubectl get svc -n ingress-apisix to get the service, curl it and you will get the service output that you target at the route.


Now we using 3.9.1 version
https://apisix.apache.org/docs/apisix/plugins/prometheus/

https://artifacthub.io/packages/helm/apisix/apisix?modal=values&path=apisix.prometheus

https://github.com/apache/apisix/blob/master/conf/config.yaml.example
