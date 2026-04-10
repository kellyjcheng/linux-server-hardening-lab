# Linux Server Hardening & Network Analysis Lab

## Project Overview
A hands-on security lab focused on deploying, securing, and auditing a Linux-based web server. This project simulates a professional hardening workflow, moving from initial service deployment to network-level traffic analysis.

## Core Technical Skills
* **System Administration:** Ubuntu 24.04 LTS, Repository management (`apt`), Systemd service control.
* **Network Security:** Host-based firewalls (UFW), Port management, Protocol analysis.
* **Defensive Hardening:** Service obfuscation (Banner grabbing mitigation).
* **Auditing Tools:** Wireshark (Packet Analysis), Nmap (Vulnerability scanning), Lsof.

## Phase 1: Environment Setup & Troubleshooting
* **Challenge:** Resolved a common configuration error where `apt` was locked to a non-existent CD-ROM installation media.
* **Action:** Modified `/etc/apt/sources.list` to disable local media and prioritize global Ubuntu repositories.

## Phase 2: Nginx Hardening
* **Service Deployment:** Installed and verified Nginx web server on Port 80.
* **Information Leakage Mitigation:** Disabled `server_tokens` in `nginx.conf` to prevent version enumeration.
* **Firewall Configuration:** Implemented UFW with a "Default Deny" policy, explicitly allowing only `TCP/22` (SSH) and `TCP/80` (HTTP).

## Phase 3: Packet Analysis (Wireshark)
* Captured and analyzed a **TCP Three-Way Handshake** to verify service reachability.
* Performed a "Follow TCP Stream" audit on unencrypted HTTP traffic to visualize "Clear Text" vulnerabilities (GET requests, User-Agents).
