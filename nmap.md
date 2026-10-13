# Ethical Hacking Lab 4: Network Scanning Using Nmap and Vulnerability Assessment

## Aim

To utilize Nmap to discover live hosts, identify open ports, detect services and operating systems, and understand vulnerability assessment using Nessus.

## Overview

Network scanning is an important activity in ethical hacking and cybersecurity. It helps security professionals understand which devices are reachable on a network, which ports are exposed, and which services are running.

In this experiment, Nmap is used to perform network discovery, port scanning, service detection, operating system detection, and scan result reporting. Nessus is introduced for identifying potential security vulnerabilities in authorized systems.

## Tools and Technologies

- **Kali Linux:** Operating system used for cybersecurity testing.
- **Nmap:** Network discovery and port-scanning tool.
- **Nessus:** Vulnerability assessment software developed by Tenable.
- **Terminal:** Used to execute commands and analyze scan results.

## Prerequisites

- Kali Linux installed on a physical machine or virtual machine.
- Nmap installed and working.
- Basic knowledge of IP addresses, network interfaces, and ports.
- An authorized lab network and target machine.
- Nessus installed and activated for the vulnerability assessment section.

## Experiment Steps

### Step 1: Check Nmap Installation

```bash
nmap --version
```

**Purpose:** Displays the installed Nmap version and confirms that the command is available.

If Nmap is not installed, use:

```bash
sudo apt update
sudo apt install nmap -y
```

### Step 2: Check Network Configuration

```bash
ip addr
```

**Purpose:** Displays network interfaces and their assigned IP addresses.

Example:

```text
inet 10.0.2.15/24
```

Here, `10.0.2.15` is an example IP address, and `/24` is the network prefix.

### Step 3: Identify the Connected Network

```bash
ip route
```

**Purpose:** Displays routing information and helps identify the network connected to Kali Linux.

Example:

```text
10.0.2.0/24 dev eth0
```

Use the network range reported by your own machine rather than assuming that the example network applies to your setup.

### Step 4: Discover Live Hosts

```bash
nmap -sn <LAB-NETWORK>/24
```

**Purpose:** Discovers reachable hosts without performing a port scan.

Replace `<LAB-NETWORK>` with the appropriate network address for your authorized lab.

Example:

```bash
nmap -sn 10.0.2.0/24
```

### Step 5: Perform a Basic Port Scan

```bash
nmap <TARGET-IP>
```

**Purpose:** Scans commonly used TCP ports on the specified target.

Example:

```bash
nmap 10.0.2.20
```

Replace the example IP with the address of your authorized target.

### Step 6: Display Open Ports

```bash
nmap --open <TARGET-IP>
```

**Purpose:** Displays only ports identified as open.

### Step 7: Scan a Specific Port

```bash
nmap -p 80 <TARGET-IP>
```

**Purpose:** Scans TCP port 80, commonly associated with HTTP.

### Step 8: Scan Multiple Ports

```bash
nmap -p 22,80,443 <TARGET-IP>
```

**Purpose:** Scans selected TCP ports commonly associated with SSH, HTTP, and HTTPS.

### Step 9: Scan a Port Range

```bash
nmap -p 1-100 <TARGET-IP>
```

**Purpose:** Scans TCP ports from 1 through 100.

### Step 10: Perform a Fast Scan

```bash
nmap -F <TARGET-IP>
```

**Purpose:** Scans a smaller list of commonly used ports to obtain a quick overview.

### Step 11: Detect Services and Versions

```bash
nmap -sV <TARGET-IP>
```

**Purpose:** Attempts to identify the services and software versions running on open ports.

### Step 12: Detect the Operating System

```bash
sudo nmap -O <TARGET-IP>
```

**Purpose:** Attempts to estimate the target operating system using network responses. OS detection may require suitable privileges and may not always be accurate.

### Step 13: Perform Combined Detection

```bash
sudo nmap -sV -O <TARGET-IP>
```

**Purpose:** Performs service/version detection and operating system detection together.

### Step 14: Save Nmap Results

```bash
sudo nmap -sV -O <TARGET-IP> -oN nmap_result.txt
```

**Purpose:** Saves the scan output in a normal text file named `nmap_result.txt`.

View the saved results:

```bash
cat nmap_result.txt
```

Check the current directory:

```bash
pwd
```

### Step 15: Vulnerability Assessment Using Nessus

Nessus is a vulnerability assessment tool that helps identify potential security weaknesses in systems and services.

General procedure:

1. Install a supported Nessus edition from the official Tenable website.
2. Complete setup and activation according to the selected edition.
3. Open the Nessus web interface, commonly available at `https://localhost:8834` for a local installation.
4. Create a basic network scan.
5. Enter the IP address of an authorized lab target.
6. Start the scan and wait for the results.
7. Review the identified vulnerabilities, severity ratings, affected services, and recommended remediation.
8. Record the findings for the lab report.

Official website: https://www.tenable.com/products/nessus

**Note:** Nessus is proprietary software, not open-source software. Its available features depend on the edition and license.

## Nmap Command Reference

| Command | Purpose |
|---|---|
| `nmap --version` | Check Nmap version |
| `ip addr` | Display IP addresses and interfaces |
| `ip route` | Display network routes |
| `nmap -sn <NETWORK>` | Discover live hosts |
| `nmap <TARGET-IP>` | Perform a basic port scan |
| `nmap --open <TARGET-IP>` | Display open ports only |
| `nmap -p 80 <TARGET-IP>` | Scan port 80 |
| `nmap -p 22,80,443 <TARGET-IP>` | Scan selected ports |
| `nmap -p 1-100 <TARGET-IP>` | Scan ports 1–100 |
| `nmap -F <TARGET-IP>` | Perform a fast scan |
| `nmap -sV <TARGET-IP>` | Detect services and versions |
| `sudo nmap -O <TARGET-IP>` | Attempt OS detection |
| `sudo nmap -sV -O <TARGET-IP>` | Combine service and OS detection |
| `sudo nmap -sV -O <TARGET-IP> -oN nmap_result.txt` | Save scan results |
| `cat nmap_result.txt` | Display saved results |

## Understanding Port States

| State | Meaning |
|---|---|
| Open | A service is accepting connections on the port. |
| Closed | The target is reachable, but no service is listening on the port. |
| Filtered | Filtering prevents Nmap from determining whether the port is open or closed. |

An open port does not automatically indicate a vulnerability. Further assessment is required to determine whether the service is misconfigured, outdated, or exposed to a known security issue.

## Result and Observations

During the experiment:

- Network interfaces and IP addresses were examined.
- The connected network was identified using routing information.
- Host discovery was performed on an authorized lab network.
- TCP ports were scanned to identify their states.
- Service and version detection was performed.
- Operating system detection was attempted.
- Nmap results were saved to a text file.
- The Nessus vulnerability assessment workflow was studied or performed, depending on the lab setup.

**Actual results:** Record the IP addresses, open ports, service versions, and Nessus findings observed in your own experiment. Example outputs in this README are illustrative and are not guaranteed scan results.

## Conclusion

The experiment demonstrates how Nmap can be used for network discovery, port scanning, service identification, operating system estimation, and scan result documentation. Nessus provides an additional approach to vulnerability assessment by identifying potential security weaknesses and suggesting remediation measures.

These techniques help cybersecurity professionals understand network exposure and improve the security of authorized systems.

## Ethical and Safety Guidelines

- Scan only systems and networks for which you have permission.
- Use a dedicated lab environment for practical testing.
- Do not treat open ports as proof of vulnerabilities.
- Verify vulnerability findings before drawing conclusions.
- Keep scan reports secure because they may contain sensitive network information.

## References

- Nmap Official Website: https://nmap.org/
- Nmap Reference Guide: https://nmap.org/book/man.html
- Tenable Nessus: https://www.tenable.com/products/nessus
- Kali Linux Documentation: https://www.kali.org/docs/

---

**Experiment:** Ethical Hacking Lab 4  
**Topic:** Network Scanning Using Nmap and Vulnerability Assessment  
**Platform:** Kali Linux  
**Tools:** Nmap and Nessus
