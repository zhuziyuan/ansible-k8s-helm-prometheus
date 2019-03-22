## Installation
$ helm install --name prometheus ./prometheus
NAME:   prometheus
LAST DEPLOYED: Thu Mar 21 14:12:59 2019
NAMESPACE: default
STATUS: DEPLOYED

RESOURCES:
==> v1/ConfigMap
NAME                                         DATA  AGE
prometheus-alertmanager  1     2s
prometheus-server        3     2s

==> v1/ServiceAccount
NAME                                               SECRETS  AGE
prometheus-alertmanager        1        2s
prometheus-kube-state-metrics  1        2s
prometheus-node-exporter       1        2s
prometheus-pushgateway         1        2s
prometheus-server              1        2s

==> v1/Service
NAME                                               TYPE       CLUSTER-IP     EXTERNAL-IP  PORT(S)   AGE
prometheus-alertmanager        ClusterIP  10.104.25.189  <none>       80/TCP    2s
prometheus-kube-state-metrics  ClusterIP  None           <none>       80/TCP    1s
prometheus-node-exporter       ClusterIP  None           <none>       9100/TCP  1s
prometheus-pushgateway         ClusterIP  10.106.245.46  <none>       9091/TCP  1s
prometheus-server              ClusterIP  10.103.0.112   <none>       80/TCP    1s

==> v1beta1/Deployment
NAME                                               DESIRED  CURRENT  UP-TO-DATE  AVAILABLE  AGE
prometheus-alertmanager        1        1        1           0          1s
prometheus-kube-state-metrics  1        1        1           0          1s
prometheus-pushgateway         1        1        1           0          1s
prometheus-server              1        1        1           0          1s

==> v1/Pod(related)
NAME                                                             READY  STATUS             RESTARTS  AGE
prometheus-node-exporter-gxg5t               0/1    ContainerCreating  0         1s
prometheus-node-exporter-m6dxx               0/1    ContainerCreating  0         1s
prometheus-alertmanager-b676bc488-g7j7z      0/2    Pending            0         1s
prometheus-kube-state-metrics-7fffc764gtxfb  0/1    ContainerCreating  0         1s
prometheus-pushgateway-7c7f8c5445-v27fm      0/1    ContainerCreating  0         1s
prometheus-server-669b9cd7f-vvh7x            0/2    Pending            0         1s

==> v1/PersistentVolumeClaim
NAME                                         STATUS   VOLUME         CAPACITY  ACCESS MODES  STORAGECLASS  AGE
prometheus-alertmanager  Pending  local-storage  2s
prometheus-server        Pending  local-storage  2s

==> v1beta1/ClusterRole
NAME                                               AGE
prometheus-kube-state-metrics  2s
prometheus-server              2s

==> v1beta1/ClusterRoleBinding
NAME                                               AGE
prometheus-kube-state-metrics  2s
prometheus-server              2s

==> v1beta1/DaemonSet
NAME                                          DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE  NODE SELECTOR  AGE
prometheus-node-exporter  2        2        0      2           0          <none>         1s


NOTES:
The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-server.default.svc.cluster.local


Get the Prometheus server URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9090


The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
prometheus-alertmanager.default.svc.cluster.local


Get the Alertmanager URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9093


The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
prometheus-pushgateway.default.svc.cluster.local


Get the PushGateway URL by running these commands in the same shell:
  export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
  kubectl --namespace default port-forward $POD_NAME 9091

For more information on running Prometheus, visit:
https://prometheus.io/

## Testing
$ export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")

$ kubectl --namespace default port-forward $POD_NAME 9090
Forwarding from [::1]:9090 -> 9090
Forwarding from 127.0.0.1:9090 -> 9090

$ curl localhost:9090
<a href="/graph">Found</a>

$ curl localhost:9090/metrics

$ curl localhost:9090/graph
