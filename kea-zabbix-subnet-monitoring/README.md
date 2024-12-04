# Kea Subnet Monitoring with Zabbix

This project provides scripts and configurations to monitor Kea DHCP server subnet statistics using Zabbix. The solution includes:

- Automatic discovery of Kea subnets.
- Monitoring subnet usage percentages.
- A Zabbix template for seamless integration.

---

## Prerequisites

- A working Kea DHCP server with the API enabled.
- Zabbix agent installed and configured on the Kea server.
- Python 3 installed on the Kea server.
- SSL certificate (`CA.pem`) for secure API communication.

---

## Setup Instructions

### 1. Place the Scripts

Save the following scripts to your Kea server:

- **Subnet Discovery Script**: `/sbin/subnet_discovery`
- **Subnet Usage Script**: `/sbin/subnet_usage`

Make the scripts executable:
```bash
chmod +x /sbin/subnet_discovery
chmod +x /sbin/subnet_usage
```

---

### 2. Configure Zabbix Agent

Add the following lines to the Zabbix agent configuration directory (/etc/zabbix/zabbix_agent2.d/kea.conf):

```bash
UserParameter=kea.subnet.discovery,/usr/bin/python3 /sbin/subnet_discovery
UserParameter=kea.subnet.usage[*],/usr/bin/python3 /sbin/subnet_usage $1
```

Restart the Zabbix agent to apply the changes:

```bash
systemctl restart zabbix-agent2
```

### 3. Upload Zabbix Template
- Import the provided Zabbix template into your Zabbix server.
- Link the template to the host where the Kea server is running.

## Contributing
Feel free to submit issues or pull requests to improve the project.
