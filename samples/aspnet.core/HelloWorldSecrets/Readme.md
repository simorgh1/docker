#### HelloWorld aspnet.core with ConfigMap

This sample reads the appsettings.json and secrets from kubernetes ConfigMap
Application configuration is stored in the config map, and passwords are stored in the secrets, both item types are set to environment variables. passwords are also mounted into a readonly mountPath just as example.

Step 1: Build the docker image

```
PS C:\HellowroldSecrets\src> docker build -t helloworld-secrets:dev .

```

Step 2: Deploy the appsettings.json to kubernetes ConfigMap:

```
PS C:\HellowroldSecrets\.k8s> kubectl create cm app-configuration --from-file=appsettings.json
PS C:\HellowroldSecrets\.k8s> kubectl describe cm app-configuration
```

Step 3: Create the application secrets:

```
PS: C:\HellowroldSecrets\src> kubectl create secret generic db-passwords --type=string --from-literal=db-app-password='app-password' --from-literal=db-admin-password='db-admin-password'
PS: C:\HellowroldSecrets\src> kubectl describe secret db-passwords
```

Step 4: Apply the deployment:

```
PS C:\HellowroldSecrets\.k8s> kubectl create -f .\helloworld.secrets.deployment.yaml --save-config
```

Step 5: port-forward the pod and open the application:

```
PS C:\HellowroldSecrets> kubectl get pod
NAME                          READY   STATUS    RESTARTS   AGE
helloworld-7b749c5d74-7knk7   1/1     Running   0          11m

PS C:\HellowroldSecrets> kubectl port-forward helloworld-7b749c5d74-7knk7 8080
```

Then goto: http://localhost:8080

#### Cleanup

Remove the deployment the related ConfigMap

```
PS C:\HellowroldSecrets\.k8s> kubectl delete -f .\Hellowrold.secrets.deployment.yaml
PS C:\HellowroldSecrets\.k8s> kubectl delete cm app-configuration
PS C:\HellowroldSecrets\.k8s> kubectl delete secret db-passwords

```