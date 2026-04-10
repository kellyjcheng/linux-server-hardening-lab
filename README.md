# Linux Server Hardening & Network Analysis Lab

## Project Overview
A hands-on security lab focused on deploying, securing, and auditing a Linux-based web server. This project simulates a professional hardening workflow, moving from initial service deployment to network-level traffic analysis. This lab served as a practical application of "Purple Team" concepts—combining defensive configuration with offensive verification.

## Core Technical Skills
* **System Administration:** Ubuntu 24.04 LTS, Repository management (`apt`), Systemd service control.
* **Network Security:** Host-based firewalls (UFW), Port management, Protocol analysis.
* **Defensive Hardening:** Service obfuscation (Banner grabbing mitigation), Nginx security configuration.
* **Auditing & Analysis:** Wireshark (Packet Analysis), Nmap (Vulnerability scanning), Netcat (Network pivoting).

---

## Phase 1: Environment Deployment & Troubleshooting
**Objective:** Establish a stable Linux environment and resolve critical configuration blockers that would impede security updates.

* **Virtualization:** Deployed **Ubuntu 24.04 LTS** via VirtualBox.
* **The "CD-ROM" Repository Conflict:** Encountered a critical `apt` lock where the system prioritized a non-existent physical CD-ROM media, blocking all software installations and security patches.
    * **Resolution:** Manually edited `/etc/apt/sources.list` to comment out `cdrom:` entries, successfully pivoting the system to official Ubuntu mirrors.
* **Kernel/Display Optimization:** Diagnosed a persistent "Frozen Login Screen" by re-allocating Video Memory and installing Guest Additions for proper driver support.

## Phase 2: Network Reconnaissance & Port Discovery
**Objective:** Identify the attack surface of the local machine using industry-standard tools to understand what an adversary sees.

* **Service Identification:** Utilized **Nmap** to footprint the system and identify active services.
    * *Command Used:* `nmap -sV localhost`
* **Active Connection Auditing:** Leveraged `lsof -i` and `netcat` to verify process-to-port mapping.
* **Terminal Environment:** Documented the relationship between the **tty** (teletype) and active shell sessions to better understand session management and potential local escalation paths.

## Phase 3: Web Server Deployment & Defensive Hardening
**Objective:** Build a functional Nginx web server and apply "Blue Team" defensive configurations to minimize the attack surface.

* **Service Setup:** Installed and initialized **Nginx** via `systemctl`.
* **Firewall Orchestration (UFW):**
    * Implemented a "Deny by Default" posture.
    * Configured specific rules to allow `Nginx Full` (Ports 80/443).
* **Banner Grabbing Mitigation:**
    * Modified `nginx.conf` to set `server_tokens off;`.
    * **Result:** Successfully masked the specific Nginx version, preventing automated scanners from identifying version-specific CVEs.

## Phase 4: Traffic Analysis with Wireshark
**Objective:** Validate security controls by analyzing raw packet data and observing the "wire" during an interaction.

* **Packet Capture:** Monitored the loopback interface during active HTTP requests.
* **Analysis:**
    * Verified the **TCP Three-Way Handshake** (SYN, SYN-ACK, ACK) to ensure connection integrity.
    * Inspected HTTP headers to confirm that the hardening steps in Phase 3 successfully removed sensitive version metadata from the packet payloads.
* **Validation:** Confirmed that the UFW firewall was actively filtering traffic by observing packet drops on unauthorized port connection attempts.

---

## Tools Summary
| Category | Tool |
| :--- | :--- |
| **Virtualization** | VirtualBox |
| **Operating System** | Ubuntu 24.04 LTS |
| **Web Server** | Nginx |
| **Network Auditing** | Nmap, Wireshark, Netcat |
| **Defense** | UFW (Uncomplicated Firewall) |

---

## Key Takeaways
This lab demonstrated that security is a continuous lifecycle rather than a single setup. Troubleshooting the `apt-get` CD-ROM error highlighted a critical lesson: **Security updates are only possible on a well-configured system.** By combining Nginx hardening with Wireshark analysis, I was able to verify that defensive configurations actually changed the data signatures leaving the host.
