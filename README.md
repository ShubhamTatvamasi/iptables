# iptables

List the rules in a chain:
```bash
sudo iptables -L -n -v --line-number
```
> add `-n` flag for **numeric output of addresses and ports**

restore rules:
```bash
sudo iptables-restore < rules
```

change input policy to DROP:
```bash
sudo iptables --policy INPUT DROP
sudo iptables --policy FORWARD DROP
sudo iptables --policy OUTPUT ACCEPT
```

drop connection from specfic IP:
```bash
sudo iptables -I INPUT 1 -s 192.168.0.54 -j DROP

# Append rules
sudo iptables -A INPUT -s 192.168.0.54 -j DROP
```

accept everything on localhost:
```bash
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -A OUTPUT -o lo -j ACCEPT
```

allow icmp trafic:
```bash
sudo iptables -I OUTPUT 1 --proto icmp -j ACCEPT
```

delete rule number 3 from chain INPUT:
```bash
sudo iptables -D INPUT 3
```

allow destination port 22:
```bash
sudo iptables -A OUTPUT -p tcp --dport 22 -j ACCEPT
```

all new connections on port 80:
```bash
sudo iptables -A INPUT -p tcp --dport 80 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```

allow input from range 192.168.1.0/24 on port 3306:
```bash
sudo iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 3306 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
