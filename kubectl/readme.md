## Update Kubectl client version from 1.27 to 1.28

To interact with your cluster post-upgrade, ensure that you have the latest version of kubectl compatible with Kubernetes 1.27.
    
    curl -LO "https://dl.k8s.io/release/v1.28.0/bin/darwin/amd64/kubectl"
    chmod +x ./kubectl
    mv ./kubectl /usr/local/bin/kubectl

Checing the version of installed Kubectl

    kubectl version

    Example output:

    Client Version: v1.28.0
    Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
    Server Version: v1.27.13-eks-3af4770

## Upgrade EKS Control Plane

Using the AWS CLI, initiate the upgrade of your EKS cluster’s control plane to version 1.27.

    aws eks update-cluster-version --name gcc-application --kubernetes-version 1.28

Sample output:

    {
        "update": {
            "id": "bf2335f2-9ac0-3f47-930a-0cab779d8e99",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.28"
                },
                {
                    "type": "PlatformVersion",
                    "value": "eks.16"
                }
            ],
            "createdAt": "2024-07-27T17:28:54.300000+06:00",
            "errors": []
        }
    }

Monitor the upgrade status using the following command until it is "ACTIVE":

    aws eks describe-cluster --name gcc-application --query "cluster.status"


## Update EKS Node Groups

Once the control plane is updated, move on to your node groups. This ensures your nodes are in sync with the master’s version.
Find the Node Group name under AWS console > EKS > Compute > Node Groups

aws eks update-nodegroup-version --cluster-name gcc-application --nodegroup-name gcc-application-ng-public1 --kubernetes-version 1.27

Sample output:

    {
        "update": {
            "id": "515b8009-11e4-320f-86dc-d2d8f0ae381b",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.28"
                },
                {
                    "type": "ReleaseVersion",
                    "value": "1.28.8-20240703"
                }
            ],
            "createdAt": "2024-07-27T17:50:39.172000+06:00",
            "errors": []
        }
    }

Check status:

    kubectl get nodes



---------------------------

## Update Kubectl client version to 1.27

To interact with your cluster post-upgrade, ensure that you have the latest version of kubectl compatible with Kubernetes 1.27.
    
    curl -LO "https://dl.k8s.io/release/v1.27.0/bin/darwin/amd64/kubectl"
    chmod +x ./kubectl
    mv ./kubectl /usr/local/bin/kubectl

Checing the version of installed Kubectl

    kubectl version --short

    Example output:

    Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
    Client Version: v1.27.0
    Kustomize Version: v5.0.1
    Server Version: v1.26.15-eks-3af4770

## Upgrade EKS Control Plane

Using the AWS CLI, initiate the upgrade of your EKS cluster’s control plane to version 1.27.

    aws eks update-cluster-version --name gcc-application --kubernetes-version 1.27

Sample output:

    {
        "update": {
            "id": "21733a52-8cc1-32c8-9650-f855af2a3bcb",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.27"
                },
                {
                    "type": "PlatformVersion",
                    "value": "eks.17"
                }
            ],
            "createdAt": "2024-06-10T16:07:40.952000+06:00",
            "errors": []
        }
    }

Monitor the upgrade status using the following command until it is "ACTIVE":

    aws eks describe-cluster --name gcc-application --query "cluster.status"


## Update EKS Node Groups

Once the control plane is updated, move on to your node groups. This ensures your nodes are in sync with the master’s version.
Find the Node Group name under AWS console > EKS > Compute > Node Groups

aws eks update-nodegroup-version --cluster-name gcc-application --nodegroup-name gcc-application-ng-public1 --kubernetes-version 1.27

Sample output:

    {
        "update": {
            "id": "9ad019c9-afe1-31fa-b3e7-21d687b00b9e",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.27"
                },
                {
                    "type": "ReleaseVersion",
                    "value": "1.27.12-20240605"
                }
            ],
            "createdAt": "2024-06-10T16:32:38.647000+06:00",
            "errors": []
        }
    }

Check status:

    kubectl get nodes



---------------------------


## Update Kubectl client version to 1.26

To interact with your cluster post-upgrade, ensure that you have the latest version of kubectl compatible with Kubernetes 1.26.
    
    curl -LO "https://dl.k8s.io/release/v1.26.0/bin/darwin/amd64/kubectl"
    chmod +x ./kubectl
    mv ./kubectl /usr/local/bin/kubectl


## Upgrade EKS Control Plane

Using the AWS Management Console or the AWS CLI, initiate the upgrade of your EKS cluster’s control plane to version 1.26.

    aws eks update-cluster-version --name gcc-application --kubernetes-version 1.26

Sample output:

    {
        "update": {
            "id": "c79c7387-49fd-3a9e-abc0-84546e45b4f1",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.26"
                },
                {
                    "type": "PlatformVersion",
                    "value": "eks.18"
                }
            ],
            "createdAt": "2024-06-04T15:45:56.298000+06:00",
            "errors": []
        }
    }

Monitor the upgrade status using:

    aws eks describe-cluster --name gcc-application --query "cluster.status"


## Update EKS Node Groups

Once the control plane is updated, move on to your node groups. This ensures your nodes are in sync with the master’s version.
Find the Node Group name under AWS console > EKS > Compute > Node Groups

aws eks update-nodegroup-version --cluster-name gcc-application --nodegroup-name gcc-application-ng-public1 --kubernetes-version 1.26

Sample output:

    {
        "update": {
            "id": "eb8e6494-ab45-3269-a638-3b9ea9446c6c",
            "status": "InProgress",
            "type": "VersionUpdate",
            "params": [
                {
                    "type": "Version",
                    "value": "1.26"
                },
                {
                    "type": "ReleaseVersion",
                    "value": "1.26.15-20240522"
                }
            ],
            "createdAt": "2024-06-04T16:10:12.798000+06:00",
            "errors": []
        }
    }

Check status:

    kubectl get nodes

