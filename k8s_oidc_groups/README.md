# Setup AzureAD OIDC on ARO with OIDC based mapping for groups

This directory contains Terraform config that is used to add `OpenID Azure AD` oAuth Identity Provider as well
as add AzureAD secret to an existing ARO cluster. It is similar to the terraform code in k8s_oidc directory with addition of the group mapper introduced starting with OCP 4.10 (https://mobb.ninja/docs/idp/group-claims/aro/ for details)
  
Execute following commands and substitute all the properties values with correct values in `custom.tfvars` file:
```
cp custom.tfvars.template custom.tfvars
```

_Use `<prefix>RG-app-service-principal.json` in [create_cluster_n_gen_kubeconfig](../create_cluster_n_gen_kubeconfig)
directory to populate values for the following variables, in `custom.tfvars` file:_
| custom.tfvars field | &lt;prefix&gt;RG-app-service-principal.json property |
| -------- | ------- |
| `tenant_id`  | `tenant`    |
| `client_id`  | `appId`    |
| `client_secret`  | `password`    |

Using the `custom.tfvars` file will allow his file to be used for variables instead of being prompted for each variable.

To generate `kubeconfig`, execute following commands:
```
./run.sh
```
  
This script will allow you to initialize `terraform` or `import` or `plan` or `apply` the
changes.
  
  When running in `plan` mode, it will prompt to ask for whether to use file or prompt for variables:
  * File/prompt - give `file` as the value
  
    If `prompt` value is provided for previous input, it will prompt for the following variable values:
    * Resource prefix
    * ARO cluster name
    * Tenant ID
    * Client ID
    * Client Secret
  
  Some of these fields have default values but can be overridden by providing
  new values. Once all the values are provided the script invokes `terraform`
  by passing in the input values to corresponding variables needed by the
  Terraform scripts.
  
  To run Terraform without using the script, please use the following command
  (substitute values with correct ones)
  ```
  terraform plan -out main.tfplan -var-file=custom.tfvars
  ```
  
**To add the `oidc`, follow these steps by inputting `file` when prompted for file/prompt:**
* Select `import`
* Once the import completes successfully, execute `./run.sh` again and select
  `plan`, and then select `apply` when prompted to choose between apply and destroy
* Once the plan completes successfully, execute `./run.sh` again and select
  `apply`
* Once `apply` runs
  
## Variables used in this module:
  * `cluster_name`: Name of the ARO cluster
  * `tenant_id`: Tenant ID
  * `client_id`: Client ID
  * `client_secret`: Client Secret (password)
