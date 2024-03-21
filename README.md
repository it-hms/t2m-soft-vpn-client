# Talk2m Software Client Example 
Copyright © 2024 HMS Industrial Networks Inc

This project provides and example VPN client for Talk2M for Linux devices.

## Functionality
- Talk2M vpn client functionality
- LAN traffic routing via NAT (masquerade)
- Broadcast traffic encapsulation for PLC discovery 

## Requirements 
Use with Linux environments that include the following dependencies options:
- iptables 
- kernel configured to enable IP masquerading
- docker 
- Talk2M account and device certificates
- IP forwarding enabled 
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

## How to use 
Best practices are to make sure that security keys are never loaded to Github projects. To aid in this an example VPN configuration file is provided. The project already has git ignore the file **vpn/vpn.conf**

1. Copy the example VPN client configuration file to **vpn/vpn.conf**. This file name is used by the container and is ignored by the git configuration. 
```bash 
cp vpn/example.conf vpn/vpn.conf
```

2. Copy the device key, to **vpn/vpn.conf** between the key tags.
```openvpn
<key>
-----BEGIN RSA PRIVATE KEY-----
-----END RSA PRIVATE KEY-----
</key>
```
3. Copy the device certificate, to **vpn/vpn.conf** between the cert tags.
```openvpn
<cert>
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
</cert>
```
4. Copy the CA certificate, to **vpn/vpn.conf** between the ca tags.
```openvpn
<ca>
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
</ca>
```
5. Optional - designate a LAN connection for access from talk2M. On the gateway device, run the command ``` ip a ``` to see a list of interfaces. Find the desired interface that should be the LAN connection. Modify the **LAN_IFACE** environment variable in **compose.yml**. Set LAN_FACE to equal the name of the LAN interface. 
```yml
   environment:
      - LAN_IFACE=eno1
```

6. Run the docker compose. This command may take around a minute to download all docker images and run.
```bash
docker compose up 
``` 

## 

