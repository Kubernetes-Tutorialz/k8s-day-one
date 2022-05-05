## Primeiros passos com Kubernetes - Parte 2

1. Primeiramente vamos comecar analisando nosso *POD*:

```bash
# kubectl get pods
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          4h45m
```

2.  Agora vamos usar um outro comando para criar nosso *service*:

```bash
# kubectl expose pod nginx
error: couldn't find port via --port flag or introspection
See 'kubectl expose -h' for help and examples
```
#### Concepts
- veja que ele retornou um erro pedindo para setar a porta.
- vamos usar o `YML` para subir com a porta.

3.  Agora que editei a porta no `YML` file vamos executar de novo o comando `expose`:

```yml
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
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

4.  Veja que agora podemos expor o *service*:

```bash
# kubectl expose pod nginx
service/nginx exposed
```

5.  Listando:

```bash
# kubectl describe pods nginx | grep -i port
    Port:           80/TCP
    Host Port:      0/TCP
```

6.  Veja que ele agora possui um *service* criado:

```bash
# kubectl get service
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP   6d10h
nginx        ClusterIP   10.106.174.205   <none>        80/TCP    14s
```

7.  Testando  usando o comando `curl`:

```html
# curl 10.106.174.205
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

8.  Veja agora mais detalhes do *service*:

```bash
# kubectl describe service nginx
Name:              nginx
Namespace:         default
Labels:            run=nginx
Annotations:       <none>
Selector:          run=nginx
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.106.174.205
IPs:               10.106.174.205
Port:              <unset>  80/TCP
TargetPort:        80/TCP
Endpoints:         10.44.0.1:80
Session Affinity:  None
Events:            <none>
```

9.  Vamos editar nosso *service* do *NGINX*:

```bash
# kubectl edit service nginx
service/nginx edited
```

- mudei de *ClusterIP* -> *NodePort*
- veja que agora ele aparece com a porta

```bash
# kubectl get service
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP        6d10h
nginx        NodePort    10.106.174.205   <none>        80:30654/TCP   11m
```

10. Vou acessar no browser o IP da minha instancia com essa porta:

`http://192.168.0.222:30654/`

```java
Welcome to nginx!

If you see this page, the nginx web server is successfully installed and working. Further configuration is required.

For online documentation and support please refer to nginx.org.
Commercial support is available at nginx.com.

Thank you for using nginx.
```

11. Pegando o `YML` do meu *service*:

`# kubectl get service nginx -o yaml`

```yml
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2022-03-06T01:49:05Z"
  labels:
    run: nginx
  name: nginx
  namespace: default
  resourceVersion: "400096"
  uid: 040663fa-43be-4335-8517-95f70e9459e0
spec:
  clusterIP: 10.106.174.205
  clusterIPs:
  - 10.106.174.205
  externalTrafficPolicy: Cluster
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - nodePort: 30654
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx
  sessionAffinity: None
  type: NodePort
status:
  loadBalancer: {}  
```



