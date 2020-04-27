### Route 53

Route53 is a managed DNS (Domain Name System). DNS is a collection of rules and records which helps clients understanding how to reach a server through URLs.

In AWS, the most common records are:

- A: URL to IPv4
- AAAA: URL to IPv6
- CNAME: URL to URL
- Alias: URL to AWS resource

Always prefer to use Alias over CNAME for performance reasons. For example, you can set up an Alias record to redirect a domain name (dennisxiao.com) to an Application Load Balancer DNS name.

#### Routing Policy

- Simple routing - If you choose the simple routing policy, you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.

- Weighted routing - Allow you to split your traffic based on different weights assigned. For example, 10% of your traffic go to US-EAST-1 and 90% go to EU-WEST-1.

- Latency-based routing - Allow you to route your traffic based on the lowest network latency for your end user.

- Failover routing - Failover routing is used when you want to create an active/passive set up. For example, you want your primary site to be in US-EAST-1 and secondary disaster recovery site in EU-WEST-1.

- Geolocation routing - Use when you want to route traffic based on the location of your users.

- Geoproximity routing - Use when you want to route traffic based on the location of your resources.

- Mutivalue answer routing - Let you configure Route 53 to return multiple values. This is similar to simple routing however it allows you to put health checks on each record set.
