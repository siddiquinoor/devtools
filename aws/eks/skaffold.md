# Introduction

## Understanding Microservices: https://www.cuelogic.com/blog/microservices-in-practice-from-architecture-to-deployment

## Installing VPS server using Digital Ocean free $100 Credits

### Installing Kubernetes a VPS on Ubuntu 20.04

Ref: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

# Deployment

## Using Kubernetes in Digital ocean

### Create Kubernetes cluster and running by following documentation available in DigitalOcean

Then run:
$ brew install doctl
$ doctl auth init

    Create Registry using `doctl`
    $ doctl registry create edge-gcc

    Login in the registry
    $ doctl registry login

    Now we can push our docker images into the DO Registry
    First build all docker images and then run

    $ docker tag admin registry.digitalocean.com/edge-gcc/admin
    $ docker tag server registry.digitalocean.com/edge-gcc/server
    $ docker tag client registry.digitalocean.com/edge-gcc/client

    Then Push all these images into DO
    $ docker push registry.digitalocean.com/edge-gcc/admin
    $ docker push registry.digitalocean.com/edge-gcc/server
    $ docker push registry.digitalocean.com/edge-gcc/client

    Run:
    $ docker run -p 80:80 registry.digitalocean.com/edge-gcc/admin
    $ docker run -p 80:80 registry.digitalocean.com/edge-gcc/server
    $ docker run -p 80:80 registry.digitalocean.com/edge-gcc/client

# Docker

    First update the system
    $ sudo apt-get update

    Ref: https://docs.docker.com/engine/install/ubuntu/

    $ sudo apt-get install ca-certificates curl gnupg lsb-release

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


    $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    Now update again
    $ sudo apt-get update

    $ sudo apt-get install docker-ce docker-ce-cli containerd.io

# Installing NodeJS

    $ sudo apt install nodejs

# Install Kubernetes

# Skaffold

    - Installing Skaffold: https://skaffold.dev/docs/install/
        - curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/latest/skaffold-darwin-amd64 && \
          sudo install skaffold /usr/local/bin/

    - In EC2
        $ curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/latest/skaffold-linux-amd64 && sudo install skaffold /usr/local/bin/

    - Installing ingress-nginx: https://kubernetes.github.io/ingress-nginx/deploy/
        $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.0/deploy/static/provider/cloud/deploy.yaml

    check the running Kubernetes ingress load balancer
        $ kubectl get svc -n ingress-nginx



    Check docker is running on port 80
        $ sudo lsof -i tcp:80
        This will print something like:
        COMMAND    PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
        com.docke 8263 user  113u  IPv6 0xa20e89998489120d      0t0  TCP *:http (LISTEN)

        if not then kill the other process

    Check Kubernetes is running

        $ kubectl cluster-info

# Adding docker image for auth

    $ docker build -t siddiquinoor/admin .

# Pushing docker image to docker hub

    $ docker push siddiquinoor/admin

# Running Skaffold

    $ skaffold dev

# SSL Error in Chrome (in local there is no way to test the virtual server)

    On the SSL error tab click on any empty space and type "thisisunsafe" (withou quotes)

# Form validation

    use https://www.npmjs.com/package/express-validator
    $ npm install express-validator

# Error Handling

    Expressjs Error Handling

# Install Express Async Errors

    from npmjs.com

# Install types of mongoose for type support

    $ npm install @types/mongoose

# Using JSON webtoken

    from npmjs.com jsonwebtoken

# Cookie Session

    $ npm install cookie-session @types/cookie-session

# jsonwebtoken

    $ npm install jsonwebtoken @types/jsonwebtoken

# Cookie verificaiton

    Initiate a Signup using https://edge.com/users/signup and copy the Cookie from the cookie tab then Go to the website https://base64decode.org and decode the cookie.
    Then from that jwt key copy the value and go to this site: jwt.io and paste it. Then from the bottom right your-256-bit-secret modify the value as you used as 'asdf' as a secret key. Check if jwt.io show "Signature Verified"
     const userJwt = jwt.sign({
        id: user.id,
        email: user.email
    }, 'asdf');

# Secrets

    $ kubectl get secrets

# Add cookie secret into Pod's environment veriable 'asdf' is the key here

    $ kubectl create secret generic jwt-secret --from-literal JWT_KEY=asdf

# Diagnosis of Pods error

    $ kubectl get pods
    Find that all pods are running without any any error

    $ kubectl describe pod <name-of-the-pod-from-the-previous-command>

# Check JavaScript heap size

    $ node -e 'console.log(v8.getHeapStatistics().heap_size_limit/(1024*1024))'

    Set it to 4GB
    $ export NODE_OPTIONS=--max_old_space_size=4096

# Implement Test using supertest (npmjs.com)

    $ npm install --save-dev @types/jest @types/supertest jest ts-jest supertest mongodb-memory-server

# Delete and re-run a POD inside Kubernetes

    $ kubectl get pods
    This will list all the running pods. Copy the NAME of the POD we want to delete for example 'client-depl-cdf8c5867-5hjd2'
    Now lets delete the POD 'client-depl-cdf8c5867-5hjd2'

    $ kubectl delete pod client-depl-cdf8c5867-5hjd2

    Kubernetes will re-create the pod again, to see that run the list of POD again:
    $ kubectl get pods
    This will list the pod again showing that AGE <few seconds>

# Working on Client

## Install TailwindCSS inside our client app

    Follow other DevTools doc in GitHub

# Install axios

    $ npm install axios

# Bug fixing of "Error: getaddrinfo ENOTFOUND ingress-nginx-controller.ingress-nginx.svc.cluster.local"

    - Installing ingress-nginx: https://kubernetes.github.io/ingress-nginx/deploy/
        $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml

# Ingress error: "Error from server (InternalError): error when creating "STDIN": Internal error occurred: failed calling webhook "validate.nginx.ingress.kubernetes.io": Post "https://ingress-nginx-controller-admission.ingress-nginx.svc:443/networking/v1/ingresses?timeout=10s": dial tcp 10.104.92.126:443: connect: connection refused"

    $ kubectl delete -A ValidatingWebhookConfiguration ingress-nginx-admission
    Ref: https://stackoverflow.com/questions/67212876/error-when-creating-stdin-internal-error-occurred-while-running-skaffold-dev

# Print kubernetes namespaces

    $ kubectl get namespace

    Output:

    NAME              STATUS   AGE
    default           Active   7d4h
    ingress-nginx     Active   7h35m
    kube-node-lease   Active   7d4h
    kube-public       Active   7d4h
    kube-system       Active   7d4h

# Print kubernetes services

    $ kubectl get services

    Output:
    NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)     AGE
    server-mongo-srv   ClusterIP   10.97.91.194   <none>        27017/TCP   132m
    server-srv         ClusterIP   10.100.81.82   <none>        3000/TCP    132m
    client-srv       ClusterIP   10.110.178.8   <none>        3000/TCP    132m
    kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP     7d4h

# Print services inside a namespace

    $ kubectl get services -n ingress-nginx

    Output:

    NAME                                 TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
    ingress-nginx-controller             LoadBalancer   10.96.234.241   localhost     80:30563/TCP,443:30907/TCP   7h37m
    ingress-nginx-controller-admission   ClusterIP      10.106.206.8    <none>        443/TCP                      7h37m

# Skaffold dev deploy the following images so far

Starting deploy...

- deployment.apps/auth-depl created
- service/auth-srv created
- deployment.apps/auth-mongo-depl created
- service/auth-mongo-srv created
- deployment.apps/client-depl created
- service/client-srv created
- ingress.networking.k8s.io/ingress-service created

# AWS SSH Login

    First set permission to the .cer or .pem file as following:
    $ chmod 400 mykey.cer
    $ ssh -i EC2UbuntuKey.cer ubuntu@54.215.90.217


    Mouse:  defaults write .GlobalPreferences com.apple.mouse.scaling 8
            defaults read .GlobalPreferences com.apple.mouse.scaling

# Admin panel

## Install MongoDB in local machine (process are mostly same for all other platform)

Go to the site and download the installation file: https://www.mongodb.com/try/download/community
Copy all the file inside the directory in a specific folder like: /Documents/Project/MongoDB

Installation guideline: https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x-tarball/

    $ sudo cp /Documents/Project/MongoDB/bin/* /usr/local/bin/
    $ sudo ln -s  /Documents/Project/MongoDB/bin/* /usr/local/bin/
    $ sudo mkdir -p /usr/local/var/mongodb
    $ sudo mkdir -p /usr/local/var/log/mongodb
    $ sudo chown my_mongodb_user /usr/local/var/mongodb
    $ sudo chown my_mongodb_user /usr/local/var/log/mongodb

## Run Mongo DB

    $ mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork
    $ mongod --dbpath /usr/local/var/mongodb

### Run MongoD from a config file automatically create a config file

    $ sudo nano /usr/local/etc/mongod.conf
    Add configuration like the following
    ```
    systemLog:
        destination: file
        path: "/var/log/mongodb/mongod.log"
        logAppend: true
    storage:
        journal:
            enabled: true
    processManagement:
        fork: true
    net:
        bindIp: 127.0.0.1
        port: 27017
    setParameter:
        enableLocalhostAuthBypass: false
    ...
    ```

    $ mongod --config /usr/local/etc/mongod.conf

## Mongo running error fixing in Mac: Ref: https://stackoverflow.com/questions/63562177/mongod-aborts-on-mac

    Check the service error log to know about the error:
    $ code /usr/local/var/log/mongodb/mongo.log

    Check if the log says the following:
    `Failed to unlink socket file","attr":{"path":"/tmp/mongodb-27017.sock","error":"Permission denied"`
    That means somehow permission denied to access the mongodb socket

    Remote the socket file:
    $ sudo rm -rf /tmp/mongodb-27017.sock

    Run the server again:
    $ mongod --dbpath /usr/local/var/mongodb --logpath /usr/local/var/log/mongodb/mongo.log --fork

## Mongo GUI editor

Inside the downloaded folder there is a file named `install_compass` run it to install
If anything goes wrong Go to the Mac System Preference and allow it to open

## Go to application and find `MongoDB Compass.app` to run the GUI of the MongoDB

### Run the Project

    $ npm install
    $ npm start

# Run all services

    - Change configuration on .env file inside Admin
        - SERVER=edge.com
        - isLocal=false
    - Create JWT secret Key
    -

    $ admin  -> docker build -t siddiquinoor/admin .
    $ admin  -> docker push siddiquinoor/admin
    $ server -> docker build -t siddiquinoor/server .
    $ server -> docker push siddiquinoor/server
    $ client -> docker build -t siddiquinoor/client .
    $ client -> docker push  siddiquinoor/client
    $

# Mongo deployment Error:

- deployment/server-mongo-depl: container server-mongo is waiting to start: mongo can't be pulled
  - pod/server-mongo-depl-dbc9b845f-5m8pd: container server-mongo is waiting to start: mongo can't be pulled
- deployment/server-mongo-depl failed. Error: container server-mongo is waiting to start: mongo can't be pulled.
  Cleaning up...
- deployment.apps "admin-depl" deleted
- service "admin-srv" deleted
- deployment.apps "client-depl" deleted
- service "client-srv" deleted
- ingress.networking.k8s.io "ingress-service" deleted
- deployment.apps "server-depl" deleted
- service "server-srv" deleted
- deployment.apps "server-mongo-depl" deleted
- service "server-mongo-srv" deleted
  1/4 deployment(s) failed

### Solution: Download the mongo pod using the docker command

    - Pull Mongo using command line

    $ docker pull mongo

    - Then run

    $ skaffold dev

## Troubleshoot everything is running but site not showing up like edge.com or edge.com/admin

### Solution check the following

    - First check all Pods are running well

    $ kubectl get pods

    Output:

    NAME                                READY   STATUS    RESTARTS   AGE
    admin-depl-76bb9d77d8-tql28         1/1     Running   0          50m
    client-depl-56b8f57f8d-c4bhj        1/1     Running   0          50m
    server-depl-85f65689cc-8sx77        1/1     Running   0          50m
    server-mongo-depl-8c78bc446-8kv7g   1/1     Running   0          50m



    - Check all services

    $ kubectl get services

    Output should like the following:

    NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)     AGE
    admin-srv          ClusterIP   10.107.16.13     <none>        3000/TCP    49m
    client-srv         ClusterIP   10.110.152.187   <none>        3000/TCP    49m
    kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP     25h
    server-mongo-srv   ClusterIP   10.106.111.173   <none>        27017/TCP   49m
    server-srv         ClusterIP   10.108.50.219    <none>        3000/TCP    49m



    - Check Namespace that specially ingress-nginx is running or not

    $ kubectl get namespace

    Output should like the following:

    NAME              STATUS   AGE
    default           Active   25h
    ingress-nginx     Active   72s
    kube-node-lease   Active   25h
    kube-public       Active   25h
    kube-system       Active   25h

    If the ingress nginx not found then run the following command and run deployment again

    $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.1.2/deploy/static/provider/cloud/deploy.yaml

    $ skaffold dev

    Deployment end without loosing any data use:
    $ skaffold dev --cleanup=false

# REST API not returning the whole page HTML instead of the actual JSON data

    - Check the Networking related Ingress file and check the path exposed or not
    $ nano infra/k8s/ingress-srv.yaml

# jQuery onclick not working when navigating back to Resources page for the filter options

## Solution found on: https://github.com/vercel/next.js/issues/4477#issuecomment-1017817919

## Signup and Signin Error not registering cookie

### Check that cookie is storing in the browser, if not then reset browser cookie will solve this issue, but importantly this should be fixed re-generating new cookie

## Heading over the Mongo Database inside a Kubernetes cluster

### Executing bash inside Mongo Pod

    $ kubectl get pod
    $ kubectl exec -i <pod-name> bash
    $ mongosh
    $ show dbs // show all database
    $ use <db-name> // use any database
    $ db // current database
    $ show collections // show all collections

    Set a specific collection in the current database to a variable coll, as in the following example:
    $ coll = db.<collection>;
    Find all:
    $ coll.find();

# Server error

## In browser: 502 Server Error

## In server log:

    $ [server] Error: Debug Failure. False expression: Non-string value passed to `ts.resolveTypeReferenceDirective`, likely by a wrapping package working with an outdated `resolveTypeReferenceDirectives` signature. This is probably not a problem in TS itself.

## Solution: https://stackoverflow.com/questions/72374103/running-a-simple-express-app-with-ts-node-dev-and-get-error-false-expression-n

    $ Just change the `ts-node-dev` version from `1.1.8` to `2.0.0-0` in my package.json file, then run `npm install` again, and the error disappears.

# Client Error: autoprefixer: Replace color-adjust to print-color-adjust. The color-adjust shorthand is currently deprecated

Solution: https://stackoverflow.com/questions/72163411/react-bootstarp-warning-about-color-adjust/72164969#72164969

    $ npm install autoprefixer@10.4.5 --save-exact

---

# Amazon Elastic Kubernetes Service endpoints and quotas

(Ref: https://docs.aws.amazon.com/general/latest/gr/eks.html)
$ Europe (London) eu-west-2 eks.eu-west-2.amazonaws.com HTTPS

## Install kubectl for AWS

Ref: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

## EKS IAM Role

Ref: https://docs.aws.amazon.com/eks/latest/userguide/create-node-role.html#create-worker-node-role

## Step 1: Create your Amazon EKS cluster and nodes

### Ref: https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html

    $$ eksctl create cluster --name <my-cluster> --region <region-code> --fargate
    $ eksctl create cluster --name edge-daemon --region eu-west-2 --fargate

    Output:
    Cluster creation takes several minutes. During creation you'll see several lines of output. The last line of output is similar to the following example line.

    `...
    2022-05-12 00:05:09 [ℹ]  building cluster stack "eksctl-edge-daemon-cluster"
    2022-05-12 00:05:12 [ℹ]  deploying stack "eksctl-edge-daemon-cluster
    [✓]  EKS cluster "my-cluster" in "region-code" region is ready`

### \*\*\*\* If NEEDED can Delete a cluster

    $ **** eksctl delete cluster --region=eu-west-2 --name=edge-daemon

### Check AWS cloudformation list

    $ aws cloudformation list-stacks --region eu-west-2

### Delete a specific cloudformaiton

    $ aws cloudformation delete-stack --region eu-west-2 --stack-name eksctl-edge-daemon-cluster

##

### Create ECR in AWS console then copy the URL like below

    $$ like 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-daemon

## Run the command to docker login using the URI of ECR without the name

    $ aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 761799505441.dkr.ecr.eu-west-2.amazonaws.com

## Docker build image for AWS ECR:

    $ docker build -t siddiquinoor/admin .
    $ docker build -t siddiquinoor/server .
    $ docker build -t siddiquinoor/client .
    $ docker pull mongo

## Docker TAG images to AWS ECR:

    $ docker tag siddiquinoor/admin:latest 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-admin
    $ docker tag siddiquinoor/server:latest 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-server
    $ docker tag siddiquinoor/client:latest 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-client
    $ docker tag mongo:latest 761799505441.dkr.ecr.eu-west-2.amazonaws.com/mongo

## Docker Push images to AWS ECR:

    $ docker push 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-admin
    $ docker push 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-server
    $ docker push 761799505441.dkr.ecr.eu-west-2.amazonaws.com/edge-client
    $ docker push 761799505441.dkr.ecr.eu-west-2.amazonaws.com/mongo

## Enable Fargate logging:

https://docs.aws.amazon.com/eks/latest/userguide/fargate-logging.html

Fargate logging policy created:

{
"Policy": {
"PolicyName": "eks-fargate-logging-policy",
"PolicyId": "ANPA3CXWJ6YQYKBC2TMXG",
"Arn": "arn:aws:iam::761799505441:policy/eks-fargate-logging-policy",
"Path": "/",
"DefaultVersionId": "v1",
"AttachmentCount": 0,
"PermissionsBoundaryUsageCount": 0,
"IsAttachable": true,
"CreateDate": "2022-05-12T15:42:47+00:00",
"UpdateDate": "2022-05-12T15:42:47+00:00"
}
}
(END)

aws iam attach-role-policy \
 --policy-arn arn:aws:iam::761799505441:policy/eks-fargate-logging-policy \
 --role-name eksctl-edge-daemon-cluster-FargatePodExecutionRole-1AAL3KANYP5M9

To create a task execution IAM role (AWS CLI)

Create a file named ecs-tasks-trust-policy.json that contains the trust policy to use for the IAM role. The file should contain the following:

{
"Version": "2012-10-17",
"Statement": [
{
"Sid": "",
"Effect": "Allow",
"Principal": {
"Service": "ecs-tasks.amazonaws.com"
},
"Action": "sts:AssumeRole"
}
]
}

Create an IAM role named ecsTaskExecutionRole using the trust policy created in the previous step.

aws iam create-role \
 --role-name ecsTaskExecutionRole \
 --assume-role-policy-document file://ecs-tasks-trust-policy.json

aws iam attach-role-policy \
 --role-name ecsTaskExecutionRole \
 --policy-arn arn:aws:iam::aws:policy/service-role/AmazonECSTaskExecutionRolePolicy

curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/aws-iam-authenticator
chmod +x ./aws-iam-authenticator
mkdir -p $HOME/bin
cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$HOME/bin:$PATH

# Update Kubectl config

Ref: https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html

    $ aws eks update-kubeconfig --region region-code --name cluster-name
    $ aws eks update-kubeconfig --region eu-west-2 --name edge-daemon

    Test:
    $ kubectl get svc

    Output:
    NAME             TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    svc/kubernetes   ClusterIP   10.100.0.1   <none>        443/TCP   1m

---

# Using EC2 managed nodes - Linux

    $ eksctl create cluster --name edge-daemon --region eu-west-2

    View Kubernetes resources:

    $ kubectl get nodes -o wide
    Example output:

    NAME                                            STATUS   ROLES    AGE    VERSION              INTERNAL-IP      EXTERNAL-IP     OS-IMAGE         KERNEL-VERSION                  CONTAINER-RUNTIME
    ip-192-168-12-49.region-code.compute.internal   Ready    <none>   6m7s   v1.22.6-eks-d1db3c   192.168.12.49    52.35.116.65    Amazon Linux 2   5.4.156-83.273.amzn2.x86_64   docker://20.10.7
    ip-192-168-72-129.region-code.compute.internal  Ready    <none>   6m4s   v1.22.6-eks-d1db3c   192.168.72.129   44.242.140.21   Amazon Linux 2   5.4.156-83.273.amzn2.x86_64   docker://20.10.7

    View the workloads running on your cluster.
    $ kubectl get pods -A -o wide


    If needed delete the cluster
    $ $$eksctl delete cluster --name edge-daemon --region eu-west-2


    Deploying applications:
    $ kubectl apply -f infra/k8s/server-mongo-depl.yaml
    $ kubectl apply -f infra/k8s/admin-depl.yaml
    $ kubectl apply -f infra/k8s/server-depl.yaml
    $ kubectl apply -f infra/k8s/client-depl.yaml

-- **\*\*** ------------------- **\*** ------------- \***\*\*\*\*\***\*\***\*\*\*\*\***

# Deploying in AWS

## Creating Cluster

    $ eksctl create cluster --name=edge-gcc \
                      --region=eu-west-2 \
                      --without-nodegroup

### There should have no nodes available, lets check it

    $ kubectl get nodes

### Check cluster

    $ eksctl get clusters

## Create & Asociate IAM OIDC (Open ID Connect) provider for our EKS Cluster

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.2/deploy/installation/

    $ eksctl utils associate-iam-oidc-provider \
    --region eu-west-2 \
    --cluster edge-gcc \
    --approve

## Create EC2 Keypair

    $ Go to AWS console and then EC2 and create a new keypair

## Creating Nodegroups

    $ eksctl create nodegroup --cluster=edge-gcc \
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

    $ kubectl get nodes
    $ kubectl get nodes -o wide

### List EKS clusters

    $ eksctl get cluster

### List NodeGroups in a cluster

    $ eksctl get nodegroup --cluster=edge-gcc

### List Nodes in current kubernetes cluster

    $ kubectl get nodes -o wide

### Our kubectl context should be automatically changed to new cluster

    $ kubectl config view --minify

### Login into the EC2 instance (Worker Nodes)

    $ ssh -i edge-gcc-keypair.cer ec2-user@18.133.253.204

### Check storage space used

    $ df -h

### If needed to access via Nodeport we must set edit security group and add a new Inbound rules as

    All traffic Protocol (All) Port range (All) Source (Anywhere) from the AWS console

### Delete cluster

    $ $$ eksctl  delete cluster cluster_name

### Check for IAM Service account in a cluster

    $ eksctl get iamserviceaccount --cluster=edge-gcc

### Download the latest IAM policy

    $ curl -o iam_policy_latest.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/main/docs/install/iam_policy.json

### Create IAM Policy using policy downloaded

    $ aws iam create-policy \
        --policy-name AWSLoadBalancerControllerIAMPolicy \
        --policy-document file://iam_policy_latest.json

### Policy ARN

arn:aws:iam::761799505441:policy/AWSLoadBalancerControllerIAMPolicy

### Check for any service account available for awl-load-balancer-controller

    $ kubectl get sa -n kube-system
    $ kubectl get sa aws-load-balancer-controller -n kube-system

### Create IAM Role using eksctl

    $ eksctl create iamserviceaccount --cluster=edge-gcc --namespace=kube-system --name=aws-load-balancer-controller --attach-policy-arn=arn:aws:iam::761799505441:policy/AWSLoadBalancerControllerIAMPolicy --override-existing-serviceaccounts --approve

### Verify the IAM role

    $ eksctl get iamserviceaccount --cluster=edge-gcc
    $ kubectl get sa -n kube-system
    $ kubectl get sa aws-load-balancer-controller -n kube-system

### Describe Service Account aws-load-balancer-controller

    $ kubectl describe sa aws-load-balancer-controller -n kube-system

## Using HELM3 Add the eks-charts repository.

    $ helm repo add eks https://aws.github.io/eks-charts

### Update your local repo to make sure that you have the most recent charts.

    $ helm repo update

## Install the AWS Load Balancer Controller.

    $ helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=edge-gcc --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set region=eu-west-2 --set vpcId=vpc-0dbffb4498dff156f --set image.repository=602401143452.dkr.ecr.eu-west-2.amazonaws.com/amazon/aws-load-balancer-controller

### Verify that the controller is installed.

    $ kubectl -n kube-system get deployment
    $ kubectl -n kube-system get deployment aws-load-balancer-controller
    $ kubectl -n kube-system describe deployment aws-load-balancer-controller

### Verify AWS Load Balancer Controller Webhook service created

    $ kubectl -n kube-system get svc
    $ kubectl -n kube-system get svc aws-load-balancer-webhook-service
    $ kubectl -n kube-system describe svc aws-load-balancer-webhook-service

## Verify Labels in Service and Selector Labels in Deployment

    $ kubectl -n kube-system get svc aws-load-balancer-webhook-service -o yaml
    $ kubectl -n kube-system get deployment aws-load-balancer-controller -o yaml

## Verify AWS Load Balancer Controller Logs

### List Pods

    $ kubectl get pods -n kube-system

### Review logs for AWS LB Controller POD-1

    $ kubectl -n kube-system logs -f  aws-load-balancer-controller-68cb6d74cb-lzkvw

### Review logs for AWS LB Controller POD-2

    $ kubectl -n kube-system logs -f aws-load-balancer-controller-68cb6d74cb-q55d4

### Verify AWS Load Balancer Controller k8s Service Account - Internals

#### List Service Account and its secret

    $ kubectl -n kube-system get sa aws-load-balancer-controller
    $ kubectl -n kube-system get sa aws-load-balancer-controller -o yaml

### Uninstall (if needed) AWS Load Balancer Controller

    $ $$ helm uninstall aws-load-balancer-controller -n kube-system

### Add IngressClass as a default Ingress class inside AWS

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/ingress_class/

    $ apiVersion: networking.k8s.io/v1
        kind: IngressClass
        metadata:
            name: my-aws-ingress-class
            annotations:
                ingressclass.kubernetes.io/is-default-class: "true"
        spec:
            controller: ingress.k8s.aws/alb

### Create JWT secret for Client-Server token based communicaiton

    $ kubectl create secret generic jwt-secret --from-literal JWT_KEY=asdf

## Finally run all our deployment

    $ kubectl apply -f infra/aws/server-mongo-depl.yaml
    $ kubectl apply -f infra/aws/admin-depl.yaml
    $ kubectl apply -f infra/aws/client-depl.yaml
    $ kubectl apply -f infra/aws/server-depl.yaml

### Check all pods

    $ kubectl get pods

## Deployment of the Ingress service

Ref: https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.4/guide/ingress/annotations/

    $ kubectl apply -f infra/aws/ingress-srv.yaml

## Delete (if needed) all deployment

    $ $$ kubectl apply -f infra/aws/ingress-default-class.yaml
    $ $$ kubectl apply -f infra/aws/server-mongo-depl.yaml
    $ $$ kubectl apply -f infra/aws/admin-depl.yaml
    $ $$ kubectl apply -f infra/aws/client-depl.yaml
    $ $$ kubectl apply -f infra/aws/server-depl.yaml
    $ $$ kubectl apply -f infra/aws/ingress-srv.yaml

## Verify all deployments

    $ kubectl get pods
    $ kubectl get services
    $ kubectl get ingress   # Get the DNS or public URL to visit the application e.g. ingress-service-rules-847778227.eu-west-2.elb.amazonaws.com
    $ kubectl describe ingress ingress-service  # check for any Warning under the Events section
    $ kubectl get pods -n kube-system   # Checking load balancer
    $ kubectl get services -n kube-system # Checking the running service related to the load balancer
    $ kubectl -n kube-system logs -f aws-load-balancer-controller-68cb6d74cb-lzkvw

API Client: http://edge-service-rules-1711676827.eu-west-2.elb.amazonaws.com/

# Troubleshooting inside PODs

## Deleting services

    $ kubectl delete service admin-srv

## Expose a service mentioning port

    $ kubectl expose pod admin-depl-85bb4b8896-lrj72  --type=NodePort --port=3000 --target-port=3000 --name=admin-srv

## See Kubernetes configuration file

    $ kubectl get service admin-srv -o yaml

## Show logs

    $ kubectl logs admin-depl-85bb4b8896-lrj72

## Show logs and watch

    $ kubectl logs -f admin-depl-85bb4b8896-lrj72

## Get public IP of the EC2 instance or Kubernetes Nodes

    $ kubectl get nodes -o wide

## Get Kubernetes Deployment

    $ kubectl get deploy -A

## Delete everything related to Kubernetes

    $ kubectl get all
    $ kubectl delete -f infra/aws/admin-depl.yaml -f infra/aws/client-depl.yaml -f infra/aws/ingress-srv.yaml -f infra/aws/server-depl.yaml -f infra/aws/server-mongo-depl.yaml
    $ OR kubectl delete -f infra/k8s/

---

# Docker build for Production

## Build docker using -f flag for the Docker config file name

    $ docker build -f Dockerfile.prod -t siddiquinoor/mongo .
    $ docker build -f Dockerfile.prod -t siddiquinoor/admin .
    $ docker build -f Dockerfile.prod -t siddiquinoor/server .
    $ docker build -f Dockerfile.prod -t siddiquinoor/client .

## Docker push as well

    $ docker push siddiquinoor/mongo
    $ docker push siddiquinoor/admin
    $ docker push siddiquinoor/server
    $ docker push siddiquinoor/client

# Good bye Docker Desktop for Mac and start using Colima (https://github.com/abiosoft/colima)

Before using `Colima` I had to uninstall the Docker Desktop from my Mac by following the link below:
Ref: https://stackoverflow.com/questions/44346109/how-to-easily-install-and-uninstall-docker-on-macos/65468254#65468254

Then I follow the Github link to install `Colima`: https://github.com/abiosoft/colima

    $ brew install colima
    $ brew install docker

Then I was running Colima by the following command

    $ colima start --kubernetes

Then run CD `skaffold dev` but it shows an error that Docker Daemon is not found.

I ran `docker info` and have found the there was no information related to `Server`.

After searching a lot and posting question to StackOverflow finally spending a day I have found a solution which was then I posted as an answer to my StackOverflow question:

Ref: https://stackoverflow.com/questions/72557053/why-does-docker-daemon-is-not-found/72560928#72560928

So basically I needed to set the Docker host for the Docker Daemon which is inside Colima. I ran the the following command:

    $ export DOCKER_HOST="unix://$HOME/.colima/docker.sock"

and then

    $ docker info

Now everything seems good.

    $ skaffold dev  // ran well

Now the continuous development using Skaffold seems working fine but the Client was not running :( shwoing that Axios create error

Then I checked the used resources for Clima and found that Colima was using 2 GB RAM by default so I re-configured it as the following:

    $ colima start --cpu 2 --memory 4 --kubernetes

After all the above everything worked like charm :))

///**\*\*\*** _////////////////////\***\*\*\*\*\***//_////\***\*\*\*\*\***\*\***\*\*\*\*\***

# IMPORTANT NOTES BEFORE DEPLOYMENT

## Connect to AWS EKS Kubernetes for kubectl

### https://www.youtube.com/watch?v=uLnrHqzoArc

    $ aws eks --region eu-west-2 update-kubeconfig --name edge-gcc

## Kubectl setting up default context

### TO list all available config run:

    $ kubectl config get-contexts

    Get the name from the above command and then run:

    $ kubectl config use-context CONTEXT_NAME
    ex:
    $ kubectl config use-context CONTEXT_NAME

    Veriry kubectl comman:
    $ kubectl get service

    Output:
    NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)           AGE
    admin-srv          NodePort    10.100.176.135   <none>        3000:31510/TCP    54d
    client-srv         NodePort    10.100.164.241   <none>        3000:31284/TCP    54d
    kubernetes         ClusterIP   10.100.0.1       <none>        443/TCP           68d
    server-mongo-srv   NodePort    10.100.8.244     <none>        27017:32471/TCP   54d
    server-srv         NodePort    10.100.207.66    <none>        3000:32705/TCP    54d

## Change in Admin service for local or online status

    $ Change `IS_LOCAL=false` in `admin/.env` file

## Change Environment in Admin service

    $ Change `ENVIRONMENT=development` or `ENVIRONMENT=production` depending on the context

## Change Environment in Client service

    $ Change `ENVIRONMENT=prod` or `ENVIRONMENT=dev` depending on the context in `client/.env.local`

## Change AWS ALB or the Public DNS according to the ALB URI

    $ Change `API_AWS=http://edge-service-rules-424877693.eu-west-2.elb.amazonaws.com` in `client/.env.local`

## Check for the deployment configuration files under the `Infrastructure` directory

    $ There are 2 seperate folders. One for local and other for AWS

## Create JWT Secret

    $ kubectl create secret generic jwt-secret --from-literal JWT_KEY=asdf
