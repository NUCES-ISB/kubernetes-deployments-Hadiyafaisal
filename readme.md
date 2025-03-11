This repository contains a Kubernetes deployment for a Flask web application connected to a PostgreSQL database using Minikube.
Ensure Minikube is running:
minikube start
docker build -t hadiya671/flask-app:v1 ./app
docker push hadiya671/flask-app:v1
kubectl apply -f manifests/configmap/
kubectl apply -f manifests/secret/
kubectl apply -f manifests/deployment/
kubectl apply -f manifests/service/
kubectl get pods
kubectl get services
minikube service flask-service
kubectl scale deployment flask-deployment --replicas=4
kubectl scale deployment flask-deployment --replicas=2
kubectl get pods

kubectl get all
NAME                                      READY   STATUS             RESTARTS   AGE
pod/flask-deployment-75f877f65c-sjdng     0/1     ImagePullBackOff   0          6m41s
pod/flask-deployment-c8fd477d5-v7spr      1/1     Running            0          18m
pod/flask-deployment-c8fd477d5-wtxzw      1/1     Running            0          18m
pod/postgres-deployment-8c87d96c9-v574n   1/1     Running            0          6m3s

NAME                       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/flask-app          NodePort    10.104.224.160   <none>        5000:30691/TCP   69m
service/flask-service      NodePort    10.96.219.144    <none>        80:30007/TCP     100m
service/kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP          135m
service/postgres           ClusterIP   10.97.47.104     <none>        5432/TCP         70m
service/postgres-service   ClusterIP   10.105.28.171    <none>        5432/TCP         101m

NAME                                  READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/flask-deployment      2/2     1            2           18m
deployment.apps/postgres-deployment   1/1     1            1           15m

NAME                                             DESIRED   CURRENT   READY   AGE
replicaset.apps/flask-deployment-75f877f65c      1         1         0       6m41s
replicaset.apps/flask-deployment-7947b8cbbd      0         0         0       6m42s
replicaset.apps/flask-deployment-c8fd477d5       2         2         2       18m
replicaset.apps/flask-deployment-cbb88498c       0         0         0       18m
replicaset.apps/postgres-deployment-5474ff957d   0         0         0       6m15s
replicaset.apps/postgres-deployment-58b75984cd   0         0         0       14m
replicaset.apps/postgres-deployment-7dc554b5d8   0         0         0       15m
replicaset.apps/postgres-deployment-8c87d96c9    1         1         1       6m3s
replicaset.apps/postgres-deployment-d9487597d    0         0         0       6m6s


kubectl scale deployment flask-deployment --replicas=2
kubectl get pods
deployment.apps/flask-deployment scaled
NAME                                  READY   STATUS         RESTARTS   AGE
flask-deployment-75f877f65c-pkx9d     0/1     Terminating    0          17s
flask-deployment-75f877f65c-sjdng     0/1     ErrImagePull   0          115s
flask-deployment-c8fd477d5-22h64      1/1     Terminating    0          17s
flask-deployment-c8fd477d5-v7spr      1/1     Running        0          13m
flask-deployment-c8fd477d5-wtxzw      1/1     Running        0          13m
postgres-deployment-8c87d96c9-v574n   1/1     Running        0          77s


