## Minikube
E um aplicativo usado para teste onde voce pode simular um cluster de Kubernetes. Se voce e uma pessoa desenvolvedor de software ou DevOps Engineer existe essa ferramenta para voce instalar localmente na sua maquineta e comecar a brincar com k8s. Sempre usar Minikube como ambiente de desenvolvimento apenas para testes.

## Install Minikube
Primeiro preciso remover as instalacoes antigas se existir:

```bash
# minikube delete
🔄  Uninstalling Kubernetes v1.22.3 using kubeadm ...
🔥  Deleting "minikube" in none ...
💀  Removed all traces of the "minikube" cluster.
root@inspiron-5566:~# minikube delete
🙄  "minikube" profile does not exist, trying anyways.
💀  Removed all traces of the "minikube" cluster.
```

Agora vamos partir para a instalacao:

```bash
# minikube start
😄  minikube v1.24.0 on Ubuntu 21.10
🎉  minikube 1.25.2 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.25.2
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

✨  Using the virtualbox driver based on user configuration
🛑  The "virtualbox" driver should not be used with root privileges.
💡  If you are running minikube within a VM, consider using --driver=none:
📘    https://minikube.sigs.k8s.io/docs/reference/drivers/none/

❌  Exiting due to DRV_AS_ROOT: The "virtualbox" driver should not be used with root privileges.
```