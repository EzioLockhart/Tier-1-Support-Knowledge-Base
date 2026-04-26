# VPN & Remote Access Troubleshooting Guides

| Article | Description |
|---------|-------------|
| [VPN Connection Fails with Authentication Error](./vpn-authentication-error.md) | Login failed, invalid credentials, MFA issues, server address, protocol |
| [VPN Connected but No Network Access](./vpn-no-network-access.md) | Connected but no resources, DNS, split tunneling, proxy, MTU, routing |

---

## VPN Commands and Shortcuts Quick Reference

| Action | How To Access |
|--------|---------------|
| Check IP configuration | Command Prompt: ipconfig /all |
| Flush DNS | Command Prompt (Admin): ipconfig /flushdns |
| Register DNS | Command Prompt (Admin): ipconfig /registerdns |
| Show routing table | Command Prompt: route print |
| Test MTU | Command Prompt: ping [IP] -f -l [size] |
| Set MTU | Command Prompt (Admin): netsh interface ipv4 set subinterface "Name" mtu=1400 store=persistent |
| Reset network stack | Command Prompt (Admin): netsh int ip reset and netsh winsock reset |
| Open VPN settings | Settings > Network & Internet > VPN |
| Open Network Connections | Win + R > ncpa.cpl |
| Open Credential Manager | Start menu > type "Credential Manager" |
