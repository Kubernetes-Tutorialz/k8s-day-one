# day-one
A basic introduction about Kubernetes following the Kubernetes documentation https://kubernetes.io/pt-br/


## Install Minikube n Ubuntu

```
sudo -E minikube start --driver=none
😄  minikube v1.24.0 on Ubuntu 21.04
✨  Using the none driver based on user configuration
👍  Starting control plane node minikube in cluster minikube
🤹  Running on localhost (CPUs=4, Memory=11781MB, Disk=222802MB) ...
ℹ️  OS release is Ubuntu 21.04
🐳  Preparing Kubernetes v1.22.3 on Docker 20.10.12 ...
    ▪ kubelet.resolv-conf=/run/systemd/resolve/resolv.conf
    > kubectl.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubeadm.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubelet.sha256: 64 B / 64 B [--------------------------] 100.00% ? p/s 0s
    > kubectl: 44.73 MiB / 44.73 MiB [---------------] 100.00% 2.43 MiB p/s 19s
    > kubeadm: 43.71 MiB / 43.71 MiB [---------------] 100.00% 1.65 MiB p/s 27s
    > kubelet: 115.57 MiB / 115.57 MiB [-------------] 100.00% 3.19 MiB p/s 36s
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🤹  Configuring local host environment ...

❗  The 'none' driver is designed for experts who need to integrate with an existing VM
💡  Most users should use the newer 'docker' driver instead, which does not require root!
📘  For more information, see: https://minikube.sigs.k8s.io/docs/reference/drivers/none/

❗  kubectl and minikube configuration will be stored in /root
❗  To use kubectl or minikube commands as your own user, you may need to relocate them. For example, to overwrite your own settings, run:

    ▪ sudo mv /root/.kube /root/.minikube $HOME
    ▪ sudo chown -R $USER $HOME/.kube $HOME/.minikube

💡  This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

---

```
 1  yum intall vim git -y
    2  yum install vim git -y
    3  yum update -y
    4  pwd
    5  vim /etc/modules-load.d/k8s.conf
    6  curl -fsSL https://get.docker.com | bash
    7  systemctl status docker
    8  systemctl start docker
    9  systemctl status docker
   10  systemctl enable docker
   11  yum install bash-completion -y
   12  cat > /etc/docker/daemon.json <<EOF
   13  {
   14    "exec-opts": ["native.cgroupdriver=systemd"],
   15    "log-driver": "json-file",
   16    "log-opts": {
   17      "max-size": "100m"
   18    },
   19    "storage-driver": "overlay2",
   20    "storage-opts": [
   21      "overlay2.override_kernel_check=true"
   22    ]
   23  }
   24  EOF
   25  sudo mkdir -p /etc/systemd/system/docker.service.d
   26  sudo systemctl daemon-reload
   27  sudo systemctl restart docker
   28  docker info | grep -i cgroup
   29  vim /etc/docker/daemon.json
   30  sudo systemctl daemon-reload
   31  sudo systemctl restart docker
   32  systemctl status docker
   33  docker info | grep -i cgroup
   34  vim /etc/yum.repos.d/kubernetes.repo
   35  sudo setenforce 0
   36  sudo systemctl stop firewalld
   37  sudo systemctl disable firewalld
   38  sudo yum install -y kubelet kubeadm kubectl
   39  sudo systemctl enable docker && sudo systemctl start docker
   40  sudo systemctl enable kubelet && sudo systemctl start kubelet
   41  vim /etc/sysctl.d/k8s.conf
   42  sudo swapoff -a
   43  vim /etc/fstab
   44  reboot
   45  ping 8.8.8.8
   46  yum install net-tools -y
   47  ifconfig
   48  sudo kubeadm config images pull
   49  sudo kubeadm init
   50  poweroff
   51  sudo kubeadm init
   52  kubectl get namespaces
   53  kubectl get nodes
   54  mkdir -p $HOME/.kube
   55  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   56  sudo chown $(id -u):$(id -g) $HOME/.kube/config
   57  sudo modprobe br_netfilter ip_vs_rr ip_vs_wrr ip_vs_sh nf_conntrack_ipv4 ip_vs
   58  kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
   59  kubectl get nodes
   60  kubectl get pods -n kube-system
   61  date
   62  poweroff
   63  kubectl get nodes
   64  kubectl get pods -n kube-system
   65  kubeadm token create --print-join-command
   66  history
```
