# Orange Pi Zero-Config Ethernet Discovery
# Both devices automatically get 169.254.x.x addresses when connected

# 1. Create this file at: /etc/netplan/02-luna-ethernet.yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enP4p65s0:
      dhcp4: false
      addresses: [169.254.100.10/16]

# 2. Apply the configuration:
# sudo netplan apply

# How it works:
# - Orange Pi: Always gets 169.254.100.10
# - Windows laptop: Automatically gets 169.254.x.x (APIPA)
# - Both can talk to each other automatically
# - Detection app scans 169.254.0.0/16 range
# - Zero configuration required from user