# kubernetes-mapreduce

kubectl create -f mapreduce-reduce.yaml
kubectl create -f mapreduce-map.yaml
kubectl create -f mapreduce-master.yaml

kubectl proxy --port=8080 &

## View result

curl http://127.0.0.1:8080/api/v1/namespaces/default/pods/mapreduce-master/proxy/compute\?text\=Hello+world+test+test+test+test+test+test+helo+araara+tttt+dddd+araara+test+hello+hi+ih+ih+ih+hi

## delete resources

### Stop the proxy

ps -ef | grep "kubectl proxy"     

kill -9 PID

### delete kubernetes resources

kubectl get all 

NAME                                      READY   STATUS    RESTARTS   AGE
pod/mapper-0                              1/1     Running   0          26m
pod/mapper-1                              1/1     Running   0          26m
pod/mapper-2                              1/1     Running   0          26m
pod/mapreduce-master                      1/1     Running   0          26m
pod/reducer-0                             1/1     Running   0          26m
pod/reducer-1                             1/1     Running   0          26m
pod/reducer-2                             1/1     Running   0          26m

NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
service/mappers              ClusterIP      None             <none>        8080/TCP         26m
service/mapreduce-master     ClusterIP      10.101.106.200   <none>        8080/TCP         26m
service/reducers             ClusterIP      None             <none>        8080/TCP         26m

NAME                       READY   AGE
statefulset.apps/mapper    3/3     26m
statefulset.apps/reducer   3/3     26m

Then delete all:

kubectl delete service/mappers
...

View docker images:

docker images

Optionally remove all docker images (take care it will really remove all your docker images):

docker rm $(docker ps -aq) 		Remove all images

docker rmi $(docker images -q)
