[[_TOC_]]

# Introduction

Two types of deployment:

Installer-Provisioned Infrastructure (IPI) deployment
User-Provisioned Infrastructure (UPI) deploymentent
Agnostic (Bare-metal) deployment

![Provider Installation](./static/D00-OCP-Deploy-0.png)
![Provider Installation](./static/D00-OCP-Deploy-1.png)

# Pre-requisites

## DNS

```
# ocp.myhybridcloud.com
sudo yum install bind bind-utils -y
sudo systemctl enable --now named
sudo firewall-cmd --permanent --add-port=53/tcp
sudo firewall-cmd --permanent --add-port=53/udp
sudo firewall-cmd --reload
```

```
# Create the sub domain
sudo cat << EOF >>  /etc/named.conf
zone "ocp.myhybridcloud.com" IN {
type master;
file "/var/named/ocp.myhybridcloud.com.db";
allow-query { any; };
allow-transfer { none; };
allow-update { none; };
};
zone "1.168.192.in-addr.arpa" IN {  
type master;  
file "/var/named/1.168.192.in-addr.arpa";
allow-update { none; };
};
EOF

```

```
# Create a forwarding zone
sudo cat <<EOF > /var/named/ocp.myhybridcloud.com.db
;[1] Begin Common Header Definition
\$TTL 86400
@ IN SOA bastion.ocp.myhybridcloud.com. root.ocp.myhybridcloud.com. (
202201010001 ;Serial
21600 ;Refresh
3600 ;Retry
604800 ;Expire
86400 ;Minimum TTL
)
;End Common Header Definition
;Name Server Information [2]
   IN NS bastion.ocp.myhybridcloud.com.
;IP address of Name Server [3]
bastion IN A 192.168.1.200
;api internal and external purposes [4]
api        IN    A    192.168.1.200 
api-int    IN    A    192.168.1.200 
;wildcard application [5]
*.apps     IN    A    192.168.1.200
;bootstrap node to start cluster install only [6]
bootstrap  IN    A    192.168.1.90 
;master nodes [7]
master1    IN    A    192.168.1.91 
master2    IN    A    192.168.1.92 
master3    IN    A    192.168.1.93
;worker nodes [8]
worker1    IN    A    192.168.1.101
worker2    IN    A    192.168.1.102
EOF

[1]: Common DNS zone header.
[2]: The nameserver will be its own Bastion server.
[3]: The IP address from the nameserver (Bastion IP).
[4]: These records are mandatory and need to point to the VIP that will be used for the OpenShift API functions. In our case, we are using the bastion server as the VIP (suitable only for lab environments).
[5]: Wildcard VIP record used for the applications that run on OpenShift. In our case, we are using the bastion server as the VIP (suitable only for lab environments).
[6]: Bootstrap node IP record, used only for the cluster installation and can be removed after it.
[7]: Master node IP records, where the control plane objects will be hosted.
[8]: Worker node IP records, where the workloads will run. If you go for a three-node cluster, disregard the worker hosts.
```

```
# Create a reverse zone file
sudo cat <<EOF > /var/named/1.168.192.in-addr.arpa
\$TTL 1W @    IN    SOA    bastion.ocp.myhybridcloud.com.root (     
2019070700 ; serial 
3H         ; refresh (3 hours) 
30M        ; retry (30 minutes) 
2W         ; expiry (2 weeks) 
1W )       ; minimum (1 week) 
5.1.168.192.in-addr.arpa. IN PTR 
api.ocp.myhybridcloud.com.;
5.1.168.192.in-addr.arpa. IN PTR 
api-int.ocp.myhybridcloud.com.;
90.1.168.192.in-addr.arpa. IN PTR 
bootstrap.ocp.myhybridcloud.com.; 
91.1.168.192.in-addr.arpa. IN PTR 
master1.ocp.myhybridcloud.com.; 
92.1.168.192.in-addr.arpa. IN PTR 
master2.ocp.myhybridcloud.com.; 
93.1.168.192.in-addr.arpa. IN PTR 
master3.ocp.myhybridcloud.com.; 
101.1.168.192.in-addr.arpa. IN PTR 
worker1.ocp. myhybridcloud.com.; 
102.1.168.192.in-addr.arpa. IN PTR 
worker2.ocp. myhybridcloud.com.;
EOF
```
> Important Notes:
> Do not create a reverse zone record for the application's wildcard VIP, as that will lead to the wrong DNS resolution.
> If you created it for a three-node cluster, disregard the worker A and PTR records.

```
sudo systemctl restart named
dig +short @192.168.1.200 api.ocp.myhybridcloud.com
dig +short @192.168.1.200 api-int.ocp.myhybridcloud.com
```

## DNS




# References

https://github.com/PacktPublishing/OpenShift-Multi-Cluster-Management-Handbook/tree/main/chapter05

