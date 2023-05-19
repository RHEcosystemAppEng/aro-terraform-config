# aro-terraform-config

This repo contains Terraform config for creating an ARO cluster along with the resource group and
service principal. It also generates the kubeconfig and updates OAuth spec for the ARO cluster.

There are a few directories with Terraform config in them. Here is some detail
on these directories:
* [create_cluster_n_gen_kubeconfig](create_cluster_n_gen_kubeconfig/README.md)
  * This directory contains code to handle creation of Resource Group, Service Principal
    as well as the ARO cluster.
  * It also generates a `kubeconfig` for the newly created ARO cluster.

* [k8s_oidc](k8s_oidc/README.md)
  * This directory contains Terraform config that can be used to import existing `oidc` resource
    and add `oidc AAD` identity provider as well as create a `Secret` for AzureAD.

* [k8s_oidc_groups](k8s_oidc_groups/README.md)
 * This directory contains Terraform config that can be used to import existing `oidc` resource
   with additional `groups` claim to enable mapping between AAD groups and kubernetes groups (https://mobb.ninja/docs/idp/az-ad-grp-sync/ ) and add `oidc AAD` identity provider as well as create a `Secret` for AzureAD.

## Note
Please make sure that the `kube_config_path` variable has same value in the two directories above
