# Deploying in AWS

## Creating Cluster

    eksctl create cluster --name=edge-gcc \
                      --region=eu-west-2 \
                      --without-nodegroup

### There should have no nodes available, lets check it

    kubectl get nodes

### Check cluster

    eksctl get clusters

## Create & Asociate IAM OIDC (Open ID Connect) provider for our EKS Cluster

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.2/deploy/installation/

    eksctl utils associate-iam-oidc-provider \
    --region eu-west-2 \
    --cluster edge-gcc \
    --approve

## Create EC2 Keypair

    Go to AWS console and then EC2 and create a new keypair

## Creating Nodegroups

    eksctl create nodegroup --cluster=edge-gcc \
                       --region=eu-west-2 \
                       --name=edge-gcc-ng-public \
                       --node-type=t3.medium \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=edge-gcc-keypair \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access

## Check if those nodes are ready

    kubectl get nodes
    kubectl get nodes -o wide

### List EKS clusters

    eksctl get cluster

### List NodeGroups in a cluster

    eksctl get nodegroup --cluster=edge-gcc

### List Nodes in current kubernetes cluster

    kubectl get nodes -o wide

### Our kubectl context should be automatically changed to new cluster

    kubectl config view --minify

### Login into the EC2 instance (Worker Nodes)

    ssh -i edge-gcc-keypair.cer ec2-user@18.133.253.204

### Check storage space used

    df -h

### If needed to access via Nodeport we must set edit security group and add a new Inbound rules as

    All traffic Protocol (All) Port range (All) Source (Anywhere) from the AWS console

### Delete cluster **** IMPORTANT :: CHECK BEFORE DELETE (IF DELETE NEEDED)

    eksctl  delete cluster cluster_name

### Check for IAM Service account in a cluster

    eksctl get iamserviceaccount --cluster=edge-gcc

### Download the latest IAM policy

    curl -o iam_policy_latest.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json

### Create IAM Policy using policy downloaded

    aws iam create-policy \
        --policy-name AWSLoadBalancerControllerIAMPolicy \
        --policy-document file://iam_policy_latest.json

### Policy ARN

arn:aws:iam::761799505441:policy/AWSLoadBalancerControllerIAMPolicy

### Check for any service account available for awl-load-balancer-controller

    kubectl get sa -n kube-system
    kubectl get sa aws-load-balancer-controller -n kube-system

### Create IAM Role using eksctl

    eksctl create iamserviceaccount --cluster=edge-gcc --namespace=kube-system --name=aws-load-balancer-controller --attach-policy-arn=arn:aws:iam::761799505441:policy/AWSLoadBalancerControllerIAMPolicy --override-existing-serviceaccounts --approve

### Verify the IAM role

    eksctl get iamserviceaccount --cluster=edge-gcc
    kubectl get sa -n kube-system
    kubectl get sa aws-load-balancer-controller -n kube-system

### Describe Service Account aws-load-balancer-controller

    kubectl describe sa aws-load-balancer-controller -n kube-system

## Creating AWS Load Balancer Controller Deployment using Helm

    # Install `helm` if it is not already installed
    brew install helm

## Using HELM3 Add the eks-charts repository.

    helm repo add eks https://aws.github.io/eks-charts
### Update your local repo to make sure that you have the most recent charts.

    helm repo update

## Install the AWS Load Balancer Controller.

### Note
- Check for the clusterName
- Check for the region
- Get the VPC ID from AWS Console and change it
- Get the image.repository URL from this link and change it (https://docs.aws.amazon.com/eks/latest/userguide/add-ons-images.html)

    helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=edge-gcc --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set region=eu-west-2 --set vpcId=vpc-0dbffb4498dff156f --set image.repository=602401143452.dkr.ecr.eu-west-2.amazonaws.com/amazon/aws-load-balancer-controller

### Verify that the controller is installed.

    kubectl -n kube-system get deployment
    kubectl -n kube-system get deployment aws-load-balancer-controller
    kubectl -n kube-system describe deployment aws-load-balancer-controller

### Verify AWS Load Balancer Controller Webhook service created

    kubectl -n kube-system get svc
    kubectl -n kube-system get svc aws-load-balancer-webhook-service
    kubectl -n kube-system describe svc aws-load-balancer-webhook-service

## Verify Labels in Service and Selector Labels in Deployment

    kubectl -n kube-system get svc aws-load-balancer-webhook-service -o yaml
    kubectl -n kube-system get deployment aws-load-balancer-controller -o yaml

## Verify AWS Load Balancer Controller Logs

### List Pods

    kubectl get pods -n kube-system

### Review logs for AWS LB Controller POD-1

    kubectl -n kube-system logs -f  aws-load-balancer-controller-68cb6d74cb-lzkvw

### Review logs for AWS LB Controller POD-2

    kubectl -n kube-system logs -f aws-load-balancer-controller-68cb6d74cb-q55d4

### Verify AWS Load Balancer Controller k8s Service Account - Internals

#### List Service Account and its secret

    kubectl -n kube-system get sa aws-load-balancer-controller
    kubectl -n kube-system get sa aws-load-balancer-controller -o yaml

### Uninstall (if needed) AWS Load Balancer Controller  **** IMPORTANT :: CHECK BEFORE UNINSTALL (IF UNINSTALL NEEDED)

    helm uninstall aws-load-balancer-controller -n kube-system

### Add IngressClass as a default Ingress class inside AWS

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/ingress_class/

1. Create a new file named `ingress-default-class.yaml` to deploy using `kubectl apply -f <file_name>` and add the following code:
```
    apiVersion: networking.k8s.io/v1
        kind: IngressClass
        metadata:
            name: my-aws-ingress-class
            annotations:
                ingressclass.kubernetes.io/is-default-class: "true"
        spec:
            controller: ingress.k8s.aws/alb
```

### Create JWT secret for Client-Server token based communicaiton

    kubectl create secret generic jwt-secret --from-literal JWT_KEY=asdf

## Finally run all our deployment

    kubectl apply -f infra/aws/server-mongo-depl.yaml
    kubectl apply -f infra/aws/admin-depl.yaml
    kubectl apply -f infra/aws/client-depl.yaml
    kubectl apply -f infra/aws/server-depl.yaml

### Check all pods

    kubectl get pods

## Deployment of the Ingress service

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/annotations/

    kubectl apply -f infra/aws/ingress-srv.yaml

## Delete (if needed) all deployment ***** IMPORTANT :: CHECK BEFORE DELETION (IN THERE IS ANY NEED)

    kubectl apply -f infra/aws/ingress-default-class.yaml
    kubectl apply -f infra/aws/server-mongo-depl.yaml
    kubectl apply -f infra/aws/admin-depl.yaml
    kubectl apply -f infra/aws/client-depl.yaml
    kubectl apply -f infra/aws/server-depl.yaml
    kubectl apply -f infra/aws/ingress-srv.yaml

## Verify all deployments

    kubectl get pods
    kubectl get services
    kubectl get ingress   # Get the DNS or public URL to visit the application e.g. ingress-service-rules-847778227.eu-west-2.elb.amazonaws.com
    kubectl describe ingress ingress-service  # check for any Warning under the Events section
    kubectl get pods -n kube-system   # Checking load balancer
    kubectl get services -n kube-system # Checking the running service related to the load balancer
    kubectl -n kube-system logs -f aws-load-balancer-controller-68cb6d74cb-lzkvw

API Client: http://edge-service-rules-1711676827.eu-west-2.elb.amazonaws.com/

# Troubleshooting inside PODs

## Deleting services

    kubectl delete service admin-srv

## Expose a service mentioning port

    kubectl expose pod admin-depl-85bb4b8896-lrj72  --type=NodePort --port=3000 --target-port=3000 --name=admin-srv

## See Kubernetes configuration file

    kubectl get service admin-srv -o yaml

## Show logs

    kubectl logs admin-depl-85bb4b8896-lrj72

## Show logs and watch

    kubectl logs -f admin-depl-85bb4b8896-lrj72

## Get public IP of the EC2 instance or Kubernetes Nodes

    kubectl get nodes -o wide

## Get Kubernetes Deployment

    kubectl get deploy -A

## Delete everything related to Kubernetes

    kubectl get all
    kubectl delete -f infra/aws/admin-depl.yaml -f infra/aws/client-depl.yaml -f infra/aws/ingress-srv.yaml -f infra/aws/server-depl.yaml -f infra/aws/server-mongo-depl.yaml
    OR kubectl delete -f infra/k8s/

---

# Docker build for Production

## Build docker using -f flag for the Docker config file name

    docker build -f Dockerfile.prod -t siddiquinoor/mongo .
    docker build -f Dockerfile.prod -t siddiquinoor/admin .
    docker build -f Dockerfile.prod -t siddiquinoor/server .
    docker build -f Dockerfile.prod -t siddiquinoor/client .

## Docker push as well

    docker push siddiquinoor/mongo
    docker push siddiquinoor/admin
    docker push siddiquinoor/server
    docker push siddiquinoor/client

# Good bye Docker Desktop for Mac and start using Colima (https://github.com/abiosoft/colima)

Before using `Colima` I had to uninstall the Docker Desktop from my Mac by following the link below:
Ref: https://stackoverflow.com/questions/44346109/how-to-easily-install-and-uninstall-docker-on-macos/65468254#65468254

Then I follow the Github link to install `Colima`: https://github.com/abiosoft/colima

    brew install colima
    brew install docker

Then I was running Colima by the following command

    colima start --kubernetes

Then run CD `skaffold dev` but it shows an error that Docker Daemon is not found.

I ran `docker info` and have found the there was no information related to `Server`.

After searching a lot and posting question to StackOverflow finally spending a day I have found a solution which was then I posted as an answer to my StackOverflow question:

Ref: https://stackoverflow.com/questions/72557053/why-does-docker-daemon-is-not-found/72560928#72560928

So basically I needed to set the Docker host for the Docker Daemon which is inside Colima. I ran the the following command:

    export DOCKER_HOST="unix://$HOME/.colima/docker.sock"

and then

    docker info

Now everything seems good.

    skaffold dev  // ran well

Now the continuous development using Skaffold seems working fine but the Client was not running :( shwoing that Axios create error

Then I checked the used resources for Clima and found that Colima was using 2 GB RAM by default so I re-configured it as the following:

    colima start --cpu 2 --memory 4 --kubernetes

After all the above everything worked like charm :))

///**\*\*\*** _////////////////////\***\*\*\*\*\***//_////\***\*\*\*\*\***\*\***\*\*\*\*\***

# IMPORTANT NOTES BEFORE DEPLOYMENT

## Connect to AWS EKS Kubernetes for kubectl

### https://www.youtube.com/watch?v=uLnrHqzoArc

    aws eks --region eu-west-2 update-kubeconfig --name edge-gcc

## Kubectl setting up default context

### TO list all available config run:

    kubectl config get-contexts

    Get the name from the above command and then run:

    kubectl config use-context CONTEXT_NAME
    ex:
    kubectl config use-context CONTEXT_NAME

    Veriry kubectl comman:
    kubectl get service

    Output:
    NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)           AGE
    admin-srv          NodePort    10.100.176.135   <none>        3000:31510/TCP    54d
    client-srv         NodePort    10.100.164.241   <none>        3000:31284/TCP    54d
    kubernetes         ClusterIP   10.100.0.1       <none>        443/TCP           68d
    server-mongo-srv   NodePort    10.100.8.244     <none>        27017:32471/TCP   54d
    server-srv         NodePort    10.100.207.66    <none>        3000:32705/TCP    54d

## Change in Admin service for local or online status

    Change `IS_LOCAL=false` in `admin/.env` file

## Change Environment in Admin service

    Change `ENVIRONMENT=development` or `ENVIRONMENT=production` depending on the context

## Change Environment in Client service

    Change `ENVIRONMENT=prod` or `ENVIRONMENT=dev` depending on the context in `client/.env.local`

## Change AWS ALB or the Public DNS according to the ALB URI

    Change `API_AWS=http://edge-service-rules-424877693.eu-west-2.elb.amazonaws.com` in `client/.env.local`

## Check for the deployment configuration files under the `Infrastructure` directory

    There are 2 seperate folders. One for local and other for AWS

## Create JWT Secret

    kubectl create secret generic jwt-secret --from-literal JWT_KEY=asdf
