### Full-configuration

```
show full-configuration
```

### Output settings

```
config system console   set output standardend
```

### Hostname

###### GET

```
show system global
```

###### SET

```
config system global   set hostname "fortigate-test-KVM-64"end
```

### Interface

###### GET

```
show system interface
```

###### SET

```
config system interface
   edit "port1"
       set vdom "root"
       set ip 192.168.1.59 255.255.255.0
       set allowaccess ping https ssh
       set type physical
       set snmp-index 1
   next
   edit "port2"
       set vdom "root"
       set type physical
       set snmp-index 2
   next
   edit "port3"
       set vdom "root"
       set type physical
       set snmp-index 3
   next
   edit "ssl.root"
       set vdom "root"
       set type tunnel
       set alias "SSL VPN interface"
       set snmp-index 4
   next
end
```

### Static route

###### GET

```
show router static
```

###### SET

```
config router static
   edit 1
       set status disable
       set dst 192.168.1.0 255.255.255.0
       set distance 1
       set weight 1
       set priority 1
       set device "port1"
       set comment "for test"
   next
end
```

### Logging

###### GET

```
show log setting
show log syslogd filter
show log syslogd setting
show log syslogd2 filter
show log syslogd2 setting
show log syslogd3 filter
show log syslogd3 setting
show log syslogd4 filter
show log syslogd4 setting
```

###### SET

```
config log syslogd$i filter   set severity notificationend
config log syslogd setting   set status enable   set server "192.168.1.99"   set port 5524end
```

### Address

###### GET

```
config log syslogd$i filter
   set severity notification
end

config log syslogd setting
   set status enable
   set server "192.168.1.99"
   set port 5524
end
```

###### SET

```
config firewall address
   edit "SSLVPN_TUNNEL_ADDR1"
       set uuid 05312aba-a6e0-51e8-1bde-9688c3b0e5eb
       set type iprange
       set associated-interface "ssl.root"
       set start-ip 10.212.134.200
       set end-ip 10.212.134.210
   next
   edit "all"
       set uuid 0532be84-a6e0-51e8-35fa-93ef6072f3cf
   next
   edit "none"
       set uuid 0532c4ec-a6e0-51e8-c50f-c4766862a4cd
       set subnet 0.0.0.0 255.255.255.255
   next
   edit "adobe"
       set uuid 0532ca14-a6e0-51e8-db9c-f30212ade1cb
       set type wildcard-fqdn
       set wildcard-fqdn "*.adobe.com"
   next
   edit "auth.gfx.ms"
       set uuid 0532e508-a6e0-51e8-937f-8621a4bc9e93
       set type fqdn
       set fqdn "auth.gfx.ms"
   next
   edit "fortinet"
       set uuid 053303ee-a6e0-51e8-302a-fc2d58779918
       set subnet 192.168.1.0 255.255.255.0
   next
```

### AddressGroup

###### GET

```
show firewall addrgrp
```

###### SET

```
config firewall addrgrp
   edit "demogrp"
       set uuid 45d60b34-a74f-51e8-d19c-4ce54a196ef8
       set member "skype" "citrix"
       set comment "demo grp"
   next
end

config firewall addrgrp
 edit "demogrp"
 append member "fortinet"
end
```

### Service

###### GET

```
show firewall service custom
```

###### SET

```
config firewall service custom
 edit "demosrv"
       set comment "asdf"
       set iprange 192.168.1.1
       set tcp-portrange 10-20:200-300
   next
   edit "tcp"
       set comment "tcp service"
       set tcp-portrange 10-20:23-45
   next
   edit "udp"
       set udp-portrange 10-20:45-1213
   next
   edit "ip"
       set protocol IP
       set protocol-number 45
   next
   edit "multi-protocol"
       set protocol ICMP
       unset icmptype
   next
   edit "icmp"
       set protocol ICMP
       set icmptype 8
       set icmpcode 0
   next
   edit "icmp6"
       set protocol ICMP6
       set icmptype 80
       set icmpcode 90
   next
end
```

### ServiceGroup

###### GET

```
show firewall service group
```

###### SET

```
config firewall service group
   edit "Email Access"
       set member "DNS" "IMAP" "IMAPS" "POP3" "POP3S" "SMTP" "SMTPS"
   next
   edit "Web Access"
       set member "DNS" "HTTP" "HTTPS"
   next
   edit "Windows AD"
       set member "DCE-RPC" "DNS" "KERBEROS" "LDAP" "LDAP_UDP" "SAMBA" "SMB"
   next
   edit "Exchange Server"
       set member "DCE-RPC" "DNS" "HTTPS"
   next
end
```

### Policy

###### GET

```
show firewall policy
```

###### SET

```
config firewall policy
   edit 1
       set name "demo-policy-1"
       set uuid c6b95774-a781-51e8-012c-cba800a0634f
       set srcintf "any"
       set dstintf "port1"
       set srcaddr "fortinet" "google-play"
       set dstaddr "all"
       set action accept
       set schedule "always"
       set service "tcp" "udp"
       set logtraffic disable
       set devices "ip-phone"
       set comments "demo"
   next
end
```

### Interface policy

可以对接口定义policy，相当于从该接口进来或者出去的流量都会应用这个策略。

### Scheduler

###### GET

```
show firewall schedule group

show firewall schedule onetime

show firewall schedule recurring
```

###### SET

```

config firewall schedule group
   edit "demo"
       set member "always" "none"
   next
end

config firewall schedule onetime
   edit "onetime-demo"
       set start 12:00 2001/12/01
       set end 00:00 2050/12/30
   next
end

config firewall schedule recurring
   edit "always"
       set day sunday monday tuesday wednesday thursday friday saturday
   next
   edit "none"
   next
   edit "recurring"
       set start 13:00
       set end 14:00
   next
end
```

###### Weekday

```
sunday       Sunday.
monday       Monday.
tuesday     Tuesday.
wednesday   Wednesday.
thursday     Thursday.
friday       Friday.
saturday     Saturday.
none         None.
```

### NAT

##### Pool(Dynamic (PAT))

###### GET

```
show firewall ippool
```

###### SET

```
config firewall ippool
    edit "inner2outter"
        set type overload
        set startip 122.1.1.1
        set endip 122.1.1.1
        set arp-reply enable
        set arp-intf "port2"
        set comments "hhhaaaa"
end
config firewall policy
    edit 3
        set srcintf "port1"
        set dstintf "port2"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set ippool enable
        set poolname "inner2outter"
        set schedule "always"
        set service "ALL"
        set nat enable
    next
end
```



##### STATIC/DNAT

```
-----DNAT-----
config firewall vip
    edit v1
        set comment "dnat"
        set src-filter 102.1.1.1 105.1.1.0/24 106.1.1.1-106.1.1.2
        set extip 155.1.1.1
        set mappedip 192.168.182.78
        set extintf port2
        set arp-reply enable
        set portforward enable
        set protocol tcp
        set extport 80-80
        set mappedport 90-90
        set portmapping-type 1-to-1
end
 
 
config firewall policy
    edit 4
        set srcintf "port2"
        set dstintf "port1"
        set srcaddr "all"
        set dstaddr "v1"
        set action accept
        set schedule "always"
        set service "ALL"
    next
end
-----STATIC-----
config firewall vip
    edit v2
        set comment "static"
        set type static-nat
        set src-filter 102.1.1.1 105.1.1.0/24 106.1.1.1-106.1.1.2
        set extip 155.1.1.22
        set mappedip 192.168.182.79
        set extintf port2
        set arp-reply enable
        set portforward enable
        set protocol tcp
        set extport 80-80
        set mappedport 90-90
        set portmapping-type 1-to-1
end
config firewall policy
    edit 5
        set srcintf "port2"
        set dstintf "port1"
        set srcaddr "all"
        set dstaddr "v2"
        set action accept
        set schedule "always"
        set service "ALL"
    next
end
```

##### SNAT ()

###### GET

```
show firewall policy central-snat-map
```

#### fortinet Configuring NAT

##### SNAT

![img](/Users/fangcong/source/study-log/md/../images/fortinetSNAT.png)

> Source Network Address Translation (SNAT) is an option available in Transparent mode and configurable in CLI only, using the following commands:

```fortran
config firewall ippool
	edit "nat-out"
        set endip 192.168.183.48
        set startip 192.168.183.48
        set interface vlan18_p3
	next
end

config firewall policy
	edit 3
        set srcintf "vlan160_p2"
        set dstintf "vlan18_p3"
        set srcaddr "all"
        set dstaddr "all"
        set action accept
        set ippool enable
        set poolname "nat-out"
        set schedule "always"
        set service "ANY"
        set nat enable
	next
end
```

##### DNAT

> The following example shows how to configure Destination Network Address Translation (DNAT) using a virtual IP on a FortiGatein Transparent Mode:

```fortran
config firewall vip
    edit "vip1"
        set extip 192.168.183.48
        set extintf "vlan160_p2"
        set mappedip 192.168.182.78
	next
end

config firewall policy
	edit 4
        set srcintf "vlan160_p2"
        set dstintf "vlan18_p3"
        set srcaddr "all"
        set dstaddr "vip1"
        set action accept
        set schedule "always"
        set service "ANY"
	next
end
```

##### Static NAT

> In Static NAT one internal IP address is always mapped to the same public IP address.
>
> In FortiGate firewall configurations this is most commonly done with the use of Virtual IP addressing.
>
> An example would be if you had a small range of IP addresses assigned to you by your ISP and you wished to use one of those IP address exclusively for a particular server such as an email server.
>
> Say the internal address of the Email server was 192.168.12.25 and the Public IP address from your assigned addresses range from 256.16.32.65 to 256.16.32.127. Many readers will notice that because one of the numbers is above 255 that this is not a real Public IP address. The Address that you have assigned to the interface connected to your ISP is 256.16.32.66, with 256.16.32.65 being the remote gateway. You wish to use the address of 256.16.32.70 exclusively for your email server.
>
> When using a Virtual IP address you set the external IP address of 256.16.32.70 to map to 192.168.12.25. This means that any traffic being sent to the public address of 256.16.32.70 will be directed to the internal computer at the address of 192.168.12.25
>
> When using a Virtual IP address, this will have the added function that when ever traffic goes from 192.168.12.25 to the Internet it will appear to the recipient of that traffic at the other end as coming from 256.16.32.70.
>
> You should note that if you use Virtual IP addressing with the Port Forwarding enabled you do not get this reciprocal effect and must use IP pools to make sure that the outbound traffic uses the specified IP address.

