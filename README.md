# multicloud

AWS: https://github.com/shmcfarl/multicloud/tree/master/aws/cloudformation
- There are JSON and YAML versions of the CloudFormation templates.
- The first template/stack to build is with the "CsrStack-pw-cleaned" file. This file creates a new VPC, network, two subnets, a single Cisco CSR1000v with two interfaces, static IPs on that CSR and also drops in the entire DMVPN configuration, interface configurations and OSPF configurations.
The second template/stack to build is with the "CsrEipRoute" file. This file uses the stack name from the first stack build and adds an External/Public IP to the outside (G1) CSR interface and also adds a route for the on-prem prefix.
