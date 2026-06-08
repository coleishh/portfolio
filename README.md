# Linux Server Project: Home Network Storage & Automated Microservices

This project is a headless Linux application server that manages local storage, automated file systems, and network services using Docker containers. The setup includes secure remote access via a reverse proxy tunnel and real-time uptime monitoring to ensure high availability.

---

## Technical Specifications & Tool Stack
* Operating System: Ubuntu Server (Headless LTS)
* Containerization & Virtualization: Docker / Docker Compose
* Network Security & Remote Access: Cloudflare Tunnels (No open inbound ports)
* Monitoring & Diagnostics: Uptime Kuma, Jellystat, PostgreSQL Database
* Storage Configuration: Local Ext4 storage arrays with persistent volume mapping

---

## Core Project Features

### 1. Network Security and Remote Access
* Secure Tunneling: Configured a Cloudflare Tunnel to route external subdomains directly to specific internal Docker containers. This setup allows remote access from anywhere without opening ports on the local router, protecting the network from external port scans.
* Central Dashboard: Deployed a Homarr landing page that acts as a single point of access for all internal network services and admin tools.

### 2. Automated File Management and Permissions
* API Automation: Set up an automated pipeline where different services communicate via API keys to request, find, and download files without manual intervention.
* Linux Permissions: Managed directory structures using Linux command-line tools, setting strict user and group permissions (UID/GID matching) to ensure containers can modify files safely without compromising host security.

### 3. Systems Monitoring and Uptime Tracking
* Uptime Monitoring: Installed Uptime Kuma to run constant HTTP and TCP ping tests on all critical container ports, sending real-time alerts if a service goes down.
* Performance Logging: Connected an analytical dashboard backed by a PostgreSQL database to monitor server performance, network usage, and active connections.

### 4. Data Backup and Storage Integrity
* Persistent Storage: Mapped Docker volumes to keep configuration data separate from the actual operating system files. This prevents data loss when updating or replacing containers.
* Critical Data Backups: Implemented a dedicated local storage area to safeguard irreplaceable personal data, such as a large multi-generational family photo library, keeping it separate from standard media directories.

---

## Troubleshooting and Technical Resolution

### The Issue
During peak usage times with multiple remote connections, users reported severe video buffering and lag. The server was slowing down significantly, causing high disk read/write queues and performance drops.

### The Fix
Using the CompTIA A+ troubleshooting methodology, I investigated the issue systematically:
1. Ran the Linux `htop` command in the terminal to check resource utilization and identified a massive spike in CPU usage.
2. Checked the application logs and discovered the server was trying to transcode complex audio formats (like multi-channel EAC3) on the fly because the remote users' web browsers did not support them natively.
3. Identified the bottleneck as a client-side codec compatibility issue rather than a server hardware failure.
4. Resolved the problem by having the remote users switch from standard web browsers to native, standalone desktop or mobile apps. This allowed their devices to decode the audio natively, changing the workload to a lightweight "Direct Stream" and immediately returning server CPU usage to normal baseline levels.
