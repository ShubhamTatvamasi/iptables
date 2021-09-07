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
