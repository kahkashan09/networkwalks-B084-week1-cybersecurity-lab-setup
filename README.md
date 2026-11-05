# networkwalks-B084-week1-cybersecurity-lab-setup
*Building an isolated virtual lab for penetration testing and ethical hacking practice**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/kahkashan%20zafar%20-C00000?style=flat-square" />
</p>

## 📌 Project Overview
This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

# 🎯 Objectives

The main objectives of this project are to:

- Install and configure VirtualBox.
- Install/import Kali Linux as a virtual machine.
- Create a private **NAT Network** for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:

- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## 🏗️ Lab Architecture:




Additional target machines can be added to the same virtual network in future projects.

---
⚙️ Lab Configuration

| 🧩 Component       | ⚙️ Configuration   |
| ------------------ | ------------------  |
| 🖥️ Host OS         | Windows 10         |
| 🧠 Host RAM        | 8 GB               |
| ⚡ Processor       | Intel Core i7      |
| 🧰 Hypervisor      | VirtualBox 7.2  |
| 🐉 Security OS     | Kali Linux 2026.2  |
| 🧠 Kali RAM        | 2048 MB            |
| 🌐 Virtual Network | NAT Network        |
| 📡 Network Address | 10.0.0.0/24        |
| 🐧 Kali IP Address | 10.0.0.2/24        |
| 🚪 Default Gateway | 10.0.0.1           |
| 🌍 DNS Server      | 8.8.8.8            |
| 🔮 Future VM Range | 10.0.0.3–10.0.0.99 |


# 🪜 Cybersecurity Lab Setup Procedure (VMware Kali Image in VirtualBox)

This version of the lab uses the **VMware** build of Kali Linux (`kali-linux-2025.4-vmware-amd64`) and runs it in **VirtualBox** by attaching its virtual disk to a new VM.

---

## Step 1. Install 7-Zip and Extract Kali

The Kali package was downloaded as a `.7z` archive, so 7-Zip was installed to extract it.

1. Install 7-Zip.
2. Right-click `kali-linux-2025.4-vmware-amd64.7z` and choose **Extract Here**.
3. Confirm the extracted folder contains a `.vmx` file and several `.vmdk` files:

```text
kali-linux-2025.4-vmware-amd64.vmx
kali-linux-2025.4-vmware-amd64.vmdk        <- main disk file (use this one)
kali-linux-2025.4-vmware-amd64-s001.vmdk   <- disk slice (do NOT use directly)
kali-linux-2025.4-vmware-amd64-s002.vmdk   <- disk slice (do NOT use directly)
```

> Keep all the files together in the same folder. Do not move or rename individual slices.

**Tool:** 7-Zip

---

## Step 2. Install VirtualBox

VirtualBox was installed as the hypervisor.

---

## Step 3. Create the NAT Network

A dedicated NAT Network was created in VirtualBox under **File → Tools → Network Manager → NAT Networks**.

```text
Network Name: NatNetwork
IPv4 Prefix:  10.0.0.0/24
DHCP:         Enabled
IPv6:         Disabled
```

![NAT Network settings](2-screenshot-network-settings-1.png)

A **NAT Network** was chosen because multiple VMs on the same NAT Network can communicate with each other while still having outbound Internet access. This allows future attacker and target VMs to talk to each other inside the lab.

---

## Step 4. Create the Kali VM from the VMware Disk

VirtualBox cannot open a VMware machine directly, so a new VM was created and the existing Kali disk was attached to it.

1. In VirtualBox click **Machine → New** (Ctrl+N).
2. Set **Name:** `Kali`, **Type:** `Linux`, **Version:** `Debian (64-bit)`.
3. Leave the ISO image empty and tick **Skip Unattended Installation**.
4. Under **Specify virtual hardware**, set **Base Memory** and **Processors**:

```text
RAM:  2048 MB minimum (4096 MB recommended)
CPUs: 2
```

5. Under **Specify virtual hard disk**, choose **Use an Existing Virtual Hard Disk File**, click the folder icon, click **Add**, and select the main disk file:

```text
kali-linux-2025.4-vmware-amd64.vmdk
```

6. Click **Finish**.
7. Select the VM, open **Settings → Network**, and configure Adapter 1:

```text
Adapter 1
Attached to:  NAT Network
Network:      NatNetwork
Adapter Type: Intel PRO/1000 MT Desktop
```

![Kali Linux VM](3-screenshot-kali-linux.png)

A shared folder can also be configured under **Settings → Shared Folders** for transferring files between the host and the Kali VM.

---

## Step 5. Start Kali and Configure the Network

1. Select the Kali VM in the **Machines** list and click **Start**.
2. Log in with the default credentials for the VMware image:

```text
Username: kali
Password: kali
```

3. Configure a consistent IPv4 address (example values):

```text
IP Address:  10.0.0.10
Subnet Mask: 255.255.255.0
Gateway:     10.0.0.1
DNS:         8.8.8.8
```

A consistent IP address makes it easier to document the lab and reference the Kali machine in later exercises.

![Kali network settings](4-screenshot-kali-network-settings.png)

---

## Step 6. Create a Clean VM Snapshot

After the initial configuration was complete, a VirtualBox snapshot was created.

```text
Snapshot name: Clean Kali - Network Setup
```

This is the clean baseline of the lab. If a future exercise breaks the VM, it can be restored to this point.

---

# 🔎 Lab Verification

| ✅ Test                        | 🧾 Command                      | 🎯 Expected Result              |
| ----------------------------- | ------------------------------- | ------------------------------- |
| 🌐 Check IP address           | `ip a`                          | Correct Kali IP displayed       |
| 📡 Test gateway               | `ping 10.0.0.1`                 | Successful replies              |
| 🌍 Test Internet connectivity | `ping 8.8.8.8`                  | Successful replies              |
| 🔎 Test DNS resolution        | `nslookup networkwalks.com`     | Domain resolves                 |
| 🧰 Verify Nmap                | `nmap --version`                | Nmap version displayed          |
| 🔄 Verify snapshot            | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

```text
IP Address: 10.0.0.10/24
Gateway:    10.0.0.1
DNS:        8.8.8.8
```

---

# 🐞 Problems Encountered & Solutions

## Problem 1. "Can't open machine" Errors in VirtualBox

**Cause:** The Kali download was the VMware version (`.vmx` / `.vmdk`). Using **Machine → Open** in VirtualBox only works with VirtualBox `.vbox` files, so it failed with repeated "Can't open machine..." notifications.

**Solution:** Create a new VM with **Machine → New** and attach the existing `.vmdk` disk instead (see Step 4). Alternatively, open the `.vmx` file in VMware Workstation.

---

## Problem 2. `VERR_NOT_SUPPORTED` When Adding the Disk

**Cause:** The wrong `.vmdk` file was selected (`kali-linux-2025.4-vmware-amd64-s001.vmdk`). Files ending in `-s001`, `-s002`, and so on are only slices of the disk and cannot be opened on their own.

**Solution:** Select the main descriptor file **without** the `-sXXX` suffix:

```text
kali-linux-2025.4-vmware-amd64.vmdk
```

Keep all slice files in the same folder.

---

## Problem 3. VirtualBox VT-x / Virtualization Error

The VM failed to start because hardware virtualization was disabled in the BIOS/UEFI.

**Solution:**

1. Restart the computer.
2. Enter the BIOS/UEFI settings.
3. Enable Intel VT-x / AMD-V (hardware virtualization).
4. Save and restart.
5. Start the Kali VM again.

If virtualization is enabled but the VM still fails, Hyper-V may be taking over. Run this in an Administrator Command Prompt and restart:

```text
bcdedit /set hypervisorlaunchtype off
```

---

## Problem 4. VM Boots to a Black Screen

**Solution:** Try these in order:

1. **Settings → System → Motherboard:** toggle **Enable EFI** on or off.
2. **Settings → Display → Screen:** set **Graphics Controller** to `VMSVGA` and **Video Memory** to `128 MB`.

---

## Problem 5. Internet Connectivity After Static IP Configuration

After manually setting the IPv4 configuration, Internet access may fail depending on the NetworkManager setup. One workaround:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
```

Then restart the connection or reboot and test again.

> **Important:** Connection names may differ between systems. Run `nmcli connection show` first to find the actual name.

---

# 💡 What I Learned

### 1. VMware vs VirtualBox Images
A VMware virtual machine cannot be opened directly in VirtualBox. The disk (`.vmdk`) can be reused by creating a new VM and attaching the existing disk.

### 2. Split Virtual Disks
Large `.vmdk` disks are split into slices (`-s001`, `-s002`, ...). Only the main descriptor `.vmdk` file should be attached, with all slices kept beside it.

### 3. NAT vs NAT Network
A NAT Network lets multiple VMs communicate with each other while sharing outbound Internet access, which makes it ideal for a multi-machine lab.

### 4. Virtual Machine Networking
VirtualBox adapters connect VMs to different network types, and the choice affects how machines communicate.

### 5. Static IP Configuration
I learned to configure and verify IP addresses, subnet masks, gateways, and DNS in Kali Linux.

### 6. VM Snapshots
A clean snapshot should be created **before** risky or experimental activity, giving a known-good recovery point.

### 7. Documentation
Recording commands, configuration, screenshots, errors, and fixes is a core part of a professional cybersecurity project.

---

# 🔐 Security & Ethical Use

This laboratory is intended strictly for educational purposes. Only test systems that you own or have explicit written permission to test.

---

# 🔗 Tools & Resources

- **7-Zip:** [https://7-zip.org/download.html](https://7-zip.org/download.html)
- **VirtualBox:** [https://virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
- **Kali Linux:** [https://kali.org/get-kali](https://kali.org/get-kali)

---

# 👤 Author

**Kahkashan**
Cybersecurity Student

LinkedIn: https://www.linkedin.com/in/kahkashan-zafar

---

## 📌 Project Information

**Program Name:** Cybersecurity at Networkwalks | **Week:** 01 | 
**Project:** Cybersecurity & Pentesting Lab Setup | **Repository:** GitHub
