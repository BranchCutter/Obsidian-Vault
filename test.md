
# 1. Prerequisites

## 1.1 Create Working Directory and Extract Files

To ensure smooth operation of the system, it is recommended to use a machine with at least 2 CPU cores and 4GB of memory.

1. Create a working directory and extract the necessary files.

```bash
$ mkdir ~/files
$ cd ~/files
$ tar -zxvf CryptoObserver.tar.gz -C ~/files/
```

![CREATE_DIRECTORY](./resources/image01.png)


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

![DOCKER_PS](./resources/image02.png)


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

![ISNTALL_MICROK8S](./resources/image03.png)


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

![INSTALL_ISTIO](./resources/image04.png)

To check Istio installation:

```bash
$ kubectl get pod -A
```

![CHECK_ISTIO](./resources/image05.png)

# 2. Key Management and Crypto Algorithms Visualization Deployment

## 2.1 Image Build (Optional)

Before building container images, Docker must be installed.

### a. Crypto Inspector

Navigate to the Crypto Inspector folder:

```bash
$ cd ~/files/CryptoObserver/CryptoInspector
```

Build the Crypto Inspector image:

```bash
$ docker build -t boanlab/crypto_inspector:latest .
$ docker save boanlab/crypto_inspector:latest > crypto_inspector.tar
$ sudo ctr images import crypto_inspector.tar
```

![INSTALL_ISTIO](./resources/image06.png)

![UPLOAD_INSPECTOR](./resources/image07.png)

Check image is uploaded
```
$ sudo ctr image ls
```

![CHECK_IMAGE](./resources/image08.png)
### b. Crypto Observer

Navigate to the Crypto Observer folder:

```bash
$ cd ~/files/CryptoObserver/CryptoObserver
```

Build the Crypto Observer image:

```bash
$ docker build -t boanlab/crypto_observer:latest .
$ docker save boanlab/crypto_observer:latest > crypto_observer.tar
$ sudo ctr images import crypto_observer.tar
```

![BUILD_CRYPTO_OBSERVER](./resources/image09.png)

![UPLOAD_CRYPTO_OBSERVER](./resources/image10.png)

```
$ sudo ctr image ls
```

![CHECK_IMAGE_UPLOAD](./resources/image11.png)

## 2.2 Deployment

Navigate to the folder containing the YAML files for deployment:

```bash
$ cd ~/files/CryptoObserver/deployments
```

Deploy using Kubernetes:

```bash
$ kubectl apply -f install.yaml
```

![K8S_DEPLOYMENT_PROCESS](./resources/image12.png)

Verify deployment:

```bash
$ kubectl get pod -n cryptoobserver
```

![CHECK_DEPLOYMENT](./resources/image13.png)

## 3. Usage

To access the system's dashboard, first identify the access IP and port.

### a. Get Access IP

```bash
$ kubectl get node -o wide
```

![CHECK_IP](./resources/image14.png)

### b. Get Access Port

```bash
$ kubectl get service -n cryptoobserver
```

![CHECK_PORT](./resources/image15.png)

Now, use the obtained IP and port to access the dashboard in a web browser.
# 4. TLS Sessions

The TLS Sessions page provides detailed information about all encryption algorithms used during service communication.

## 4.1 Screen Layout

The TLS Sessions page displays the following information:

- Dashboard Table: Detailed information of active or recently connected sessions.

```bash
# Example command to view sessions
$ kubectl get pod -n cryptoobserver
```

## 4.2 Searching

If you need to search for specific session information, use the search function in the top left corner.

```bash
# Example search command
$ kubectl describe pod <pod-name>
```

## 4.3 Reset

If the database becomes overloaded with excessive information, use the reset button to clear the output.

```bash
# Example reset command
$ kubectl delete pod <pod-name> -n cryptoobserver
```

# 5. Key Management

The Key Management page provides a lifecycle management view of certificates and keys in the cloud service mesh.

## 5.1 Screen Layout

The Key Management page shows the following information in a dashboard table:

| Timestamp | Namespace | Name | Spiffe ID | TTL | Time Left | Status |
|-----------|------------|------|-----------|-----|-----------|--------|

You can monitor certificate and key management events in real-time.

# 6. TLS Verification

The TLS Verification page attempts a TLS handshake with a specified target, providing encryption algorithm and domain information.

## 6.1 Screen Layout

The following information is displayed after performing a TLS handshake:

- IP/Port Information
- Domain Name (if available)
- TLS Version
- Cipher Suite
- Signature Algorithm
- Public Key Algorithm

## 6.2 TLS Handshake

To execute a TLS handshake, use the search icon and input the IP and Port to attempt the handshake.

```bash
# Example TLS handshake command
$ openssl s_client -connect <ip>:<port>
```

# 7. Example Usage

For testing, we will generate an example service and perform an external TLS handshake with a weak encryption algorithm to verify proper system functionality.

- Run a Google MSA demo and Ubuntu deployment.
- Perform an external OpenSSL test from outside to the Ubuntu deployment.
- Perform an internal OpenSSL test from the Ubuntu deployment to the external service.

Update the README accordingly.


# 8. Final Notes

This document outlines the deployment and management procedures for the CryptoObserver system. Make sure to follow the steps carefully to ensure proper functionality and integration with your cloud environment. For further customization or additional features, refer to the official documentation of the tools and frameworks used, such as Kubernetes, Istio, and OpenSSL.

### Summary of Key Steps:

1. Set up Docker and Kubernetes (MicroK8s) in your environment.
2. Build and deploy the CryptoObserver and CryptoInspector images.
3. Use Kubernetes to monitor and manage the pods, deployments, and services.
4. Utilize the TLS Sessions, Key Management, and TLS Verification pages for real-time insights into encryption algorithms and security postures.
5. Perform hands-on testing with the provided example usage.

For any issues or troubleshooting, consider using Kubernetes logs, Docker image checks, and OpenSSL tests to diagnose and resolve problems efficiently.
