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

## Manual Scaling- service: [scale]
- Command for manual scale:

      kubectl scale deployment myweb --replicas=3   
    
  ![scale-cmd](https://github.com/user-attachments/assets/3ecc1a0f-c6e5-41db-89f6-d8d4491bec91)

## delete all:
- delete command:

      kubectl delete all -all

## Delete minikube single-node cluster:

     minikube delete
- **Note:** After deleted cluster then Go to windows file manager then go to C:\ then -> Users -> ownuser -> `.minikube` then delete this minikube file
  
# Multi-Node-Cluster:
Now here create multi-node cluster using minikube.

**Interact with Kubernetes:**
1. CLI (Adhoc commands)
2. Code (YAML - Yet Another Markup Language , Declarative Language)
3. API

**Start Minikube Multi-node Cluster Command:**

     minikube start -n 2 -p pscluster2

![Startind-status](https://github.com/user-attachments/assets/ce59b492-f1a5-4f7e-b366-57d187afa23e)

![list-of nodes](https://github.com/user-attachments/assets/05fec64d-712a-4bd0-9da9-ef20de357504)

**Basic Format of K8s yaml manifest file:** (Use .yml extention for code file)

    apiVersion:
    kind:
    metadata:
       name:
       labels:
    spec:
       containers:
         - name: 
           image: 


## Only Launch Pod without any Deployment or else:

- Create file:
  
       notepad pod.yml

  ![pod-file](https://github.com/user-attachments/assets/31bc7b76-cb74-45b8-acfd-80ce94e5f257)

- Describe command:

       kubectl describe pods myonlypod
  
  ![Event](https://github.com/user-attachments/assets/705b1c75-5aa9-4dd7-8c51-dfabba52018b)

## Replication Controller: [rc]
- When we want to manage desired stage of pods with current stage of pods then we use Replication Controller K8s resource type.
- `replicas` , `selector` , `template` are rc modules/attributes

- While launching a pod using rc, we can give labels to pods, We also provides this pod labels to ReplicationController,
  So it helps to manage this pods with help of pods labels.
- Check list of rc command:

       kubectl get rc

- ReplicationController manifest file apply:

       notepad rc.yml
       kubectl create -f rc.yml
  
  ![rc-pic](https://github.com/user-attachments/assets/6ce5fe17-28ce-4ea6-8d52-150ae0805b0b)

- Describe rc: ( rc --launch--> Pods )
  
       kubectl describe rc myrc
  
  ![describe-rc](https://github.com/user-attachments/assets/ecc485f6-040c-4efc-bc78-e472f839d747)
    
- show lables command:

       kubectl get pods --show-labels
  
  ![show-labels](https://github.com/user-attachments/assets/a7ca666d-4942-4e74-9304-f250cd2db5ea)

- selector with show labels:

       kubectl get pods --selector team=prod --show-labels

  ![selector](https://github.com/user-attachments/assets/e72c836b-e0e3-41e5-bc1b-de130c8e1be0)

- If we want scale the replicas then we have Three way, 1st is go to yaml offline file add desired replicas and use `kubectl apply` command ,
   2nd use `kubectl scale rc myrc --replicas=5` command, & 3rd is `kubectl edit rc myrc` command this gives online edit file to us we just add replicas there.

  ![online edit](https://github.com/user-attachments/assets/88886139-a5b5-4e08-a58c-9250606bad24)

- get all command show all resources lists which created till now:

      kubectl get all
  
## Kubectl resorces type check and Explain 

- Show all types resources:

       kubectl api-resources

  ![api-resources](https://github.com/user-attachments/assets/d49bb840-a2ae-4439-8011-beeec2795de8)

- api versions list:

       kubectl api-versions

  ![api-versions](https://github.com/user-attachments/assets/960f34c0-c0fb-464b-8127-6990a2d1c5b3)

- Kubectl explain command:

       kubectl explain ReplicationController

  ![explain-cmd](https://github.com/user-attachments/assets/b86acb82-1ea3-49c9-a2df-f0e9f0010711)

- use explain cmd with option:
    
       kubectl explain ReplicationController.spec

  ![explain with more](https://github.com/user-attachments/assets/0be31c70-eb00-4584-a86c-88462dbc8ee9)

- more deep explain:

       kubectl explain ReplicationController.spec.template

  ![more-deep-explain](https://github.com/user-attachments/assets/d8cbc31f-8d95-497e-96c3-ab835c12793c)


 # Minikube dashboard:
 - This minikube dashboard command launch GUI dashboard of our cluster on browser:

       minikube dashboard -p pscluster2

   ![dashboard](https://github.com/user-attachments/assets/94a7d28c-7fb3-498b-b4cc-b7b853b4580a)

 - On Browser:
   ![GUI](https://github.com/user-attachments/assets/7fc09f08-ead0-413f-a50d-b6ea64d607fe)

## Delete all resources & delete cluster:

- Delete all resources in one command:

       kubectl delete all --all

- Delete cluster:

       minikube delete -p pscluster2

![Delete-all](https://github.com/user-attachments/assets/db56b80d-a336-4079-be8b-6ce2186c064f)
