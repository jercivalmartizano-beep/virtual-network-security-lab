<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1ff0f430-869e-4869-99ed-159c854b6a12" /><img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/96cc119d-681b-4325-8c9a-6a503b3aa9bd" /># virtual-network-security-lab
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

<img width="507" height="415" alt="image" src="https://github.com/user-attachments/assets/8d855439-f337-48b9-bee9-a333ce6dadef" />
<img width="554" height="393" alt="image" src="https://github.com/user-attachments/assets/fc488b90-f856-4bc0-a4d5-ab96b214fd63" />
<img width="552" height="419" alt="image" src="https://github.com/user-attachments/assets/e0ac92db-3c0a-465c-8316-2e28315c2762" />
<img width="585" height="377" alt="image" src="https://github.com/user-attachments/assets/576b76e5-eecd-46bc-b879-630368e3d229" />
<img width="589" height="373" alt="image" src="https://github.com/user-attachments/assets/0ad56830-b7f2-4456-9265-a7ce8ccf15ee" />
<img width="629" height="388" alt="image" src="https://github.com/user-attachments/assets/101fa26a-469c-46f9-9626-099600fa09cf" />
<img width="975" height="548" alt="image" src="https://github.com/user-attachments/assets/a89a6750-28c0-41a3-8c57-69b023aa373e" />
<img width="725" height="408" alt="image" src="https://github.com/user-attachments/assets/9d393cc9-0e95-436f-b7e1-b0edec6dfef5" />
<img width="720" height="585" alt="image" src="https://github.com/user-attachments/assets/8d7acc2d-a8ed-4671-928e-8be23d23196f" />
<img width="550" height="417" alt="image" src="https://github.com/user-attachments/assets/784e86f9-902e-4aab-925b-70c41df60ca1" />
<img width="450" height="472" alt="image" src="https://github.com/user-attachments/assets/29e96440-345f-482f-8419-15a0d38c3dd3" />

<img width="629" height="388" alt="image" src="https://github.com/user-attachments/assets/1a3e79e0-2444-4a03-82d9-49f77845ab0c" />
<img width="523" height="521" alt="image" src="https://github.com/user-attachments/assets/34ef513d-5ca9-43c5-8b33-ebca14eb13da" />
