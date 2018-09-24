# multicloud

AWS: https://github.com/shmcfarl/multicloud/tree/master/aws/cloudformation
- The sample template creates a VPC, 2 subnets, a CSR, an EIP for the CSR, basic routes and security groups and dumps a sample DMVPN config on the CSR.
- Modify the file for your own naming, pre-shared keys for IPsec, and addressing.

Azure: https://github.com/shmcfarl/multicloud/tree/master/azure/resource-manager
- There is a single file that is used with the Azure Resource Manager.
- The file creates a new Resource Group, a new Vnet, subnets, routes, NSG, a new Cisco CSR 1000v with two interfaces, static IPs and an external/public IP on the outside (G1) CSR interface.
- The template also injects the full CSR configuration to include interfaces, routing, DMVPN.
- Modify the file for your own naming, pre-shared keys for IPsec, and addressing.
- The IOS config for the CSR begins on line 269 and after "customData":

GCP: https://github.com/shmcfarl/multicloud/tree/master/gcp/deployment-manager
- There are several files involved in the GCP Deployment Manager stack build.
- There is a top-level YAML file "gcp_main_stack.yaml" which imports all of the individual resource Jinja2 files (where the actual resources are built).
- There is a second stack template file "inside-private-routes.yaml" which imports single Jinja2 file that adds a private route to the on-prem network.
- You must deploy the yaml files using the gcloud CLI. Example: gcloud deployment-manager deployments create gcp-stack --config gcp_main_stack.yaml --automatic-rollback-on-error
- Deployment Manager will create a new inside subnet, routes, firewall rules, a new Cisco CSR 1000v with two interfaces, static IPs and an external/public IP on the outside (G1) CSR interface.
- NOTE: The Cisco CSR 1000v is not officially supported on GCP and it is under active development. The image is not yet available on GCP. When it is released, official documentation will be provided by Google and Cisco on how to use this image. I will also update my example template with the final release info.
