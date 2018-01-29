# multicloud

AWS: https://github.com/shmcfarl/multicloud/tree/master/aws/cloudformation
- There are JSON and YAML versions of the CloudFormation templates.
- The first template/stack to build is with the "CsrStack-pw-cleaned" file. This file creates a new VPC, network, two subnets, routes, firewall rules and a single Cisco CSR1000v with two interfaces, static IPs on that CSR and also drops in the entire DMVPN configuration, interface configurations and OSPF configurations.
-The second template/stack to build is with the "CsrEipRoute" file. This file uses the stack name from the first stack build and adds an external/public IP to the outside (G1) CSR interface and also adds a route for the on-prem prefix.
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
