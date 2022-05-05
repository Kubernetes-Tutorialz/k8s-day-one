## Primeiros passos com Kubernetes - Parte 3

1.  Podemos tambem usar um comando que mostra detalhes de cada componente do k8s:

```bash
# kubectl explain pods
KIND:     Pod
VERSION:  v1

DESCRIPTION:
     Pod is a collection of containers that can run on a host. This resource is
     created by clients and scheduled onto hosts.

FIELDS:
   apiVersion   <string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind <string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata     <Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec <Object>
     Specification of the desired behavior of the pod. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status

   status       <Object>
     Most recently observed status of the pod. This data may not be up to date.
     Populated by the system. Read-only. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status
```

2.  Tambem podemos executar muitos comandos ao mesmo tempo:

```bash
# kubectl get pods,services,endpoints
NAME        READY   STATUS    RESTARTS   AGE
pod/nginx   1/1     Running   0          113m

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP        6d12h
service/nginx        NodePort    10.106.174.205   <none>        80:30654/TCP   112m

NAME                   ENDPOINTS            AGE
endpoints/kubernetes   192.168.0.234:6443   6d12h
endpoints/nginx        10.44.0.1:80         112m
```

3.  Podemos usar abreviacoes de comandos:

```bash
# kubectl get po
No resources found in default namespace.
```

tambem:

```bash
# kubectl get ns
NAME              STATUS   AGE
default           Active   6d12h
devops            Active   7h23m
kube-node-lease   Active   6d12h
kube-public       Active   6d12h
kube-system       Active   6d12h
```

tambem:

```bash
# kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d12h
```