1) Execute the below command to update 
```shell
sudo apt update
```  
2) Install Docker
```shell
sudo apt-get install docker.io -y
```
3) Start Docker
```shell
sudo systemctl start docker
```
4)Enable Docker
```shell
sudo systemctl enable docker
```
5)Check Docker version
```shell
docker --version
```
6)Add Kubernetes package repository key
```shell
sudo apt-get install apt-transport-https curl -y
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```
7)Configure Kubernetes repository
```shell
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt update
```
8)Disable swap temporary
```shell
sudo swapoff -a
```
9)Install Kubeadm package
```shell
sudo apt-get install kubeadm -y
kubeadm version
sudo apt-get install -y kubelet kubectl kubernetes-cni
```
10)Initialize Kubernetes Pod
```shell
sudo kubeadm init --pod-network-cidr=172.168.10.0/24
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
11)check status of node
```shell
kubectl get nodes
```
12)Pod Networking
```shell
sudo sysctl net.bridge.bridge-nf-call-iptables=1
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
13)Check Pod status
```shell
kubectl get pods --all-namespaces
sudo  kubectl get nodes
```
14)Untaint the master node so it can run regular pods
```shell
kubectl taint nodes --all node-role.kubernetes.io/master-
```
