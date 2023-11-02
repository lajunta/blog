---
title: "New_firewall"
date: 2023-11-02T18:55:07+08:00
draft: false
---


New Firewall
===

###For School
```bash
#!/bin/bash
EXIF=eth2
T1=192.168.5.100
T2=192.168.7.100
N1=192.168.5.0/24
N2=192.168.7.0/24
E1=10.2.104.0/21
E2=172.16.1.0/24
iptables -F
iptables -X
iptables -t nat -F
iptables -t mangle -F

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
iptables -t nat -F
iptables -t nat -P PREROUTING ACCEPT
iptables -t nat -P POSTROUTING ACCEPT
iptables -t nat -P OUTPUT ACCEPT

iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p udp -j ACCEPT
iptables -t nat -A PREROUTING -p udp --dport 53 -j DNAT --to 172.16.1.3:53

iptables -A INPUT -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A FORWARD -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT
iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 3/m --limit-burst 5 -j ACCEPT
iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
iptables -A INPUT -p tcp -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -p udp -m state --state RELATED,ESTABLISHED -j ACCEPT

# allow T1 T2 visit localhost
iptables -A INPUT -s $T1 -j ACCEPT
iptables -A INPUT -s $T2 -j ACCEPT

# allow T1 T2 visit net
iptables -A FORWARD -s $T1 -j ACCEPT
iptables -A FORWARD -s $T2 -j ACCEPT
iptables -A FORWARD -d $T1 -j ACCEPT
iptables -A FORWARD -d $T2 -j ACCEPT

# allow N1 N2 visit school
iptables -A FORWARD -s $N1 -d $E1 -j ACCEPT
iptables -A FORWARD -s $N1 -d $E2 -j ACCEPT
iptables -A FORWARD -s $N2 -d $E1 -j ACCEPT
iptables -A FORWARD -s $N2 -d $E2 -j ACCEPT
iptables -A FORWARD -s $E1 -d $N1 -j ACCEPT
iptables -A FORWARD -s $E1 -d $N2 -j ACCEPT
iptables -A FORWARD -s $E2 -d $N1 -j ACCEPT
iptables -A FORWARD -s $E2 -d $N2 -j ACCEPT

# allow this localhost port visited
iptables -A INPUT -p tcp -m multiport --dports 20,21,22,44,80,135,137,138,139,389,445,8008,8829 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --dports 8080:8090,12321,9001:9010,27017,1090,1080,1070,7788,40000:50000 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --sports 20,22,53,80,135,139,389,445 -j ACCEPT

iptables -t nat -A POSTROUTING -o $EXIF -j MASQUERADE
echo "school" > /root/neteasy/current
```

### For Net5
```bash
#!/bin/bash
EXIF=eth2
FNAME=net5
T1=192.168.5.100
T2=192.168.7.100
N1=192.168.5.0/24
N2=192.168.7.0/24
E1=10.2.104.0/21
E2=172.16.1.0/24

iptables -F
iptables -X
iptables -t nat -F

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p udp -j ACCEPT                                                                                                                                        
iptables -A INPUT -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A FORWARD -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

iptables -t nat -A PREROUTING -p udp --dport 53 -j DNAT --to 172.16.1.3:53 

# allow T1 T2 visit localhost
iptables -A INPUT -s $T1 -j ACCEPT
iptables -A INPUT -s $T2 -j ACCEPT

# allow T2 visit net
iptables -A FORWARD -s $T2 -j ACCEPT
iptables -A FORWARD -d $T2 -j ACCEPT

# allow N1(including T1) visit net
iptables -A FORWARD -s $N1 -j ACCEPT
iptables -A FORWARD -d $N1 -j ACCEPT

# allow N2 visit school
iptables -A FORWARD -s $N2 -d $E1 -j ACCEPT
iptables -A FORWARD -s $E1 -d $N2 -j ACCEPT
iptables -A FORWARD -s $N2 -d $E2 -j ACCEPT
iptables -A FORWARD -s $E2 -d $N2 -j ACCEPT

# allow this localhost port visited
iptables -A INPUT -p tcp -m multiport --dports 20,21,22,80,135,139,389,445,8008,8829,8080:8090,12321 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --dports 9001:9010,27017,1090,1080,1070,7788,40000:50000 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --sports 20,22,53,80,135,139,389,445 -j ACCEPT
iptables -t nat -A POSTROUTING -o $EXIF -j MASQUERADE

echo $FNAME > /root/neteasy/current

```

### For Net7 

```bash
#!/bin/bash
EXIF=eth2
FNAME=net7
T2=192.168.5.100
T1=192.168.7.100
N2=192.168.5.0/24
N1=192.168.7.0/24
E1=10.2.104.0/21
E2=172.16.1.0/24

iptables -F
iptables -X
iptables -t nat -F

iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -p udp -j ACCEPT                                                                                                                                        
iptables -A INPUT -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A FORWARD -m pkttype --pkt-type broadcast -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

iptables -t nat -A PREROUTING -p udp --dport 53 -j DNAT --to 172.16.1.3:53 

# allow T1 T2 visit localhost
iptables -A INPUT -s $T1 -j ACCEPT
iptables -A INPUT -s $T2 -j ACCEPT

# allow T2 visit net
iptables -A FORWARD -s $T2 -j ACCEPT
iptables -A FORWARD -d $T2 -j ACCEPT

# allow N1(including T1) visit net
iptables -A FORWARD -s $N1 -j ACCEPT
iptables -A FORWARD -d $N1 -j ACCEPT

# allow N2 visit school
iptables -A FORWARD -s $N2 -d $E1 -j ACCEPT
iptables -A FORWARD -s $E1 -d $N2 -j ACCEPT
iptables -A FORWARD -s $N2 -d $E2 -j ACCEPT
iptables -A FORWARD -s $E2 -d $N2 -j ACCEPT

# allow this localhost port visited
iptables -A INPUT -p tcp -m multiport --dports 20,21,22,80,135,139,389,445,8008,8829,8080:8090,12321 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --dports 9001:9010,27017,1090,1080,1070,7788,40000:50000 -j ACCEPT
iptables -A INPUT -p tcp -m multiport --sports 20,22,53,80,135,139,389,445 -j ACCEPT
iptables -t nat -A POSTROUTING -o $EXIF -j MASQUERADE

echo $FNAME > /root/neteasy/current

```

### For AllNet

```bash
#!/bin/bash
EXIF=eth2
iptables -F
iptables -X
iptables -t nat -F

iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT

iptables -A INPUT -p icmp -j ACCEPT
iptables -A INPUT -p udp -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
iptables -t nat -A PREROUTING -p udp --dport 53 -j DNAT --to 172.16.1.3:53

iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

iptables -t nat -A POSTROUTING -o $EXIF -j MASQUERADE

echo "allnet" > /root/neteasy/current
```