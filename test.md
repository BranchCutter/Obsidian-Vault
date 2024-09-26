
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

### 2.1.1 Crypto Inspector

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
### 2.1.2 Crypto Observer

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

# 3. Usage

To access the system's dashboard, first identify the access IP and port.

Get Access IP

```bash
$ kubectl get node -o wide
```

![CHECK_IP](./resources/image14.png)

Get Access Port

```bash
$ kubectl get service -n cryptoobserver
```

![CHECK_PORT](./resources/image15.png)

Now, use the obtained IP and port to access the dashboard in a web browser.

## 3.1 Topology

The Topology page provides both graphical and tabular representations of all encryption algorithms used in service communication.

### 3.1.1 Screen Layout

The Topology page displays the following information:

1. **Navigation Bar**: Allows switching between features like Topology, TLS Session, Key Management, and TLS Verification.
2. **Topology Graph**: Shows the currently active session or the most recently connected session in a graph.
3. **Dashboard Table**: Shows detailed information about the active or most recent session.

![TOPOLOGY_VIEW_LAYOUT](./resources/image16.png)
### Dashboard Table Detailed Information

| Source Namespace | Source Name | Source IP | Source Port | Destination Namespace | Destination Name | Destination IP | Destination Port | TLS Version | Cipher Suite | Certificate Signature |

By selecting an element from the topology graph or the dashboard table, additional information about the connection is displayed:
![SEARCH_RESULT_DETAIL](./resources/image17.png)

| Service Metadata | Service Resource Type |

### 3.1.2 Search

If you need to search for specific session information, you can use the search function. After searching, the topology graph and dashboard table will update with the relevant results.

![SEARCH_FUNCTION](./resources/image18.png)

### Example of Search Criteria

For instance, you could search by source type, TLS version, or other key parameters. The results will filter sessions based on the criteria.

![SEARCH_APPLIED](./resources/image19.png)

### 3.1.3 Vulnerable Encryption Detection

The Topology page provides a color-coded display to indicate encryption security:

- **Green**: Secure encryption is applied.
- **Yellow**: Vulnerable encryption is applied, but encryption is still present.
- **Red**: No encryption is applied.

When viewing the detailed connection information page, you will also see which specific encryption elements are marked as vulnerable or non-vulnerable. Vulnerability information is available for every encryption session in the system.

![DETAIL_PAGE_SHOW_WEAKNESS](./resources/image20.png)

This feature allows you to immediately identify weak encryption algorithms and take corrective actions where necessary.
 
## 3.2 TLS Sessions

The TLS Sessions page provides detailed information about all encryption algorithms used during service communication.

### 3.2.1 Screen Layout

The TLS Sessions page displays the following information:

- Dashboard Table: Detailed information of active or recently connected sessions.

![TLS_SESSION_EXAMPLE](./resources/image21.png)

### 3.2.2 Searching

If you need to search for specific session information, use the search function in the top left corner.

![TLS_SESSION_SEARCH_FUNCTION](./resources/image22.png)

### 3.2.3 Reset

If the database becomes overloaded with excessive information, use the reset button to clear the output.

![TLS_SESSION_RESET](./resources/image23.png)

## 3.3 Key Management

The Key Management page provides a lifecycle management view of certificates and keys in the cloud service mesh.

### 3.3.1 Screen Layout

1. Dashboard Table : Show certificate and key details table being managed by Istio

![TLS_SESSION_RESET](./resources/image24.png)

The Key Management page shows the following information in a dashboard table:

| Timestamp | Namespace | Name | Spiffe ID | TTL | Time Left | Status |
|-----------|------------|------|-----------|-----|-----------|--------|

You can monitor certificate and key management events in real-time.

## 3.4 TLS Verification

The TLS Verification page attempts a TLS handshake with a specified target, providing encryption algorithm and domain information.

### 3.4.1 Screen Layout

1. Dashboard Table : Show handshake information table held in TLS Verification page

![TLS_VERIFICATION_PAGE](./resources/image25.png)

The following information is displayed after performing a TLS handshake:

- IP/Port Information
- Domain Name (if available)
- TLS Version
- Cipher Suite
- Signature Algorithm
- Public Key Algorithm

### 3.4.2 TLS Handshake

The TLS handshake function may be executed through the green magnifier button at the top left as shown in screenshot below. In this case, the handshake target IP may be executed by entering the port number on the left and the port number on the right.

![TLS_HANDSHAKE](./resources/image26.png)
# 4. Example Usage

For testing, we will generate an example service and perform an external TLS handshake with a weak encryption algorithm to verify proper system functionality.

## 4.1 Topology

- Run a Google MSA demo and Ubuntu deployment.
- Perform an external OpenSSL test from outside to the Ubuntu deployment.
- Perform an internal OpenSSL test from the Ubuntu deployment to the external service.

Update the README accordingly.


# 8. Final Notes

This document outlines the deployment and management procedures for the CryptoObserver system. Make sure to follow the steps carefully to ensure proper functionality and integration with your cloud environment. For further customization or additional features, refer to the official documentation of the tools and frameworks used, such as Kubernetes, Istio, and OpenSSL.


