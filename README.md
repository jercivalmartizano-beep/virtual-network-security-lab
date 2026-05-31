# virtual-network-security-lab
An isolated virtual network sandbox environment built using VirtualBox to study Linux systems administration and network diagnostics.

Hands-On Project: Isolated Virtualization Sandbox & Network Security Lab
📝 Project Overview
This project involved architecting, configuring, and troubleshooting a completely isolated, dual-virtual-machine local sandbox network using Oracle VirtualBox. The purpose of the lab is to safely study core Linux systems administration, enterprise networking protocols, and network reconnaissance techniques without internet dependencies.

The infrastructure mimics a real-world enterprise environment consisting of two primary nodes:

Auditor Workstation: Running Kali Linux to execute diagnostic commands and network mapping.

Target Host Server: Running a Linux-based server application layer (Metasploitable 2) hosting various legacy network daemons.

🛠️ Core Technical Competencies Demonstrated
Hypervisor Architecture: VirtualBox platform engineering, host-only network configuration, virtual storage states.

Linux Systems Administration: Command-line proficiency (bash & zsh), low-level terminal diagnostics (tty system consoles), kernel filesystem rescue.

Network Infrastructure: Manual IPv4 static addressing (ifconfig), network masks, packet checking (ping), and manual TCP/IP stream interactions (telnet).

Security Reconnaissance: Passive and active port mapping, structural version detection, and asset footprinting using Nmap.

🚀 Key Milestones & Practical Accomplishments
1. Operating System Diagnostics & Filesystem Rescue
During setup, the guest operating system encountered a locked, critical fault rendering the storage volume read-only (zsh: locking failed for /home/kali/.zsh_history).

The Fix: Rather than scrapping the environment, I utilized low-level text interfaces (tty3) to manually issue a storage remount directive to the Linux kernel:

Bash
sudo mount -o remount,rw /
This successfully restored full read-write execution privileges to the virtualized volume, preserving system uptime and configuration states.

2. Manual Network Interface Configuration
To enable communication between the sandbox systems securely without bridging to the open internet, I hand-configured the local networking adapters.

Assigned a static address string to the primary ethernet card (eth0) on a private subnet:

Bash
sudo ifconfig eth0 192.168.56.10 netmask 255.255.255.0
Verified structural connectivity across the local hypervisor switch fabric using targeted network echo requests, successfully achieving a stable link with 0% packet drop:

Bash
ping -c 4 192.168.56.20
3. Full-Scale Network Port & Service Footprinting
With network paths established, I performed full-spectrum infrastructure discovery mapping to inventory open listening ports on the target infrastructure.

Initial Discovery: Discovered 23 active network ports using an open-ended Nmap probe, revealing running services including FTP, SSH, Telnet, SMTP, DNS, HTTP, and multiple database environments (MySQL/PostgreSQL).

Deep Version Auditing: Filtered down to specific endpoints to extract explicit software names and release builds. By forcing the target application layers to reply to precise network queries, I recorded a live deployment of an outdated file-transfer software daemon:

Bash
nmap -sV -p 21 192.168.56.20
# Output: PORT 21/tcp open ftp vsftpd 2.3.4
🔬 Lessons Learned & Professional Growth
Meticulous Syntax Habits: Gained deep respect for precise command syntax and flags. Encountering terminal issues due to accidental characters (like a Tab or trailing zero) highlighted how critical syntax accuracy is when interacting with remote shells or automated scripts.

Resilience in Systems Engineering: Learned that system failures (like frozen terminals, broken processes, or text-only lockouts) are standard components of infrastructure management. I built the muscle memory to switch to alternative virtual consoles (tty5/tty6), reset stuck network processes, and smoothly recover operational states.

Infrastructure Visibility: Discovered firsthand how much data an unpatched server gives away over open network protocols, emphasizing why version tracking and defensive network filtering are essential in production networks.
