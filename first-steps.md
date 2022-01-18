## `Primeiros Passos com Kubernetes`


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

















