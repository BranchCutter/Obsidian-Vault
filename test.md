
# 1. Prerequisites

## 1.1 Create Working Directory and Extract Files

To ensure smooth operation of the system, it is recommended to use a machine with at least 2 CPU cores and 4GB of memory.

1. Create a working directory and extract the necessary files.

```bash
$ mkdir ~/files
$ cd ~/files
$ tar -zxvf CryptoObserver.tar.gz -C ~/files/
```

2. Docker Installation (Optional)

   Docker is a tool used for building containers. If you're not modifying the code (i.e., using prebuilt images), you don't need to install Docker.

   To install Docker, run the following script:

```bash
$ cd ~/files/CryptoObserver/prerequisites/docker
$ ./install-docker.sh
```

Verify Docker installation:

```bash
$ docker ps
```

## 1.2 Install Kubernetes and Dependencies

For this example, we will use the lightweight version of Kubernetes, called **MicroK8s**.

```bash
$ cd ~/files/CryptoObserver/prerequisites/microk8s
$ ./01_install-microk8s.sh
$ ./02_alias.sh
$ ./03_install-istio.sh
```

To install MicroK8s manually:

```bash
$ sudo snap install microk8s --classic
$ sudo usermod -a -G microk8s $USER
$ newgrp microk8s
```

### Set up Aliases for `kubectl`

```bash
$ echo -e "alias kubectl="microk8s.kubectl"" >> ~/.bashrc
$ source ~/.bashrc
```

### Install Istio

```bash
$ sudo microk8s enable community
$ sudo microk8s.enable istio
```

To check Istio installation:

```bash
$ kubectl get pod -A
```
