## Trilha Kubernetes (Parte 1): Aprenda os principais componentes do cluster do K8s

Voltando com TUDO pessoal, hoje vamos de Kubernetes, e se tem uma parte que é MUITO importante de se entender são os componentes do forma o cluster do kubernetes e resolvi trazer aqui hoje para vocês o meu entendimento baseado na documentação da ferramenta. A ideia é bem simples, basicamente vou discorrer sobre os principais componentes que fazem parte do cluster do Kubernetes.

Fiquei sem explicar, mas vou aos detalhes do porque eu estou escrevendo esse artigo… Bem, eu tenho adentrado esse mundo do K8s e confesso que estou amando a ferramenta, os comandos, a arquitetura do K8s, como ele se integra com outras ferramentas de DevOps, pipelines e tudo mais. Baseado nisso, resolvi criar uma trilha sobre Kubernetes, ainda não sei ao certo quantos posts isso deve integrar, mas logo logo eu terei uma ideia, o que importa agora é que eu vou levar esse conteúdo até vocês, será TOP, fica ligado e pega seu café! ☕️

## Diagrama do cluster k8s

Sabe-se que para formar um cluster do K8s precisamos de um conjunto de maquinetas, que podemos dividir em dois grandes blocos (control-plane e worker nodes). A ideia é descomplicar os componentes que estão integrados dentro desses dois blocos de maquinetas. Retirei esse diagrama da documentação do k8s para que você possa visualizar em mais detalhes como é desenhada a arquitetura do cluster. Aqui nesse link você vai direto para a doc do Kubernetes para ver mais detalhes de como o cluster está estruturado.

## Componentes do Control Plane

Uma das partes do cluster do Kubernetes é o control-plane, essa maquineta é a responsável por orquestrar o cluster do kubernetes e possui os seguintes componentes:


- Kube-apiserver: é o componente que se comunica com os nós, ele faz essa comunicação de forma segura, funciona como um cérebro mesmo e é o front end do Kubernetes.
- etcd: esse componente funciona como um banco de dados, é o armazenamento baseado em chave-valor do Kubernetes para armazenar todos os dados usados para gerenciar o cluster (deploy, PODs, services). O acesso ao etcd é sempre feito pelo kube-apiserver.
- kube-schedule: esse componente determina em qual nó um POD poderá ser hospedado, ele procura por containers recém criados e atribui à um nó específico. Ele recebe as definições dos containers do Kubernetes, analisa o POD e determina em qual worker node esse POD será executado (comunicação feita pelo kube-apiserver).
- kube-controller-manager: tudo gira em torno de controladores dentro do Kubernetes (node-controller, replicaset, admission-controller), é o kube-controller-manager que gerencia os controllers do cluster do K8s.
- cloud-controller-manager: quando executamos o Kubernetes diretamente de um cloud provider, temos o cloud-controller-manager que faz a comunicação dos serviços na nuvem.

## teste