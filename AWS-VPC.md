### VPC (Virtual Private Cloud)

- VPC is an isolated network in a region that spans across multiple Availability Zones. Each EC2 or RDS instance you launch needs to be attached to a VPC. You need to assign an IP range to your VPC, for example, `172.31.0.0/16`, which is a private IP range. The `/16` indicates the size of the addresses you can use.

- A subnet must be placed in an Availability Zone and cannot span multiple Availability Zones. You first define your own IP range for your VPC (`172.31.0.0/16`), and then each subnet takes a subset of the VPC IP range. For example, we can have three subnets with `172.31.0.0/24`, `172.31.1.0/24` and `172.31.2.0/24` IP ranges respectively. The last digit of the IP range is used to denote the machine for the subnet. So each subnet can contain around 256 IP addresses in this case. These internal IPs are assigned to instances for internal communications within the VPC. 

- Public subnets usually contains:
  - Load balancers
  - Static websites
  - Files
  - Public authentication layers

- Private subnets usually contains:
  - Web application servers
  - Databases

- Route tables contain rules for which packets go where. You can create and assign different route tables to different subnets.

- An Internet Gateway is the only way the outside world can communicate with your VPC.

- Security Group operates at instance level. It supports allow rules only. It is stateful, which means return traffic is automatically allowed regardless of any rules.

- Network ACL operates at subnet level. It supports allow and deny rules. It is stateless, which means return traffic must be explicitly allowed by rules.

- Flow Logs can operate at VPC, subnet or instance level.

- It's possible to use a VPN to connect to a VPC (and access all the private IP straight from your laptop).

- You can peer VPC (within or across accounts) to make it look like they're part of the same network.
