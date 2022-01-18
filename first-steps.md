## `Primeiros passos com Kubernetes`


1. Iniciando a aula e vendo que nosso cluster esta funcionando legal

```
]# kubectl get nodes
NAME                    STATUS   ROLES                  AGE    VERSION
kube-worker01           Ready    <none>                 9h     v1.23.1
kube-worker2            Ready    <none>                 114s   v1.23.1
localhost.localdomain   Ready    control-plane,master   10h    v1.23.1
```

- no Kubernetes temos nodes **worker** e nodes **master**.
- no master vai ter o APIserver, gerencia do meu cluster, se on nodes, estap saudaveis, conversar com o etcd.
- por default ele nao recebe containers, somente nos workers.

2. Vamos agora testar o comando `kubectl describe` para ver os detalhes do master:

```
$ kubectl describe nodes localhost.localdomain
Name:               localhost.localdomain
Roles:              control-plane,master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=localhost.localdomain
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node-role.kubernetes.io/master=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sat, 15 Jan 2022 16:15:18 -0300
Taints:             node-role.kubernetes.io/master:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  localhost.localdomain
  AcquireTime:     <unset>
  RenewTime:       Sun, 16 Jan 2022 02:50:09 -0300
```

3. Agora vamos executar um comando para adicionar novos nodes ao cluster:

```
# kubeadm token create --print-join-command
```

4. Para ativar o auto-complete em Red Hat based:

```
$ yum install bash-completion -y ; kubectl completion bash > /etc/bash_completion.d/kubectl
```

5. Para ativar o auto-complete execute:

```
$ source <(kubectl completion bash)
```

6. Vamos agora descrever um POD:

```
# kubectl describe pods -n kube-system
Name:                 coredns-64897985d-7wkj2
Namespace:            kube-system
Priority:             2000000000
Priority Class Name:  system-cluster-critical
Node:                 localhost.localdomain/192.168.0.155
Start Time:           Sat, 15 Jan 2022 16:21:31 -0300
Labels:               k8s-app=kube-dns
                      pod-template-hash=64897985d
Annotations:          <none>
Status:               Running
IP:                   10.32.0.2
IPs:
  IP:           10.32.0.2
Controlled By:  ReplicaSet/coredns-64897985d
Containers:
  coredns:
    Container ID:  docker://921353442b349cc1e77c7cc150701486b9782c6682324aae1cea7b1100062544
    Image:         k8s.gcr.io/coredns/coredns:v1.8.6
    Image ID:      docker-pullable://k8s.gcr.io/coredns/coredns@sha256:5b6ec0d6de9baaf3e92d0f66cd96a25b9edbce8716f5f15dcd1a616b3abd590e
    Ports:         53/UDP, 53/TCP, 9153/TCP
    Host Ports:    0/UDP, 0/TCP, 0/TCP
    Args:
      -conf
      /etc/coredns/Corefile
    State:          Running
      Started:      Mon, 17 Jan 2022 10:53:19 -0300
    Last State:     Terminated
      Reason:       Error
      Exit Code:    255
      Started:      Sat, 15 Jan 2022 16:49:02 -0300
      Finished:     Mon, 17 Jan 2022 10:52:03 -0300
    Ready:          True
    Restart Count:  1
```

- eu posso ter mais de 1 container dentro de um mesmo POD
- esses containers compartilham  o mesmo IP entre eles

7. Para visualizar todos os namespace ativos:

```
# kubectl get pods --all-namespaces -o wide
NAMESPACE     NAME                                            READY   STATUS    RESTARTS      AGE   IP              NODE                    NOMINATED NODE   READINESS GATES
default       nginx                                           1/1     Running   1 (90m ago)   35h   10.44.0.1       kube-worker01           <none>           <none>
kube-system   coredns-64897985d-7wkj2                         1/1     Running   1 (90m ago)   44h   10.32.0.2       localhost.localdomain   <none>           <none>
kube-system   coredns-64897985d-p2z9f                         1/1     Running   1 (90m ago)   44h   10.32.0.3       localhost.localdomain   <none>           <none>
kube-system   etcd-localhost.localdomain                      1/1     Running   1 (90m ago)   44h   192.168.0.120   localhost.localdomain   <none>           <none>
kube-system   kube-apiserver-localhost.localdomain            1/1     Running   1 (90m ago)   44h   192.168.1.120   localhost.localdomain   <none>           <none>
kube-system   kube-controller-manager-localhost.localdomain   1/1     Running   1 (90m ago)   44h   192.168.1.120   localhost.localdomain   <none>           <none>
kube-system   kube-proxy-69h5f                                1/1     Running   1 (90m ago)   42h   192.168.1.210   kube-worker01           <none>           <none>
kube-system   kube-proxy-6p9vx                                1/1     Running   1 (89m ago)   33h   192.168.1.210   kube-worker2            <none>           <none>
kube-system   kube-proxy-dcxhd                                1/1     Running   1 (90m ago)   44h   192.168.1.120   localhost.localdomain   <none>           <none>
kube-system   kube-scheduler-localhost.localdomain            1/1     Running   1 (90m ago)   44h   192.168.1.120   localhost.localdomain   <none>           <none>
kube-system   weave-net-dbnw7                                 2/2     Running   2 (90m ago)   42h   192.168.1.210   kube-worker01           <none>           <none>
kube-system   weave-net-pdq4q                                 2/2     Running   2 (89m ago)   33h   192.168.1.210   kube-worker2            <none>           <none>
kube-system   weave-net-pkxh8                                 2/2     Running   3 (89m ago)   44h   192.168.1.120   localhost.localdomain   <none>           <none>
```


















