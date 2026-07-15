---
title: Artkov Lab Production Notes
description: Notes, configs and solutions from real infrastructure.
date: 2026-07-15
slug: artkov-lab-production-notes
tags: [Digital Garden, Workflow, DevOps, Linux, Obsidian, MOC]
menu:
    main:
        name: Home
        weight: -100
        params:
            icon: home
---

# Welcome

This is my working knowledge base. Here you'll find configurations, checklists, config examples, and solutions to common tasks encountered in daily administration.

No theory. Only what has been deployed, configured, and tested in production.

---

### The Stack

My tech stack is a classic infrastructure engineer's toolkit:

| Area | What's Inside |
| :--- | :--- |
| **Virtualization** | Hyper-V, VMware ESXi, Proxmox (installation, networking, LVM, RAID, device passthrough, backups) |
| **Operating Systems** | Linux (Ubuntu/Debian), Windows Server (AD, GPO, PowerShell) |
| **Networking** | MikroTik (routing, VPN, VLAN), OpenVPN, SSH, firewalls |
| **Monitoring** | Zabbix, Netdata, Wazuh SIEM |
| **Automation** | Python, PowerShell, Bash scripts, Git |

---

### How It's Organized

Everything is built on Obsidian. Notes are interconnected—if you see a link to another topic, click it for the details.

Main types of content:
- **Guides** — step-by-step instructions for installation and configuration.
- **Checklists** — quick action lists for rapid deployment.
- **Cheat sheets** — command and syntax quick references.
- **Troubleshooting** — error descriptions and how to fix them.

---

### Who Is This For

- Sysadmins and DevOps engineers working with a similar stack.
- Anyone working with virtualization platforms.
- Those looking for concise, no-fluff instructions.

---

### How to Use This Site

The easiest way to navigate is via search. Just type a keyword to find what you need.

You can start from any section. The content isn't linear; pick whatever solves your current problem.

If you spot an error or know a better way to do something, let me know. I'd appreciate the feedback.

---

The site is a work in progress. Some materials are pulled directly from my daily notes, while others are polished for publication. If something is missing, it will likely show up later.

Happy deploying.
```
