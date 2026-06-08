# Single-Node Hybrid Cloud Infrastructure: Automated Microservices & Storage Array

A headless Linux application server orchestrating containerized microservices via Docker. This architecture features automated content lifecycle pipelines, high-availability monitoring, token-based API integrations, and secure edge routing via an encrypted reverse proxy tunnel.

---

## System Architecture & Core Stack
* Host Operating System: Headless Ubuntu Server (LTS)
* Virtualization & Containerization: Docker Engine / Docker Compose
* Edge Networking & Security: Cloudflare Edge Tunnels
* High Availability & Telemetry: Uptime Kuma, PostgreSQL Database, Jellystat Engine
* Storage Matrix: Local Ext4 File System arrays with dedicated persistent volume mapping

---

## Key Infrastructure Achievements

### 1. Secure Edge Networking & Unified Access Layer
* Reverse Proxy Edge Tunnels: Integrated Cloudflare Tunnel routing to securely map subdomains to isolated internal Docker network bridge endpoints. This eliminates the need to expose vulnerable host-level inbound ports (such as port 80 or 443) to the public internet, mitigating edge-level scanning threats.
* Unified Service Aggregation: Deployed a centralized web-based landing portal (Homarr) to map active host endpoints, giving administrators and authenticated remote clients single-point secure access to the ecosystem from any network.

### 2. Asynchronous Ingestion & Lifecycle Automation
* Event-Driven Workflows: Integrated a fully automated, asynchronous ingestion stack utilizing decoupled application components. The ecosystem leverages token-based API authentication hooks to continuously sync requests, search indexers, and handle download queues natively.
* Automated File Operations: Configured atomic moves and precise data directory synchronization rules. The infrastructure handles incoming file parsing, folder permission auditing (matching strict UID/GID access control lists), and library metadata scanning dynamically before deploying content to the hardware-accelerated media host (Jellyfin).

### 3. Proactive Telemetry & High Availability Auditing
* Uptime Monitoring Engine: Deployed an independent uptime tracing engine (Uptime Kuma) executing routine synthetic HTTP/TCP socket pings across critical container ports to ensure continuous platform availability.
* Granular Analytics Pipeline: Integrated a structural logging stack backed by a relational PostgreSQL database to map real-time performance variables, tracking remote client player compatibility, active transcoder bitrates, and hardware resource consumption.

### 4. Data Integrity & Redundancy Strategy
* Decoupled Configuration State: Configured strict persistent storage volumes to completely isolate immutable configuration files and databases from dynamic runtime containers, protecting systems against data loss during rolling image upgrades.
* Cold Storage Ingestion: Implemented dedicated local archival pipelines to secure critical personal data assets, managing multi-generational user media collections independently from general streaming directories.

---

## Operational Optimization & Technical Resolution

### The Bottleneck
During multi-user peak stream windows, a technical bottleneck was identified where remote client web browsers failed to interpret complex audio container profiles (such as multi-channel DTS or EAC3). This forced the server into heavy on-the-fly digital signal translation workloads, causing intermittent playback latency and structural I/O queue wait times.

### The Engineering Resolution
Monitored live process allocation using the headless htop utility and interrogated localized application logs to confirm the root cause as a client-side codec limitation. Resolved the latency issue entirely by migrating remote end-users away from un-optimized web browsers to native, standalone desktop or mobile applications. This allowed for 100% native client-side decoding, successfully shifting the pipeline from resource-heavy audio-transcoding to a lightweight, lossless direct stream, dropping server host resource utilization back to baseline.
