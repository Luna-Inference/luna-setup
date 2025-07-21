# Orange Pi Zero-Config Ethernet Discovery

This guide explains how to set up a zero-configuration Ethernet connection between an Orange Pi and a Windows laptop using link-local addressing.

## Prerequisites
- Both devices will automatically get 169.254.x.x (APIPA) addresses when connected
- No DHCP server required

## Configuration Steps

### 1. Create Network Configuration File
Create the following file at `/etc/netplan/02-luna-ethernet.yaml`:

```yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enP4p65s0:
      dhcp4: false
      addresses: [169.254.100.10/16]
```

### 2. Remove Conflicting NetworkManager Connections
Run these commands to clean up any existing connections:

```bash
# List existing connections
nmcli connection show

# Remove any conflicting connections (replace with actual connection name if different)
sudo nmcli connection delete "Wired connection 1"
```

### 3. Apply the Configuration
Apply the new network configuration with:

```bash
sudo netplan apply
```

## How It Works

- **Orange Pi**: Always gets the static IP `169.254.100.10`
- **Windows Laptop**: Automatically gets a link-local address in the `169.254.x.x` range (APIPA)
- **Communication**: Both devices can communicate directly with each other
- **Discovery**: The detection application scans the `169.254.0.0/16` range to find the Orange Pi
- **Zero Configuration**: No manual IP configuration is required on the Windows side