# iptables

List the rules in a chain:
```bash
sudo iptables -L
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

