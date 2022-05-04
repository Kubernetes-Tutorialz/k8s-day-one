## Primeiros passos com Kubernetes


1. Iniciando a aula e vendo que nosso cluster esta funcionando legal:

```bash
# kubectl get nodes
NAME                    STATUS   ROLES                  AGE    VERSION
kube-worker01           Ready    <none>                 9h     v1.23.1
kube-worker2            Ready    <none>                 114s   v1.23.1
localhost.localdomain   Ready    control-plane,master   10h    v1.23.1
```

- no Kubernetes temos nodes worker e nodes master
- no master vai ter o APIserver, gerencia do meu cluster, se on nodes, estap saudaveis, conversar com o etcd
- por default ele nao recebe containers, somente nos workers

2. Vamos agora testar o comando `kubectl describe` para ver os detalhes do master:

```bash
# kubectl describe nodes k8smaster
Name:               k8smaster
Roles:              control-plane,master
Labels:             beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=amd64
                    kubernetes.io/hostname=k8smaster
                    kubernetes.io/os=linux
                    node-role.kubernetes.io/control-plane=
                    node-role.kubernetes.io/master=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Sun, 27 Feb 2022 12:32:58 -0300
Taints:             node-role.kubernetes.io/master:NoSchedule
Unschedulable:      false
Lease:
  HolderIdentity:  k8smaster
  AcquireTime:     <unset>
  RenewTime:       Sat, 05 Mar 2022 14:02:00 -0300
Conditions:
  Type                 Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----                 ------  -----------------                 ------------------                ------                       -------
  NetworkUnavailable   False   Wed, 02 Mar 2022 15:19:09 -0300   Wed, 02 Mar 2022 15:19:09 -0300   WeaveIsUp                    Weave pod has set this
  MemoryPressure       False   Sat, 05 Mar 2022 13:57:52 -0300   Sun, 27 Feb 2022 12:32:54 -0300   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure         False   Sat, 05 Mar 2022 13:57:52 -0300   Sun, 27 Feb 2022 12:32:54 -0300   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure          False   Sat, 05 Mar 2022 13:57:52 -0300   Sun, 27 Feb 2022 12:32:54 -0300   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready                True    Sat, 05 Mar 2022 13:57:52 -0300   Sun, 27 Feb 2022 12:40:03 -0300   KubeletReady                 kubelet is posting ready status
Addresses:
```

3. Agora vamos executar um comando para adicionar novos nodes ao cluster:

```bash
# kubeadm token create --print-join-command
kubeadm join 192.168.1.114:6434 --token j7ivmo.up6haifmk55pou7c --discovery-token-ca-cert-hash sha256:3fc69efd6451dedb945ce665bdf436ac3e54e0e55774fb0654b60562677944f7
```

4. Para ativar o auto-complete Red Hat based:

```bash
$ yum install bash-completion -y ; kubectl completion bash > /etc/bash_completion.d/kubectl
```

5. Para ativar o auto-complete execute:

```bash
$ source <(kubectl completion bash)
```

6. Vamos agora descrever um POD:

```bash
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

- eu posso ter mais de 1 container dentro de um mesmo POD.
- esses containers compartilham  o mesmo IP entre eles.

7. Para visualizar todos os namespaces dos meus PODS ativos:

```bash
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

8. Para visualizar todos os namespaces que eu tenho criado no meu control-plane:

```bash
# kubectl get namespaces
NAME              STATUS   AGE
default           Active   44h
kube-node-lease   Active   44h
kube-public       Active   44h
kube-system       Active   44h
```

8.1.  Vamos agora criar um novo namespace, para isso devemos executar o comando abaixo:

```bash
# kubectl create namespace amarops
namespace/amarops created
```

- Agora tenho ele listado:

```bash
# kubectl get namespaces
NAME              STATUS   AGE
amarops           Active   118s
default           Active   44h
kube-node-lease   Active   44h
kube-public       Active   44h
kube-system       Active   44h
```

9. Criando agora um novo POD (quando ele executa o comando run ele cria um POD):

```bash
$ kubectl run nginx --image=nginx
```

9.1 Listando meu POD criado:

```bash
# kubectl get pods
NAME    READY   STATUS    RESTARTS      AGE
nginx   1/1     Running   1 (98m ago)   35h
```

9.2 Vendo mais detalhes desse POD:

```bash
# kubectl describe pods nginx
Name:         nginx
Namespace:    default
Priority:     0
Node:         kube-worker01/192.168.1.210
Start Time:   Sun, 16 Jan 2022 00:48:48 -0300
Labels:       run=nginx
Annotations:  <none>
Status:       Running
IP:           10.44.0.1
IPs:
  IP:  10.44.0.1
Containers:
  nginx:
    Container ID:   docker://223d5b1e749a2065a760dd4cc8e71826504e5832b6632d67753f9e23c3673d52
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:0d17b565c37bcbd895e9d92315a05c1c3c9a29f762b011a10c54a66cd53c9b31
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Mon, 17 Jan 2022 10:53:03 -0300
    Last State:     Terminated
      Reason:       Error
      Exit Code:    255
      Started:      Sun, 16 Jan 2022 00:49:14 -0300
      Finished:     Mon, 17 Jan 2022 10:52:10 -0300
    Ready:          True
    Restart Count:  1
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-bx8dc (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-bx8dc:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

10. Agora quero visualizar mais detalhes do POD do nginx, buscando o manifesto (objeto) no formato `yml`:

```bash
# kubectl get pods nginx -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2022-01-16T03:49:13Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "57326"
  uid: f20a3403-d519-4a7f-8364-d4d996b2dff2
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-bx8dc
      readOnly: true
```

- como ele foi criado para o Kubernetes
- quando eu quiser criar um POD atraves do `yml` preciso fazer algo assim
- muita coisa e lixo eu nao preciso

10.1. Primeiro vamos redirecionar um POD de teste para que eu tenha um exemplo:

```bash
# kubectl get pods nginx -o yaml > meu-primeiro-pod.yml
```

10.2. Nosso `yml` file modificado:

```bash
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
  namespace: amarops
spec:
  containers:
  - image: nginx
    imagePullPolicy: Always
    name: nginx
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

10.3. Agora sim vamos criar nosso primeiro POD e usar ele no meu namesoace `amarops`:

```bash
# kubectl create -f meu-primeiro-pod.yml
pod/nginx created
```

10.4. Se eu listar agora meu namespace eu posso ver meu POD:

```bash
]# kubectl get pods -n amarops
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          2m21s
```

10.5. Veja que eu posso tambem aproveitar um comando que ja me fornece o `yml` exatamente como eu preciso:

- a opcao `dry-run` apenas simula a criacao do POD

```bash
# kubectl run nginx --image=nginx --dry-run=client -o yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

- veja agora:

```bash
# kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          16s
```
