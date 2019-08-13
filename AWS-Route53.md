### Route 53

#### Routing Policy

- Simple routing - If you choose the simple routing policy, you can only have one record with multiple IP addresses. If you specify multiple values in a record, Route 53 returns all values to the user in a random order.

- Weighted routing - Allow you to split your traffic based on different weights assigned. For example, 10% of your traffic go to US-EAST-1 and 90% go to EU-WEST-1.

- Latency-based routing - Allow you to route your traffic based on the lowest network latency for your end user.

- Failover routing - Failover routing is used when you want to create an active/passive set up. For example, you want your primary site to be in US-EAST-1 and secondary disaster recovery site in EU-WEST-1.

- Geolocation routing - Geolocation routing lets you choose where your traffic will be sent based on the geographic location of your users.

- Mutivalue answer routing - Let you configure Route 53 to return multiple values. This is similar to simple routing however it allows you to put health checks on each record set.
