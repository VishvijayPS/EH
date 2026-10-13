# EH Lab Repository

This repository contains a collection of ethical hacking and cybersecurity lab notes focused on practical tools and techniques used in authorized security testing and learning.

The files in this repo are designed to be read in a structured order and used as lab documentation for Kali Linux-based exercises.

## Repository Contents

- `Recon-ng.md` — Passive footprinting and OSINT using Recon-ng
- `nmap.md` — Network scanning, port discovery, and Nmap basics
- `john.md` — ZIP password recovery using John the Ripper
- `wireshark.md` — Packet capture and traffic analysis with Wireshark

## How to Use This Repository

### 1. Start with the project overview

Read the lab file that matches the topic you want to study.

- If you are learning OSINT and passive reconnaissance, start with `Recon-ng.md`.
- If you want to explore network discovery and scanning, read `nmap.md`.
- If you are learning password auditing and recovery, read `john.md`.
- If you want to inspect real network traffic, use `wireshark.md`.

### 2. Follow the setup steps exactly

Each file includes:

- required tools
- installation instructions
- step-by-step procedure
- commands to run
- expected outputs
- troubleshooting tips
- ethical guidelines

Do not skip the installation and requirements section before starting a lab.

### 3. Run the commands in a safe lab environment

These exercises are intended for:

- authorized security labs
- isolated virtual machines
- controlled test networks
- educational or training environments

Never run these tools against systems or networks you do not own or have permission to test.

### 4. Record your results

Each lab file includes a place where you can document:

- commands used
- tool output
- observed results
- screenshots or notes
- final conclusion

For academic or lab purposes, keep your notes clear and specific.

## Recommended Reading Order

For beginners, this is the best order:

1. `wireshark.md` — learn how network traffic looks and how protocol data is analyzed
2. `nmap.md` — learn active host and port scanning basics
3. `Recon-ng.md` — learn passive OSINT and domain footprinting
4. `john.md` — learn password recovery techniques in a controlled lab

This order helps build a logical understanding from network basics to reconnaissance and password auditing.

## Lab Focus Areas

### Recon-ng

Use this file when studying:

- passive intelligence gathering
- OSINT collection
- domain reconnaissance
- handling Recon-ng modules and workspaces

### Nmap

Use this file when studying:

- host discovery
- open port identification
- service/version detection
- OS detection basics
- vulnerability assessment workflow with Nessus

### John the Ripper

Use this file when studying:

- ZIP password recovery
- hash extraction
- wordlist-based attacks
- ethical password auditing

### Wireshark

Use this file when studying:

- packet capture
- protocol inspection
- packet filtering
- network troubleshooting
- TCP, DNS, UDP, ICMP, and HTTP analysis

## Safety and Ethical Use

This repository is for educational and authorized lab use only.

Follow these rules:

- use only systems you own or are authorized to test
- avoid scanning public or third-party targets without permission
- keep evidence and reports private
- do not exploit or damage systems
- never use these tools for unauthorized access

## Documentation Style

Each file is written in a README-style format with:

- a clear heading
- overview
- objectives
- requirements
- installation steps
- commands
- troubleshooting
- conclusion
- ethical notes

This keeps the repo easy to read and easy to use as a study guide.

## Suggested Workflow for a Lab Session

1. Open the relevant `.md` file.
2. Read the overview and objectives.
3. Check the requirements and installation section.
4. Run commands in a safe VM or authorized environment.
5. Compare the real output with the expected results.
6. Take screenshots and write notes.
7. Finish the lab by reviewing the conclusion and ethical considerations.

## Final Note

This repository is designed as a practical learning toolkit for cybersecurity students and ethical hacking beginners. Use it as a structured reference, not as a set of instructions to perform unauthorized activities.

If you want to learn step by step, open each file in order and follow the instructions carefully.
