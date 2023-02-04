# Helm

Helm makes it real easy to play around with stuff in kubernetes.

## Resources

helm link
helm documentation link

## Tips for testing Helm template changes in projects

Using configmap-nginx for project, an example.

Prior to making changes to a template, should be able to:
  * Spin up the k8s pods and have them all running successfully.
  * Do `helm ls -n project` to see the deployed chart for the project
  * Run `helm lint helm -n project` (while in top-level of repo)
  * Run `helm show values helm -n project` (while in top-level of repo)
  * Able to get sensible results on the website / rails pod from:
    * /config
    * /feature-flags/[domain.com].json
    * /styles
    * /logo

Make changes to the template. Then do the same commands from above and confirm everything still runs successfully and appears correct.

## Tips for messing with Helm to get more experience with it

If you want to play around with helm to get a better feeling for it,
you can generate a skeleton by going to some (preferably empty) folder
and running "helm create [some-name-for-the-chart]"
then you can see it will generate all the helm templates and whatnot
you can run "helm install --dry-run [name-your-deployment] [the-chart-name-you-set]/"
and it will evaluate just like it does in run-app or in gitlab-ci.yaml

--dry-run generates the manifests like helm install normally would, but then doesn't actually run the deployment

you can just as easily go ahead and run the deployment by leaving out --dry-run
then with you run "helm ls" you will see your deployment (named whatever you set for [name-your-deployment])
and you can interact with whatever kubernetes objects your templates created
and remove the deployment with "helm uninstall [the-deployment-name-you-created]"

generate a skeleton
```
~/workspace/test/helm-test Lauren$ helm create testy-mctestface
Creating testy-mctestface
```

check out what that generated
```
~/workspace/test/helm-test Lauren$ ll
total 0
drwxr-xr-x   3 Lauren  FOLDER\Domain Users    96 Sep 15 13:24 .
drwxr-xr-x@ 57 Lauren  FOLDER\Domain Users  1824 Sep 15 13:23 ..
drwxr-xr-x   7 Lauren  FOLDER\Domain Users   224 Sep 15 13:24 testy-mctestface

~/workspace/test/helm-test Lauren$ ll testy-mctestface/
total 24
drwxr-xr-x   7 Lauren  FOLDER\Domain Users   224 Sep 15 13:24 .
drwxr-xr-x   3 Lauren  FOLDER\Domain Users    96 Sep 15 13:24 ..
-rw-r--r--   1 Lauren  FOLDER\Domain Users   349 Sep 15 13:24 .helmignore
-rw-r--r--   1 Lauren  FOLDER\Domain Users  1107 Sep 15 13:24 Chart.yaml
drwxr-xr-x   2 Lauren  FOLDER\Domain Users    64 Sep 15 13:24 charts
drwxr-xr-x  10 Lauren  FOLDER\Domain Users   320 Sep 15 13:24 templates
-rw-r--r--   1 Lauren  FOLDER\Domain Users  1809 Sep 15 13:24 values.yaml
```

install it
```
~/workspace/test/helm-test Lauren$ helm install my-instance testy-mctestface/
NAME: my-instance
LAST DEPLOYED: Wed Sep 15 13:32:34 2021
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=testy-mctestface,app.kubernetes.io/instance=my-instance" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:80
```

check out the deployed objects
```
~/workspace/test/helm-test Lauren$ helm ls
NAME           NAMESPACE    REVISION    UPDATED                                 STATUS      CHART                     APP VERSION
my-instance    default      1           2021-09-15 13:32:34.799509 -0500 CDT    deployed    testy-mctestface-0.1.0    1.16.0
~/workspace/test/helm-test Lauren$ kubectl get deployments
NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
my-instance-testy-mctestface   1/1     1            1           18s
```

cleanup
```
~/workspace/test/helm-test Lauren$ helm uninstall my-instance
release "my-instance" uninstalled
```

