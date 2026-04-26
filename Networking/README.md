# Networking Troubleshooting Guides

| Article | Description |
|---------|-------------|
| [No Internet Access (Limited Connectivity)](./no-internet-access.md) | Yellow triangle, no connectivity, DNS issues, limited access |
| [Wi-Fi Keeps Disconnecting](./wifi-keeps-disconnecting.md) | Intermittent wireless drops, adapter power management, signal issues |

---

## Common Networking Commands Cheat Sheet

| Command | Purpose |
|---------|---------|
| `ipconfig /all` | Display full IP configuration for all adapters |
| `ipconfig /release` | Release current IP address |
| `ipconfig /renew` | Request new IP address from DHCP server |
| `ipconfig /flushdns` | Clear DNS resolver cache |
| `ping 8.8.8.8` | Test internet connectivity |
| `ping [hostname]` | Test connectivity to a specific host |
| `nslookup google.com` | Test DNS resolution |
| `tracert 8.8.8.8` | Trace route to destination |
| `netsh winsock reset` | Reset Windows network stack |
| `netsh int ip reset` | Reset TCP/IP stack |
| `netsh wlan show profiles` | List saved Wi-Fi networks |
| `netsh wlan show networks mode=bssid` | Show nearby networks with channel information |
