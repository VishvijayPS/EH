# Ethical Hacking Lab 4: Network Scanning Using Nmap

A practical cybersecurity lab focused on network discovery, host enumeration, port scanning, service detection, and vulnerability assessment using Nmap and Nessus.

This project demonstrates how ethical hackers and security analysts use Nmap to study live hosts, identify open ports, detect services, estimate the operating system, and document scan results in an authorized environment.

## Overview

Network scanning is a critical part of ethical hacking and cybersecurity assessments. It helps security professionals determine which systems are reachable on a network, which services are exposed, and which ports may require further inspection.

In this lab, Nmap is used to:

- discover active hosts
- identify open ports
- detect running services and versions
- estimate the operating system
- save scan results for reporting

Nessus is also introduced to show how vulnerability assessment complements network scanning by identifying potential security weaknesses.

## Objectives

- Install and verify Nmap in Kali Linux.
- Check network configuration and identify the active network range.
- Discover live hosts on an authorized lab network.
- Perform basic and targeted port scans.
- Detect services and software versions.
- Attempt OS detection.
- Save scan output for documentation.
- Understand how Nessus fits into vulnerability assessment.

## Tools and Technologies

- Kali Linux
- Nmap
- Nessus
- Terminal
- Authorized lab environment

## Prerequisites

- Kali Linux installed on a physical or virtual machine
- Nmap installed and working
- Basic knowledge of IP addresses, ports, and network interfaces
- Access to an authorized lab network and target system
- Nessus installed and activated for the vulnerability assessment section

## Installation and Setup

### 1. Check Nmap installation

```bash
nmap --version
```

If Nmap is not installed, run:

```bash
sudo apt update
sudo apt install nmap -y
```

### 2. Check network configuration

```bash
ip addr
```

This command shows active interfaces and assigned IP addresses. For example:

```text
inet 10.0.2.15/24
```

### 3. Identify the connected network

```bash
ip route
```

This helps determine the route and network range used by the machine. Example:

```text
10.0.2.0/24 dev eth0
```

## Discovering Live Hosts

To find reachable hosts in the local lab network:

```bash
nmap -sn <LAB-NETWORK>/24
```

Example:

```bash
nmap -sn 10.0.2.0/24
```

This is a host-discovery scan and does not inspect ports.

## Basic Network Scanning

### 1. Perform a basic port scan

```bash
nmap <TARGET-IP>
```

Example:

```bash
nmap 10.0.2.20
```

### 2. Display only open ports

```bash
nmap --open <TARGET-IP>
```

### 3. Scan a specific port

```bash
nmap -p 80 <TARGET-IP>
```

### 4. Scan multiple ports

```bash
nmap -p 22,80,443 <TARGET-IP>
```

### 5. Scan a range of ports

```bash
nmap -p 1-100 <TARGET-IP>
```

### 6. Perform a fast scan

```bash
nmap -F <TARGET-IP>
```

## Service and Version Detection

### Detect services and versions

```bash
nmap -sV <TARGET-IP>
```

This helps identify the software and version running on open ports.

## Operating System Detection

### Attempt OS detection

```bash
sudo nmap -O <TARGET-IP>
```

OS detection is best-effort and may not always be accurate, especially if the target is protected or uses non-standard responses.

### Combined detection

```bash
sudo nmap -sV -O <TARGET-IP>
```

## Saving Scan Results

```bash
sudo nmap -sV -O <TARGET-IP> -oN nmap_result.txt
```

Display the saved output:

```bash
cat nmap_result.txt
```

Check the current working directory:

```bash
pwd
```

## Vulnerability Assessment with Nessus

Nessus is a vulnerability assessment tool that helps identify weaknesses in systems and services that may have been exposed by scanning.

### General workflow

1. Install a supported Nessus edition from the official Tenable website.
2. Complete setup and activation according to the selected edition.
3. Open the Nessus web interface, usually on `https://localhost:8834`.
4. Create a basic scan.
5. Enter the IP address of an authorized target.
6. Start the scan and review results.
7. Record vulnerabilities, severity ratings, affected services, and recommended remediation steps.

Official site:

https://www.tenable.com/products/nessus

> Note: Nessus is proprietary software and its feature set depends on the edition and license used.

## Nmap Command Reference

| Command | Purpose |
|---|---|
| `nmap --version` | Check installed version |
| `ip addr` | Display IP addresses and interfaces |
| `ip route` | Display routing information |
| `nmap -sn <NETWORK>` | Discover live hosts |
| `nmap <TARGET-IP>` | Perform a basic port scan |
| `nmap --open <TARGET-IP>` | Show only open ports |
| `nmap -p 80 <TARGET-IP>` | Scan a specific port |
| `nmap -p 22,80,443 <TARGET-IP>` | Scan selected ports |
| `nmap -p 1-100 <TARGET-IP>` | Scan a range of ports |
| `nmap -F <TARGET-IP>` | Run a fast scan |
| `nmap -sV <TARGET-IP>` | Detect service and version |
| `sudo nmap -O <TARGET-IP>` | Attempt OS detection |
| `sudo nmap -sV -O <TARGET-IP>` | Combine service and OS detection |
| `sudo nmap -sV -O <TARGET-IP> -oN nmap_result.txt` | Save output to a file |
| `cat nmap_result.txt` | View saved results |

## Port States Explained

| State | Meaning |
|---|---|
| Open | The port is accepting connections |
| Closed | The target is reachable but no service is listening |
| Filtered | A firewall or filter prevents Nmap from determining the port state |

An open port does not automatically prove a vulnerability. It only indicates that a service is reachable and may require deeper assessment.

## Results and Observations

During the experiment, the following tasks were performed:

- network interfaces and IP addresses were checked
- the active network was identified
- live hosts were discovered on an authorized lab network
- open ports were identified
- service and version detection was performed
- operating system detection was attempted
- report data was saved in a text file
- vulnerability assessment workflow using Nessus was reviewed

Actual results should be recorded from the lab environment being used. Any examples in this document are illustrative only and should not be treated as confirmed findings.

## Conclusion

This lab demonstrates how Nmap can be used for host discovery, port scanning, service identification, operating system estimation, and result documentation. Nessus extends this workflow by helping identify likely vulnerabilities in authorized systems.

These techniques give cybersecurity professionals a practical understanding of how networks and services are exposed and how the information can be used to improve system security.

## Ethical and Safety Guidelines

- Scan only systems and networks for which you have explicit authorization.
- Prefer a lab or isolated environment for practical testing.
- Do not treat open ports as proof of compromise.
- Verify vulnerability findings before drawing conclusions.
- Protect scan reports because they may contain sensitive network information.

## References

- Nmap Official Website: https://nmap.org/
- Nmap Reference Guide: https://nmap.org/book/man.html
- Tenable Nessus: https://www.tenable.com/products/nessus
- Kali Linux Documentation: https://www.kali.org/docs/

## Project Summary

- Project: Ethical Hacking Lab 4
- Topic: Network Scanning Using Nmap and Vulnerability Assessment
- Platform: Kali Linux
- Tools: Nmap and Nessus
