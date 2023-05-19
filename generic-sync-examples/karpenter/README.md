### Testing the karpenter CRD syncing

#### Prerequisits
* This example assumes that you have a an AWS EKS cluster configured with Karpeneter to provision nodes.
* Most of the examples listed here also create the related `ClusterRoles` and/or `Roles` needed for the relevant tool/framework.

1. Once you've followed the installation instructions for setting up and installing karpenter on the host cluster and verified that the installation works, proceed to the next step of creating the vcluster
2. Create a vcluster with the above config as a values file
  ```sh
    vcluster create vcluster -f https://raw.githubusercontent.com/loft-sh/vcluster/main/generic-sync-examples/karpenter/config.yaml
  ```
3. Connect to the vcluster and apply the crds. 
  ```sh
    kubectl apply -f https://raw.githubusercontent.com/loft-sh/vcluster/main/generic-sync-examples/karpenter/provisioner-node.yaml
  ```
4. Create a workload and set the nodeselector to match the labels set within the Provisioner. If not, the node will not be scheduled by karpenter. 
  ```yaml
  nodeSelector:
    project: vcluster
  ```