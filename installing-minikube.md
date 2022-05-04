# Minikube
E um aplicativo usado para teste onde voce pode simular um cluster de Kubernetes. Se voce e uma pessoa desenvolvedor de software ou DevOps Engineer existe essa ferramenta para voce instalar localmente na sua maquineta e comecar a brincar com k8s. Sempre usar Minikube como ambiente de desenvolvimento apenas para testes.

## Requeriments
- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container or virtual machine manager

## Install Minikube
1-  Primeiro preciso remover as instalacoes antigas se existir:

```bash
# minikube delete
🔄  Uninstalling Kubernetes v1.22.3 using kubeadm ...
🔥  Deleting "minikube" in none ...
💀  Removed all traces of the "minikube" cluster.
root@inspiron-5566:~# minikube delete
🙄  "minikube" profile does not exist, trying anyways.
💀  Removed all traces of the "minikube" cluster.
```

2-  Agora vamos partir para a instalacao do [Minikube](https://minikube.sigs.k8s.io/docs/start/)

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

3-  Veja que ele deu erro na instalacao por privilegios de administrador.

```bash
❌  Exiting due to DRV_AS_ROOT: The "virtualbox" driver should not be used with root privileges.
```

4-  Vou prosseguir agora sem o usuario *root*:

```bash
$ minikube start
😄  minikube v1.24.0 on Ubuntu 21.10
🎉  minikube 1.25.2 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.25.2
💡  To disable this notice, run: 'minikube config set WantUpdateNotification false'

✨  Automatically selected the virtualbox driver. Other choices: none, ssh
💿  Downloading VM boot image ...
    > minikube-v1.24.0.iso.sha256: 65 B / 65 B [-------------] 100.00% ? p/s 0s
    > minikube-v1.24.0.iso: 225.58 MiB / 225.58 MiB [] 100.00% 4.70 MiB p/s 48s
👍  Starting control plane node minikube in cluster minikube
💾  Downloading Kubernetes v1.22.3 preload ...
    > preloaded-images-k8s-v13-v1...: 501.73 MiB / 501.73 MiB  100.00% 4.68 MiB
🔥  Creating virtualbox VM (CPUs=2, Memory=2900MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.22.3 on Docker 20.10.8 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

## Minikube Commands
Principais comandos do Minikube para que voce possa comecar do seu lado:

```bash
# minikube start
# kubectl get nodes
# minikube ip
# minikube ssh 
# minikube start
# minikube stop
# minikube dashboard
# minikube logs
```