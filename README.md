# Ubuntu Netplan Network Configuration Guide

:

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

2. Add the following configuration, adjusting values for your network:

network:
  ethernets:
    ens18:
      addresses:
        - 10.10.5.23/24    (change ip addresss)
      gateway4: 10.10.5.1
      nameservers:
        addresses:
          - 8.8.8.8
  version: 2


> **Note:** Replace `enp0s3` with your network interface name, which can be found using `ip a` command.

## Applying Changes

Apply the new configuration using one of the following commands:

```bash
# Standard apply
sudo netplan apply

# Debug mode for troubleshooting
sudo netplan --debug apply
```

## Verification

Verify your network configuration:

```bash
# Check interface configuration
ip addr show enp0s3

# Test connectivity to gateway
ping -c 4 192.168.1.1

# Test internet connectivity
ping -c 4 8.8.8.8

# Check DNS resolution
nslookup google.com
```

## Troubleshooting

If you encounter issues with your Netplan configuration:

1. Validate your YAML file:
   ```bash
   sudo netplan try
   ```
   This will apply the configuration temporarily and revert after a timeout if you don't confirm.

2. Check for syntax errors:
   ```bash
   sudo netplan generate
   ```

3. Common issues:
   - Incorrect indentation in YAML file
   - Interface name mismatch
   - IP address conflicts
   - Missing or incorrect gateway address

4. Check system logs:
   ```bash
   journalctl -u systemd-networkd
   ```

## License

This project is licensed under the MIT License - see the LICENSE file for details.
