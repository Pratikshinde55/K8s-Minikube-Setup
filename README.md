
**There are many ways to create K8s cluster:**
1. EKS
2. AKS
3. GKE
4. Kubeadm
5. Minikube

Here I use Minikube for Multi-Node Cluster:
Note: The Cluster is creating is automatic by Minikube we just put our requirement but this is not give fully customize option like Kubeadm.

## Installation of Minikube & Kubectl on Window:
1. Minikube install on window:
    - Search on Browser "kubernetes minikube install" and then Click on ->  'latest release' 
    [Minikube-Download-link](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+downloa)
    ![Download-minikube](https://github.com/user-attachments/assets/676f0852-8c27-4780-aba7-5069338b9c69)
    - After Download Extract exe file then, add **"Path in System Environment variable"**.
    - Note: Install Oracle VirtualBox on Window [download-virtualBox-Link](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html)

2.  Now Install Client side/ User side command that is **"kubectl"** for managing K8s Cluster:
    - Search on Browser:-> "kubectl install" -> then click on "Install and Set Up kubectl on Windows"
    [kubectl-Download-cmd-Link](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-on-windows-via-direct-download-or-curl)
