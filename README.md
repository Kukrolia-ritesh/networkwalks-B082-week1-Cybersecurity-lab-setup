# networkwalks-B082-week1-Cybersecurity-lab-setup
Cyber Security Home Lab Setup Week 01 

# 🛡️ Virtual Cybersecurity & Penetration-Testing Laboratory

## 📌 Project Overview

This project focuses on building a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The objective is to create a controlled and isolated environment where cybersecurity tools and techniques—including network reconnaissance, port scanning, vulnerability assessment, packet analysis, and security testing—can be safely practiced and repeated.

The laboratory is configured on a private virtual network, allowing additional virtual machines to be added as targets for **authorized security testing** in future projects.

---

## 🎯 Objectives

The primary objectives of this project are to:

* Install and configure VirtualBox.
* Install and import Kali Linux as a virtual machine.
* Create a dedicated **NAT Network** for the cybersecurity laboratory.
* Configure network connectivity for the Kali Linux VM.
* Assign a consistent IP address to the Kali VM.
* Verify network connectivity and DNS resolution.
* Create a clean VM snapshot for recovery.
* Document the complete laboratory setup process.
* Prepare the environment for future cybersecurity projects and experiments.

---

## 🛡️ Purpose of the Laboratory

The laboratory provides an isolated and controlled environment for cybersecurity education, experimentation, and authorized security testing.

It can be used for activities such as:

* Network reconnaissance
* Port scanning
* Vulnerability assessment
* Packet analysis
* Web security testing
* Exploitation practice
* Security-tool experimentation

> ⚠️ **Important:** This laboratory must only be used against systems that you own or have explicit authorization to test. Security tools and techniques should never be used against unauthorized systems.

Additional attacker and target machines can be connected to the same virtual network as the laboratory is expanded.

---

## ⚙️ Lab Configuration

| Component                    | Configuration      |
| ---------------------------- | ------------------ |
| 🖥️ Host Operating System    | Windows 10         |
| 🧠 Host RAM                  | 16 GB               |
| ⚡ Processor                  | Intel Core i5      |
| 🧰 Hypervisor                | VirtualBox 7.2.14     |
| 🐉 Security Operating System | Kali Linux 2026.2  |
| 🧠 Kali Linux RAM            | 2048 MB            |
| 🌐 Virtual Network           | NAT Network        |
| 📡 Network Address           | 10.0.0.0/24        |
| 🐧 Kali IP Address           | 10.0.0.2/24        |
| 🚪 Default Gateway           | 10.0.0.1           |
| 🌍 DNS Server                | 8.8.8.8            |
| 🔮 Future VM Address Range   | 10.0.0.3–10.0.0.99 |

---

# 🪜 Laboratory Setup Procedure

## Step 1 — Install 7-Zip

7-Zip was installed to extract the Kali Linux virtual-machine package, which may be distributed as a `.7z` archive.

**Tool:** 7-Zip

---

## Step 2 — Install VirtualBox

VirtualBox was installed as the hypervisor for hosting and managing the Kali Linux virtual machine.

---

## Step 3 — Create the NAT Network

A dedicated NAT Network was created in VirtualBox with the following configuration:

```text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

A **NAT Network** was selected because multiple virtual machines connected to the same NAT Network can communicate with one another while also having outbound network connectivity.

This configuration provides a suitable foundation for future attacker and target virtual machines within the cybersecurity laboratory.

---

## Step 4 — Import Kali Linux

Kali Linux was downloaded from the official Kali Linux website and imported into VirtualBox.

The VM's network adapter was configured as follows:

```text
Adapter 1
Attached to: NAT Network
Network:     NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

The Kali Linux VM was allocated:

```text
RAM: 2048 MB
```

A shared folder was also configured to facilitate the transfer of required files between the Windows host operating system and the Kali Linux VM.

---

## Step 5 — Configure the Kali Linux Network

The Kali Linux network configuration was reviewed and configured with a consistent IPv4 address.

The intended configuration was:

```text
IP Address:   10.0.0.2
Subnet Mask:  255.255.255.0
Gateway:      10.0.0.1
DNS:          8.8.8.8
```

Using a consistent IP address makes the laboratory easier to document and allows the Kali machine to be referenced predictably during future exercises.

---

## Step 6 — Create a Clean VM Snapshot

After completing the initial configuration, a VirtualBox snapshot was created to preserve the clean baseline state of the laboratory.

Example snapshot name:

```text
Clean Kali - Network Setup
```

The snapshot provides a known-good recovery point. If a future experiment changes or damages the VM configuration, the Kali machine can be restored to this baseline.

---

# 🔎 Laboratory Verification

The following tests were performed to verify the laboratory configuration:

| Test                          | Command                         | Expected Result                   |
| ----------------------------- | ------------------------------- | --------------------------------- |
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP address displayed |
| 📡 Test gateway               | `ping 10.0.0.1`                 | Successful replies                |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies                |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves successfully      |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed            |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Baseline configuration restored   |

### Example Network Configuration

```text
IP Address:
10.0.0.2/24

Gateway:
10.0.0.1

DNS:
8.8.8.8
```

Successful completion of these tests confirms that the Kali VM has the expected network configuration and connectivity.

---

# 🐞 Problems Encountered & Solutions

Documenting technical issues and their solutions is an important part of the project because it helps with troubleshooting and provides a useful reference for future deployments.

## Problem 1 — Internet Connectivity After Static IP Configuration

After manually configuring the IPv4 settings, Internet connectivity may fail depending on the Kali Linux and NetworkManager configuration.

One workaround used during this laboratory was:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

The network connection was then restarted or the system was rebooted, followed by connectivity testing.

> **Important:** Network interface and connection names can vary between systems. Before executing an `nmcli` command, identify the actual connection name configured on the system.

---

## Problem 2 — VirtualBox VT-x / Hardware Virtualization Error

The Kali Linux VM initially failed to start because hardware virtualization was disabled in the system firmware/BIOS.

The issue was resolved by:

1. Restarting the computer.
2. Entering the BIOS/UEFI configuration.
3. Enabling Intel VT-x / hardware virtualization.
4. Saving the configuration.
5. Restarting the computer.
6. Launching the Kali Linux VM again.

After hardware virtualization was enabled, the VM started successfully.

---

# 💡 What I Learned

This project provided practical experience in building and configuring a virtual environment for cybersecurity learning and experimentation.

The key concepts I learned include:

### 1. NAT vs. NAT Network

A standard NAT configuration and a NAT Network serve different purposes.

A NAT Network allows multiple virtual machines connected to the same virtual network to communicate with one another while also providing network address translation for external connectivity.

This makes NAT Network particularly useful when building a multi-machine cybersecurity laboratory.

### 2. Virtual Machine Networking

I learned how VirtualBox virtual network adapters connect virtual machines to different types of networks and how network settings affect communication between virtual machines and external networks.

### 3. Static IP Configuration

I learned how to configure and verify IPv4 addresses, subnet masks, default gateways, and DNS settings in Kali Linux.

### 4. VM Snapshots

I learned the importance of creating a **clean snapshot before performing potentially disruptive or experimental activities**.

A snapshot provides a known-good recovery point and makes it easier to reset the environment between cybersecurity exercises.

### 5. Documentation

I learned that documenting commands, configurations, screenshots, problems, and solutions is an important part of a professional cybersecurity workflow.

Good documentation makes a laboratory easier to troubleshoot, reproduce, maintain, and expand.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for **education, experimentation, and authorized security testing**.

All scanning, vulnerability assessment, exploitation, and other security-testing activities should be performed only against systems that are owned by the tester or for which explicit permission has been obtained.

The isolated laboratory environment should be used as the primary environment for practicing cybersecurity techniques and testing security tools.

---

# 🔗 Tools & Resources

* **7-Zip:** https://www.7-zip.org/
* **VirtualBox:** https://www.virtualbox.org/wiki/Downloads
* **Kali Linux:** https://www.kali.org/get-kali/#kali-virtual-machines

These resources should be obtained from their official websites to ensure that the software is downloaded from trusted sources.



# 🔗 Annexure



Aurthor: Ritesh Kukrolia

Aurthor LinkedIn Prfile: https://linkedin.com/in/ritesh-kukrolia

Instructor/ Mentor: Waqas Karim

Instructor LinkedIn Profile: https://linkedin.com/in/waqaskarim/

Internship Firm: Network Walks

Internship Duration: 1 Month





