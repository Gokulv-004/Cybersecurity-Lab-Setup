# 🔐 Cybersecurity Testing Lab Setup (Week 1)

## 📌 Project Overview
This project documents the setup of an isolated virtual cybersecurity lab on my personal laptop using VirtualBox and Kali Linux. The purpose is to create a safe, controlled environment for practicing penetration testing and network security.

## 🖥️ My Host Machine Specs
- **Laptop Model:** Aspire Lite AL15-52H
- **Operating System:** Windows 11 (64-bit)
- **RAM:** 16.0 GB
- **Processor:** 12th Gen Intel(R) Core(TM) i5-12450H (2.00 GHz)
- **Storage:** 477 GB SSD

## ⚙️ Lab Configuration
| Component | Details |
|-----------|---------|
| Hypervisor | VirtualBox 7.2.2 |
| Attacker OS | Kali Linux 2026.1 |
| Virtual Network | NAT Network (`10.0.0.0/24`) |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

## 🪜 Setup Process
1. Installed 7-Zip and extracted the Kali Linux virtual machine file.
2. Installed VirtualBox and created a dedicated NAT Network (`10.0.0.0/24`).
3. Imported Kali Linux and allocated 2048 MB RAM.
4. Configured the network adapter to attach to the NAT Network.
5. Set a static IP (`10.0.0.2`), Gateway (`10.0.0.1`), and DNS (`8.8.8.8`).
6. Enabled Shared Clipboard (Bidirectional), Drag'n'Drop (Bidirectional), and set up Shared Folders.
7. Verified gateway, internet, and DNS connectivity using terminal commands.
8. Created a clean baseline snapshot named "Clean Kali - Week 1".

## 🐞 Problems I Faced & How I Fixed Them

**Problem 1: NetworkManager Failed to Apply Static IP**
When I tried to apply the manual IP configuration via the GUI, the connection failed with the error: 
`Error: Connection activation failed: IP configuration could not be reserved (no available address, timeout, etc.)`
As a result, my Kali Linux had no IPv4 address on `eth0`.

**Solution:**
I diagnosed the issue by checking the network interfaces with `ip a`. I realized the static IP wasn't applying properly. I fixed this by using the terminal to force the network configuration using `nmcli` commands:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.addresses 10.0.0.2/24
sudo nmcli connection modify "Wired connection 1" ipv4.gateway 10.0.0.1
sudo nmcli connection modify "Wired connection 1" ipv4.dns 8.8.8.8
sudo nmcli connection modify "Wired connection 1" ipv4.method manual
sudo nmcli connection up "Wired connection 1"
```
After running these commands, ip a successfully showed inet 10.0.0.2/24 on eth0, and I was able to ping the gateway and internet perfectly.

🔎 Verification Tests Conducted
IP Check: ip a (Confirmed 10.0.0.2/24)

Gateway Test: ping 10.0.0.1 (Successful replies)

Internet Test: ping 8.8.8.8 (Successful replies)

DNS Test: nslookup networkwalks.com (Successfully resolved)

Browser Test: Loaded www.networkwalks.com in Firefox

💡 What I Learned
How to configure and manage a NAT Network in VirtualBox.

The difference between standard NAT and NAT Network for multi-VM labs.

How to troubleshoot Linux network issues using nmcli in the terminal.

The importance of taking a clean VM snapshot before performing security testing.

How to professionally document a technical project.

🔐 Security & Ethical Use
This laboratory is strictly for educational purposes and authorized security testing only. I will only use these tools on systems I own or have explicit permission to test.

👤 Author
Gokul V
Cybersecurity Intern - Networkwalks (Batch B083)
LinkedIn: https://www.linkedin.com/in/gokul-v-17b0a2357/
