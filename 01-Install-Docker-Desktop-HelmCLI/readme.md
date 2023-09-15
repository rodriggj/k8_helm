# K8 Helm Course

# Resources
- [ ] Main Course Repo [here](https://github.com/stacksimplify/helm-masterclass)
- [ ] Course Presentation Slides [here](https://github.com/stacksimplify/helm-masterclass/tree/main/course-presentation)
- [ ] Course Helm Charts - Part 1 [here](https://github.com/stacksimplify/helm-charts)
- [ ] Course Helm Charts - Part 2 [Here](https://github.com/stacksimplify/helm-charts-repo)

# Environment Setup
- [ ] Setup `Docker Desktop` and `Helm CLI` [here](https://github.com/stacksimplify/helm-masterclass/tree/main/01-Install-Docker-Desktop-and-HelmCLI)

# Deploy Sample App & Test K8 Cluster
1. Navigate to the following location and deploy the sample application [here](https://github.com/stacksimplify/helm-masterclass/tree/main/01-Install-Docker-Desktop-and-HelmCLI)

2. In the `01-Install-Docker-Desktop-and-HelmCLI` directory will be a subdirectory called `kube-manifests`, which contain a _Deployment_ & a _Service_ manifest. You will need these files locally. Either clone the repo or copy these files to your local.

3. Change directories to the `01-Install-Docker-Desktop-HelmCLI` directory and run the following command: 
```s
kubectl apply -f kube-manifests/
```

> You should see in the console a message that indicates that both the _Deployment_ & _Service_ were creaeted.

```s
gabrrodriguez@US-NF9V9G1605 01-Install-Docker-Desktop-HelmCLI % kubectl apply -f kube-manifests/
deployment.apps/myapp1-deployment created
service/myapp1-nodeport-service created
```

4. Now run the following command to get the _Deployment_ details
```s
kubectl get deploy
```

> You should see the following in the console: 
```s
gabrrodriguez@US-NF9V9G1605 01-Install-Docker-Desktop-HelmCLI % kubectl get deploy
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
myapp1-deployment   2/2     2            2           2m16s
```

5. You can now also see the pod details by running the following command: 
```s
kubectl get pods
```

> Should result in something similar to the following: 

```s
gabrrodriguez@US-NF9V9G1605 01-Install-Docker-Desktop-HelmCLI % kubectl get pods
NAME                                 READY   STATUS    RESTARTS   AGE
myapp1-deployment-77dddf88c5-9wzwk   1/1     Running   0          3m21s
myapp1-deployment-77dddf88c5-jgrsl   1/1     Running   0          3m21s
```

6. Now we can also see the _Service_ details by running the following command:

```s
kubectl get svc
```

> You should see a console output similar to the following. You can see that a _NodePort_ service is being used and the nodeport is 80 and the Service port is 31300.

```s
gabrrodriguez@US-NF9V9G1605 01-Install-Docker-Desktop-HelmCLI % kubectl get svc
NAME                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes                ClusterIP   10.96.0.1       <none>        443/TCP        46m
myapp1-nodeport-service   NodePort    10.98.137.217   <none>        80:31300/TCP   4m33s
```

7. Now you can open a browser session and navigate to `localhost:31300` and you should see a UI displayed for your application.

8. Finally, now that we've validated that the `Docker Desktop` and `Kubernetes` single-node cluster is running, we can now delete the resources created. You can do this by running the following command: 

```s
kubectl delete -f kube-manifests/
```

> You should see a console output similar to the following. If you run `get nodes, deployment, or svc` again you will see that no resourcs are available.

```s
gabrrodriguez@US-NF9V9G1605 01-Install-Docker-Desktop-HelmCLI % kubectl delete -f kube-manifests 
deployment.apps "myapp1-deployment" deleted
service "myapp1-nodeport-service" deleted
```

Congrats.

-------

# Download and Install Helm

1. Install `helm`, package manager for kubernetes. See documentation [here](https://helm.sh/)

2. Once `helm` is installed verify the env configuration by running the following command: 

```s 
helm env
```

> Results in something like this... 

```s
gabrrodriguez@US-NF9V9G1605 k8_helm % helm env
HELM_BIN="helm"
HELM_BURST_LIMIT="100"
HELM_CACHE_HOME="/Users/gabrrodriguez/Library/Caches/helm"
HELM_CONFIG_HOME="/Users/gabrrodriguez/Library/Preferences/helm"
HELM_DATA_HOME="/Users/gabrrodriguez/Library/helm"
HELM_DEBUG="false"
HELM_KUBEAPISERVER=""
HELM_KUBEASGROUPS=""
HELM_KUBEASUSER=""
HELM_KUBECAFILE=""
HELM_KUBECONTEXT=""
HELM_KUBEINSECURE_SKIP_TLS_VERIFY="false"
HELM_KUBETLS_SERVER_NAME=""
HELM_KUBETOKEN=""
HELM_MAX_HISTORY="10"
HELM_NAMESPACE="default"
HELM_PLUGINS="/Users/gabrrodriguez/Library/helm/plugins"
HELM_REGISTRY_CONFIG="/Users/gabrrodriguez/Library/Preferences/helm/registry/config.json"
HELM_REPOSITORY_CACHE="/Users/gabrrodriguez/Library/Caches/helm/repository"
HELM_REPOSITORY_CONFIG="/Users/gabrrodriguez/Library/Preferences/helm/repositories.yaml"
```