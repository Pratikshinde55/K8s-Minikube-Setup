
**There are many ways to create K8s cluster:**
1. EKS
2. AKS
3. GKE
4. Kubeadm
5. Minikube

Here I use Minikube for Multi-Node Cluster:
Note: The Cluster is creating is automatic by Minikube we just put our requirement but this is not give fully customize option like Kubeadm.

## Installation of Minikube & Kubectl on Window:
1. *Minikube install on window:*
    - Search on Browser "kubernetes minikube install" and then Click on ->  'latest release' 
    [Minikube-Download-link](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+downloa)
    ![Download-minikube](https://github.com/user-attachments/assets/676f0852-8c27-4780-aba7-5069338b9c69)
    - After Download Extract exe file then, add **"Path in System Environment variable"**.
    - Note: Install Oracle VirtualBox on Window [download-virtualBox-Link](https://www.oracle.com/virtualization/technologies/vm/downloads/virtualbox-downloads.html)

2.  *Now Install Client side/ User side command that is **"kubectl"** for managing K8s Cluster:*
    - Search on Browser:-> "kubectl install" -> then click on "Install and Set Up kubectl on Windows"
    [kubectl-Download-cmd-Link](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/#install-kubectl-binary-on-windows-via-direct-download-or-curl)

- Note: If CLI show error then put both minikube & kubectl file in same folder of window. 

# Single-Node Cluster:
Here i create Single-node cluster that is means on single node Master & Worker Node work done.

To Create Single-Node Culster using minikube command is:

    minikube start

## Deployment:
- Now create deployment using image:

      kubectl create deployment myweb --image=pratikshinde55/apache-webserver:v1

  ![Deployment](https://github.com/user-attachments/assets/7ed66fae-9733-4ef7-abe2-c80e0879ddaa)

- Use describe:

      kubectl describe deployment myweb

- Print list of Deployment & Pod:

      kubectl get pods
      kubectl get deployment

   ![get-cmd](https://github.com/user-attachments/assets/88dc8c0c-917d-4c97-8126-d43c31459b29)

- Get Full lenght information:

      kubectl get pods myweb-b77b85fb9-bghs9  -o wide
      kubectl get deployment myweb -o wide

## Load Balancer: [expose]
- Create service or expose our deployment app to outside world:

      kubectl expose deployment myweb --type=NodePort --port=80

- Print list of LB:

      kubectl get svc 
      kubectl get service

- **Note:** `--type=NodePort` is define give Public_IP & `--port=80` => This is port number of Container or If any app running inside pod/Container then give that port no for example Python-flask app port 5000.
      
      kubectl describe svc myweb

- Here, We see all three pods are attached to the Load Balancer, If we Scale-out or Scale-in that will automatic upadte to Load Balancer Service
  ![See all details](https://github.com/user-attachments/assets/59709750-cdd0-4f5d-990e-3b8d615ba2cb)

## Manual Scaling: [scale]
- Command for manual scale:

    kubectl scale deployment myweb --replicas=3   
    
  ![scale-cmd](https://github.com/user-attachments/assets/3ecc1a0f-c6e5-41db-89f6-d8d4491bec91)

# Multi-Node-Cluster:
Now here create multi-node cluster using minikube.


