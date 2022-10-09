# Introduction
- revision history : back to version
- consistency : tweek the cluster directly caused inconsistency
- helm is packaging manager, charts are package.
- helm upgrade apache bitnami/apache --namespace=prod
- helm unistall apache
# Advantage:
- helm pull chart and do the configuration in a single commad
- revision 1 and revison 2 revert thing
- dynamic configuration
- life cycle hooks , backup ,
- security, hash key
# Commands
- bitnami.com/stacks/helm
- helm repo list
- helm repo add bitnami https://charts.bitnami.com/bitnami
- helm search repo apache
- helm search repo apache --versions
- helm list --namespace prod
- helm unistall mydb
### Upgrade ###
- help repo update
- helm status mydb
- helm upgrade mydb bitnami/mysql --values /home/sam/UI/helm/values.yml      
- helm upgrade mydb bitnami/mysql --resue-values
### Records ###
- helm keeps secret for each upgrade -- kubectl get secrets
#### WorkFLow ###
- load the chart and its dependencies
- parse the deafult values.yml overide --values 
- generate the yaml
- parse yaml to kube object and validate
- generate yaml and send to kube
### --dry-run ###
- helm install mydb bitnami/mysql --values /home/sam/UI/helm/values.yml --dry-run
- debugging process best
### template ###
- helm template mydb bitnami/mysql --values /home/sam/UI/helm/values.yml
### helm get ###
- helm get notes mydb
- helm get values mydb
- helm get manifest mydb
### helm history ###
- helm history myweb
### helm rollback ###
- helm rollback myweb 1
- helm uninstall myweb --keep-history {u can rollback with keep history}
### helm-upgrade-install ###
- helm upgrade --install myweb bitnami/apache --namespace prod --create-namespace
### helm-generate-name ###
- helm install  bitnami/apache --generate-name
### other ###
- helm install  bitnami/apache --generate-name --wait --timeout 10m10s 
- helm install  bitnami/apache --generate-name --atomic --timeout 10m10s {previous release used after wait failure}
- helm upgrade myweb bitnami/apache--force, --cleanup-on-failure

# charts 
- helm create firstchart {by deafault uses nginx chart}
- helm install firstapp firstchart/
- export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=firstchart,app.kubernetes.io/instance=firstapp" -o jsonpath="{.items[0].metadata.name}")  export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")  echo "Visit http://127.0.0.1:8080 to use your application"   kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT 
# package
- helm package firstchart
- helm package firstchart -u,-d /home/sam
# lint
- helm lint firstchart
- https://siweheee.medium.com/deploy-your-programs-onto-minikube-with-docker-and-helm-a68097e8d545




