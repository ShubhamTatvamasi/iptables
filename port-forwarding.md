# Port Forwarding

Check if port forwarding is enabled:
```bash
sudo sysctl -a | grep -i eth0.forwarding
```

Enable port forwarding:
```bash
sudo sysctl net.ipv4.conf.eth0.forwarding=1
```

---

Get default interface device name:
```bash
INTERFACE=$(ip -4 route ls | grep default | grep -Po '(?<=dev )(\S+)' | head -1)
echo $INTERFACE
```

Get default interface IP:
```bash
INTERFACE_IP=$(ip -o -4 addr list $INTERFACE | awk '{print $4}' | cut -d'/' -f1)
echo $INTERFACE_IP
```

Get the VM IP:
```bash
VM_IP=$(sudo virsh domifaddr ubuntu | tail -2 | head -1 | awk '{print $4}' | cut -d'/' -f1)
echo $VM_IP
```

Create port forwarding rules for port 80 and 443:
```bash
PORT=443
PORT=80

sudo -E bash -c "iptables -t nat -I PREROUTING -i $INTERFACE -p tcp -d $INTERFACE_IP --dport $PORT -j DNAT --to-destination $VM_IP:$PORT -m comment --comment nginx"
```

List all the rules:
```bash
sudo iptables -t nat -L --line-numbers
```

Delete the rule `1` for IP tables:
```bash
sudo iptables -t nat -D PREROUTING 1
```

---


Simple NAT Rule:
```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport $PORT -j DNAT --to-destination $VM_IP:$PORT
```

