# DEPLOY REDIS CLUSTER
*Test*

```
# helm install redis -f values.yaml oci://registry-1.docker.io/bitnamicharts/redis -n <NAMESPACE>
```

```
NAME                            READY   STATUS    RESTARTS         AGE
pod/redis-node-0                3/3     Running   0                4h2m
pod/redis-node-1                3/3     Running   0                4h2m
pod/redis-node-2                3/3     Running   0                4h1m

NAME                                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)              AGE
service/redis                       ClusterIP   10.43.84.152    <none>        6379/TCP,26379/TCP   4h2m
service/redis-headless              ClusterIP   None            <none>        6379/TCP,26379/TCP   4h2m
service/redis-master                ClusterIP   10.43.252.159   <none>        6379/TCP             4h2m

NAME                                READY   AGE
statefulset.apps/redis-node         3/3     4h2m
```

**service/redis-master ⇒ Auto point to master node. If master node unhealthy, sentinal auto promote other master node from 1 read replica and service/redis-master will auto pointed to new master node (Using connect for app)**

**"disableCommands" default value is ["FLUSHDB","FLUSHALL"] ⇒ Block FLUSHDB & FLUSHALL command. Replace or set empty list value if want custom or allow all command**
