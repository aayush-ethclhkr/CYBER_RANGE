# 🧠 Step 1: Set Up Wazuh Manager

## What You Are Building

You are setting up a central security server that will:

- Collect logs from all machines
- Analyze them in real time
- Generate alerts
- Show everything on a dashboard

 After this step, you’ll have:

-  A web dashboard (your SOC screen)
-  A backend engine (log processing)

---

##  1. System Requirements (Your VM)

Before installation, make sure your VM has:

- OS: Ubuntu 22.04 LTS (recommended)
- RAM: 4–8 GB minimum
- CPU: 2–4 cores
- Disk: 40+ GB

 This VM will later come from Terraform, but for now you can install manually for testing.

---

##  2. Install Wazuh (Single Node – Easiest Way)

Wazuh provides an all-in-one installer (recommended approach).

### Run These Commands

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

---

##  What This Installs

Automatically sets up:

- Wazuh Manager (log analysis engine)
- Wazuh Indexer (Elasticsearch backend)
- Wazuh Dashboard (web UI)

 No need to install separately — this is why we use `-a`

---

##  3. Wait for Installation

This takes approximately:

- 10–20 minutes (depending on VM performance)

During this process:

- Services are configured
- Ports are opened
- Credentials are generated

---

##  4. Get Login Credentials

At the end, you’ll see something like:

User: admin  
Password: <generated-password>

 Save this carefully.

---

##  5. Access the Dashboard

Open your browser:

https://<your-server-ip>

Example:

https://192.168.1.10

---

## First Login Notes
- You may see SSL warning → click Advanced → Proceed
- Login using:
  - username: admin
  - password: (from installer)

---

##  6. What You Should See

After login, you’ll land on:

- Dashboard homepage
- Security events panel
- Agent status section

 Right now it will feel empty — that’s normal.

No agents = no data yet.

---

##  7. Verify Services (Important Check)

Run:

```bash
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-indexer
sudo systemctl status wazuh-dashboard
```

All should show:

active (running)

---

##  8. Open Required Ports (If Needed)

If firewall is enabled:

```bash
sudo ufw allow 1514/tcp
sudo ufw allow 1515/tcp
sudo ufw allow 5601/tcp
sudo ufw allow 443/tcp
```

---

##  What You’ve Achieved (Pause and Understand)

Right now, you have built:

- A central log brain
- A real SOC dashboard
- A foundation for detection

But it is still blind.

---

##  How This Connects to Your Full Project

###  Infrastructure Layer

This Wazuh VM will later be:

- Auto-created via Terraform
- Configured via Ansible

---

### Red Engine

When MITRE CALDERA attacks:

- Your Wazuh will receive logs
- Detect techniques

---

###  White Cell

Your alerts → used for:

- Scoring
- Detection metrics

---

##  Next Step

 Install and connect Wazuh Agents to start receiving real data.
