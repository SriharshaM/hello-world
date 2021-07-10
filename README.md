kubectl config current-context
kubectl config view
kubectl version -o json

root@ip-10-0-0-37:~# kubectl proxy
Starting to serve on 127.0.0.1:8001
http://a92e40994d2c04d71a6e6f9a5329e095-c2e743d3f78019c1.elb.ap-south-1.amazonaws.com/

kubectl get nodes

oot@ip-10-0-0-37:~# kubectl get po -n wrdm
NAME                                             READY   STATUS             RESTARTS   AGE
deploy-wrdm-base-authmgmt-5775f66c68-cmvxz       1/1     Running            0          114d
deploy-wrdm-base-authmgmt-5775f66c68-g9qsh       1/1     Running            0          114d
deploy-wrdm-base-authmgmt-5775f66c68-w4ldl       1/1     Running            0          114d
deploy-wrdm-base-awsses-797c4654d7-sfs6x         1/1     Running            0          114d
deploy-wrdm-base-notifmgmt-7dbd5645fc-54pkm      1/1     Running            0          114d
deploy-wrdm-base-sitemgmt-84f54cc7c9-xjnrq       1/1     Running            0          114d
deploy-wrdm-base-usermgmt-6cc5c499b8-s4rp6       1/1     Running            0          114d
deploy-wrdm-beapi-dashboardmgmt-768df855-lk5fs   0/1     CrashLoopBackOff   40         114d
deploy-wrdm-beapi-devicemgmt-85c7d58d8b-rv9k7    0/1     CrashLoopBackOff   40         114d
deploy-wrdm-frontend-6bf8d897f9-4xdfl            1/1     Running            0          114d
mysql-0                                          2/2     Running            0          3h13m

oot@ip-10-0-0-37:~# kubectl get nodes
NAME                                        STATUS   ROLES    AGE    VERSION
ip-10-0-0-204.ap-south-1.compute.internal   Ready    <none>   175d   v1.20.4
ip-10-0-0-37.ap-south-1.compute.internal    Ready    master   175d   v1.20.4

kubectl get svc -n wrdm -o wide

To connect to mysql pod
kubectl run -n wrdm -it --rm --image=mysql:latest --restart=Never mysql-client -- mysql -h mysql-0.mysql -u wrdmuser -p mrdws3cr3t

root@ip-10-0-0-37:~# kubectl get pods -n wrdm
NAME                                             READY   STATUS             RESTARTS   AGE
deploy-wrdm-base-authmgmt-5775f66c68-cmvxz       1/1     Running            0          115d
deploy-wrdm-base-authmgmt-5775f66c68-g9qsh       1/1     Running            0          115d
deploy-wrdm-base-authmgmt-5775f66c68-w4ldl       1/1     Running            0          115d
deploy-wrdm-base-awsses-797c4654d7-sfs6x         1/1     Running            0          115d
deploy-wrdm-base-notifmgmt-7dbd5645fc-54pkm      1/1     Running            0          115d
deploy-wrdm-base-sitemgmt-84f54cc7c9-xjnrq       1/1     Running            0          115d
deploy-wrdm-base-usermgmt-6cc5c499b8-s4rp6       1/1     Running            0          115d
deploy-wrdm-beapi-dashboardmgmt-768df855-lk5fs   0/1     CrashLoopBackOff   70         115d
deploy-wrdm-beapi-devicemgmt-85c7d58d8b-rv9k7    0/1     CrashLoopBackOff   69         115d
deploy-wrdm-frontend-6bf8d897f9-4xdfl            1/1     Running            0          115d
mysql-0                                          2/2     Running            0          5h49m


root@ip-10-0-0-37:~/spinnaker-operator# kubectl get svc -n spinnaker-operator -o wide
NAME                         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE     SELECTOR
spinnaker-operator           ClusterIP   10.96.238.177   <none>        443/TCP             8m32s   name=spinnaker-operator
spinnaker-operator-metrics   ClusterIP   10.96.233.21    <none>        8686/TCP,8383/TCP   8m27s   name=spinnaker-operator

oot@ip-10-0-0-37:~/spinnaker-operator/deploy/operator/helm# kubectl get deploy -n spinnaker -o yaml
apiVersion: v1
items: []
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""
root@ip-10-0-0-37:~/spinnaker-operator/deploy/operator/helm# kubectl get deploy -n spinnaker-controller -o yaml
apiVersion: v1
items: []
kind: List
metadata:
  resourceVersion: ""
  selfLink: ""

  Use 'kubectl describe pod/spinnaker-operator-74b445d4ff-zzhf8 -n spinnaker-operator' to see all of the containers in this pod.



  To set up krew in kubectl

  https://krew.sigs.k8s.io/docs/user-guide/setup/install/

  Follow the above commands and reboot the VM

  after setting up krew:  to install kubectx to switch namespaces
  kubectl krew install ctx
kubectl krew install ns

Enter
kubectl ns - To get the names of the namespaces and switch to them

oot@ip-10-0-0-37:~# kubectl get deployments --all-namespaces
NAMESPACE              NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
default                jenkins-operator                  1/1     1            1           9h
ingress-nginx          ingress-nginx-controller          1/1     1            1           171d
kube-system            coredns                           2/2     2            2           178d
kube-system            metrics-server                    1/1     1            1           170d
kubernetes-dashboard   dashboard-metrics-scraper         1/1     1            1           170d
kubernetes-dashboard   kubernetes-dashboard              1/1     1            1           170d
monitoring             grafana                           1/1     1            1           171d
monitoring             jenkins-operator                  1/1     1            1           11m
monitoring             prometheus-deployment             1/1     1            1           171d
spinnaker-operator     spinnaker-operator                1/1     1            1           5h31m
wrdm                   deploy-wrdm-base-authmgmt         3/3     3            3           177d
wrdm                   deploy-wrdm-base-awsses           1/1     1            1           175d
wrdm                   deploy-wrdm-base-notifmgmt        1/1     1            1           175d
wrdm                   deploy-wrdm-base-sitemgmt         1/1     1            1           177d
wrdm                   deploy-wrdm-base-usermgmt         1/1     1            1           175d
wrdm                   deploy-wrdm-beapi-dashboardmgmt   0/1     1            0           175d
wrdm                   deploy-wrdm-beapi-devicemgmt      0/1     1            0           175d
wrdm                   deploy-wrdm-frontend              1/1     1            1           178d


If we want to delete a pod then we have to delete the deployments
root@ip-10-0-0-37:~# kubectl delete -n monitoring deployment jenkins-operator
deployment.apps "jenkins-operator" deleted

If the deployment is in default namespace:
root@ip-10-0-0-37:~# kubectl delete deployment jenkins-operator
deployment.apps "jenkins-operator" deleted
