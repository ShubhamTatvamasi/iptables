# iptables

List the rules in a chain:
```bash
sudo iptables -L
```

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

