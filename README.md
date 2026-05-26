# Secure Enterprise Home Lab: pfSense Firewall & Ubuntu Workstation

## 🚧 Status: Work in Progress (WIP)
*An active systems and infrastructure learning project focused on building, isolating, and securing a virtualized office network environment.*

---

## 🖥️ Project Overview
This repository documents the implementation of a sandboxed enterprise network infrastructure using Oracle VirtualBox. The goal of this project is to build a secure network perimeter using a virtualized firewall to control, monitor, and route traffic for internal client machines. 

This project demonstrates practical skills in:
* **Network Segmentation** (Separating public WAN traffic from local LAN data).
* **Firewall Engineering** (Stateful packet filtering, NAT routing, and security rules).
* **Linux System Administration** (Kernel troubleshooting, recovery environments, and driver configuration).

---

## 🛠️ Architecture & Technical Stack
* **Hypervisor:** Oracle VirtualBox
* **Firewall/Router:** pfSense (Configured with isolated WAN and internal LAN interfaces)
* **Internal Workstation Client:** Ubuntu Desktop 26.04 LTS (Locked to the internal host-only network)

---

## ⚙️ Implementation & Logs

### 1. Firewall Deployment
* Deployed pfSense with two distinct virtual network adapters.
* Configured the external gateway interface (WAN) and mapped an isolated internal subnet for network clients (LAN).

### 2. Client Provisioning & Linux Troubleshooting 🛠️
* Installed Ubuntu Desktop on the internal network segment.
* **Technical Hurdle:** Encountered a total display freeze at the initial user login screen caused by a conflict between the default Ubuntu Wayland display server and the virtual graphics hardware.
* **Resolution:** 1. Booted the virtual machine directly into Linux **Recovery Mode** to bypass the corrupted GUI environment.
  2. Dropped into a `root` administrative maintenance shell.
  3. Remounted the root filesystem with write permissions (`mount -o remount,rw /`).
  4. Modified the global GDM3 configuration manager (`/etc/gdm3/custom.conf`) to explicitly force disable Wayland backend protocols: `WaylandEnable=false`.
  5. Successfully stabilized the desktop environment to utilize the robust Xorg display driver layer upon system reboots.

---

## 🗓️ Project Roadmap / To-Do
- [x] Deploy and configure pfSense Firewall base interfaces<img width="1905" height="1078" alt="Screenshot 2026-05-19 092149" src="https://github.com/user-attachments/assets/2b851a0a-5481-48c5-afcf-265262d401c3" />

- [x] Install internal Ubuntu Client Workstation <img width="1917" height="1017" alt="uBuntu" src="https://github.com/user-attachments/assets/7bb81086-8ddf-41bd-bf68-0a55bf3d8040" />
- [x] Troubleshoot and resolve Linux display server crash (Wayland fix)<img width="1693" height="918" alt="Screenshot 2026-05-18 134425" src="https://github.com/user-attachments/assets/b9b21577-81bb-4442-a257-0d60df1ac589" />

- [ ] Verify automated IP leasing via pfSense DHCP server
- [ ] Build stateful firewall access control rules to restrict internal outbound traffic
- [ ] Perform network connectivity, traceroute, and packet inspection verification tests
