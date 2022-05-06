## Trilha Kubernetes (Parte 1): Aprenda os principais componentes do cluster do K8s

Voltando com TUDO pessoal, hoje vamos de Kubernetes, e se tem uma parte que é MUITO importante de se entender são os componentes do forma o cluster do kubernetes e resolvi trazer aqui hoje para vocês o meu entendimento baseado na documentação da ferramenta. A ideia é bem simples, basicamente vou discorrer sobre os principais componentes que fazem parte do cluster do Kubernetes.

Fiquei sem explicar, mas vou aos detalhes do porque eu estou escrevendo esse artigo… Bem, eu tenho adentrado esse mundo do K8s e confesso que estou amando a ferramenta, os comandos, a arquitetura do K8s, como ele se integra com outras ferramentas de DevOps, pipelines e tudo mais. Baseado nisso, resolvi criar uma trilha sobre Kubernetes, ainda não sei ao certo quantos posts isso deve integrar, mas logo logo eu terei uma ideia, o que importa agora é que eu vou levar esse conteúdo até vocês, será TOP, fica ligado e pega seu café! ☕️

## Diagrama do cluster k8s

Sabe-se que para formar um cluster do K8s precisamos de um conjunto de maquinetas, que podemos dividir em dois grandes blocos (control-plane e worker nodes). A ideia é descomplicar os componentes que estão integrados dentro desses dois blocos de maquinetas. Retirei esse diagrama da documentação do k8s para que você possa visualizar em mais detalhes como é desenhada a arquitetura do cluster. Aqui nesse link você vai direto para a doc do Kubernetes para ver mais detalhes de como o cluster está estruturado.