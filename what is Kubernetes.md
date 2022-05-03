## Table of Contents
- [Table of Contents](#table-of-contents)
- [Kubernetes](#kubernetes)
- [Componentes Kubernetes](#componentes-kubernetes)
  - [POD](#pod)
  - [Replicaset](#replicaset)
  - [Deployment](#deployment)
  - [Services](#services)
## Kubernetes
O *Kubernetes* ou *k8s* e um orquestrador de containers baseado no *Borg* usado anteriormente pelo *Google*. Usado para implantacao de aplicacoes conteinerizadas. Hoje e um dos maiores projetos de codigo aberto do mundo, tornou-se a *API* padrao para construcao de aplicacoes nativas em nuvem e esta presente em quase todos os provedores de nuvem publica.

- escrito em Go
- orquestra os containers
- beseado no *Borg* do *Google*
- Infraestrutura moderna

## Componentes Kubernetes
Temos alguns papeis que sao importantes dentro de um cluster de *Kubernetes*.

### POD
POD no contexto do Kubernetes se refere a menor unidade do *k8s*, e dentro dos *POD's* que se abriga os containers, podendo ter mais de um container por *POD*, a boa pratica e sempre manter um container por *POD*.

### Replicaset
Faz o gerenciamento dos *POD's* no *k8s*. Guarda a versao da imagem do container sempre cuidando das replicas dos POD's.

### Deployment
Faz o gerenciamento do *replicaset* e ajuda na parte de atualizacao das novas versoes das imagens dos containers, e gera um novo *replicaset* baseado nas configuracoes que fazemos no *deployment*.

### Services
Ajuda na parte de acessos dos servicos dentro do container, para se ter acessos atraves de pessoas, ferramentas, precisamos ter um *service* configurado. O *service* gera a possibilidade de ter acesso aos nossos *POD's*.

- [ ] *selector*: usado para identificar a label com o container (app: front)
- [ ] *Cluster IP*: funciona como se fosse um IP interno para se comunicar com o container.
- [ ] *NodePort*:  


