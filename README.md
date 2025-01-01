# Kubernates Installation in Ubuntu on AWS Cloud

## Steps to install docker, minikube, microk8s:

Requirement:
1. Instance type: t2.medium (AWS)
2. Ubuntu 22.04 system
3. 25 GiB free disk

### Docker installation
(create a file.sh enter below code there and install the docker on Ubuntu)

```
#!/bin/bash 

# Update the server and add the Docker official gpg keys:

sudo apt-get update
sudo apt install ca-certificates curl gnupg wget apt-transport-https -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Latest docker and docker packages

$ sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```

### Ensure that curl is also installed:
```
sudo apt-get update && sudo apt-get install curl -y
```

### Install VirtualBox (if not already installed)
```
sudo apt-get update
sudo apt-get install conntrack -y
sudo apt-get install curl wget apt-transport-https -y
sudo apt-get install virtualbox virtualbox-ext-pack -y
```

### Install kubectl
(create a file kube.sh and then enter below code and install the kubectl on ubuntu)
```
#!/bin/bash 
sudo apt-get update

# apt-transport-https may be a dummy package; if so, you can skip that package

sudo apt-get install -y apt-transport-https ca-certificates curl gnupg

# If the folder `/etc/apt/keyrings` does not exist, it should be created before the curl command, read the note below.

sudo mkdir -p -m 755 /etc/apt/keyrings
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg # allow unprivileged APT programs to read this keyring

# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   # helps tools such as command-not-found to work correctly

sudo apt-get update
sudo apt-get install -y kubectl
```


### Install minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

### Once all dependencies are installed, you can start Minikube. Ensure Docker is running, and then start Minikube:
```
minikube start --driver=docker
```
