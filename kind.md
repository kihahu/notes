## USING KIND TO TEST LOCAL K8S DEPLOYMENTS
- Install KIND
- Download and install helm 3 from https://github.com/helm/helm/releases
- wget latest archive
- Extract and store it under /usr/local/bin/
### Add Jenkins helm chart repo
- `helm repo add jenkins https://charts.jenkins.io`
### Install Jenkins using helm chart
- `helm install jenkins jenkins/jenkins`
### Accessing Jenkins
1. Get your 'admin' user password by running:
  `kubectl exec --namespace jenkins -it svc/jenkins -c jenkins -- /bin/cat /run/secrets/chart-admin-password && echo`
2. Get the Jenkins URL to visit by running these commands in the same shell:
  echo http://127.0.0.1:8080
  kubectl --namespace jenkins port-forward svc/jenkins 8080:8080
3. Login with the password from step 1 and the username: admin
4. Configure security realm and authorization strategy

### Testing Local Application
- Configure and start KIND with a local registry by using this script.
- Build your application image and tag it and push it to the local registry.
- Build a Jenkins job for your application using a Jenkinsfile.
- Configure the cluster to deploy to in the Jenkinsfile to the localhost KIND cluster

```
sh 'kubectl config use-context lc-jenkins'
sh "helm upgrade -i --debug {service name} {application chart} --version {chart version} --namespace {application namespace} -f {path to yaml file with custom values}"
```

