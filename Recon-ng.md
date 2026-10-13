# Ethical Hacking Lab 3: Recon-ng Footprinting

A practical passive reconnaissance lab focused on collecting publicly available information using Recon-ng and OSINT sources in Kali Linux.

This project demonstrates how to perform domain footprinting ethically and responsibly while documenting the findings, tools, and limitations involved in reconnaissance.

## Overview

Footprinting is the process of collecting information about a target organization or domain before a formal security assessment begins. It helps identify:

- Domain names and subdomains
- Publicly exposed hostnames
- DNS and certificate data
- Domain registration information
- Public threat-intelligence context

Recon-ng is an open-source OSINT framework that consolidates reconnaissance tasks into a modular environment. In this lab, the focus is on passive information gathering using authorized public sources, without exploiting systems or bypassing protections.

## Objectives

- Understand the concept of passive footprinting.
- Install and configure Recon-ng in Kali Linux.
- Create and manage workspaces.
- Search, install, and run Recon-ng modules.
- Collect public hostname and domain information.
- Use OSINT sources such as HackerTarget, Certificate Transparency, Netcraft, WHOIS, and threat-intelligence services.
- Analyze and document results responsibly.

## Requirements

### Hardware

- Laptop or desktop computer
- Minimum 4 GB RAM recommended
- Stable internet connection

### Software

- Kali Linux
- Recon-ng framework
- Terminal access
- Public OSINT sources
- WHOIS utility (optional but recommended)

## Target Domains

The lab uses the following domains:

| No. | Organization | Target Domain |
|---|---|---|
| 1 | Kali Linux | kali.org |
| 2 | Debian | debian.org |
| 3 | Linux Foundation | linuxfoundation.org |
| 4 | Mozilla | mozilla.org |
| 5 | Internet Engineering Task Force (IETF) | ietf.org |
| 6 | Wikipedia | wikipedia.org |

## OSINT Sources Used

| OSINT Source | Purpose |
|---|---|
| HackerTarget | Discover publicly reported hostnames associated with a domain |
| Certificate Transparency | Identify hostnames found in public TLS certificate logs |
| Netcraft | Gather public website and hosting information |
| WHOIS | Review available domain registration information |
| Threat Intelligence | Check public reports on suspicious infrastructure |

> Note: Source availability varies by service, module version, and API restrictions. Not every source will work in every environment.

## Installation and Setup

### 1. Open the terminal

```bash
Ctrl + Alt + T
```

### 2. Check internet connectivity

```bash
ping -c 4 google.com
```

Successful replies confirm that internet access and DNS resolution are working.

### 3. Update the package list

```bash
sudo apt update
```

### 4. Install Recon-ng

```bash
sudo apt install recon-ng
```

### 5. Verify the installation

```bash
recon-ng --version
```

If the version flag is unsupported, start Recon-ng directly:

```bash
recon-ng
```

The framework should display a prompt similar to:

```text
[recon-ng][default] >
```

## Recon-ng Workspace Configuration

A workspace keeps reconnaissance results organized for each experiment.

### Basic workflow

```text
help
modules search domains
marketplace search hackertarget
marketplace install recon/domains-hosts/hackertarget
workspaces create Demo1
workspaces list
workspaces load Demo1
```

The prompt should change to:

```text
[recon-ng][Demo1] >
```

## Footprinting Using HackerTarget

### 1. Load the module

```text
modules load recon/domains-hosts/hackertarget
```

### 2. View the module information

```text
info
options list
```

### 3. Set the target domain

```text
options set SOURCE kali.org
```

### 4. Confirm the configuration

```text
options list
```

### 5. Run the module

```text
run
```

### 6. Return to the workspace

```text
back
```

### 7. Display discovered hosts

```text
show hosts
```

This output may include hostnames and related metadata returned by the source. If the module fails or returns nothing, record the actual outcome.

## Repeat for All Target Domains

Run the same process for each domain:

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE kali.org
run
back
show hosts
```

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE debian.org
run
back
show hosts
```

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE linuxfoundation.org
run
back
show hosts
```

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE mozilla.org
run
back
show hosts
```

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE ietf.org
run
back
show hosts
```

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE wikipedia.org
run
back
show hosts
```

## Certificate Transparency

Certificate Transparency logs publicly visible TLS certificate records, which can reveal hostnames and subdomains.

### Search for availability

```text
marketplace search certificate_transparency
```

### Install the module if available

```text
marketplace install recon/domains-hosts/certificate_transparency
```

### Load and execute

```text
modules load recon/domains-hosts/certificate_transparency
info
options list
options set SOURCE kali.org
run
back
show hosts
```

Repeat the process for other domains if supported by the module.

## Netcraft Footprinting

Netcraft provides public website and hosting information.

```text
marketplace search netcraft
marketplace install recon/domains-hosts/netcraft
modules load recon/domains-hosts/netcraft
info
options list
options set SOURCE kali.org
run
back
show hosts
```

If the module is unavailable or incompatible, document the issue and use another supported source.

## WHOIS Information Gathering

WHOIS may reveal domain registration details such as the registrar, creation date, and nameservers, subject to registry policies and privacy protections.

### Install the WHOIS utility

```bash
sudo apt install whois
```

### Query a domain

```bash
whois kali.org
```

Repeat for the other targets:

```bash
whois debian.org
whois linuxfoundation.org
whois mozilla.org
whois ietf.org
whois wikipedia.org
```

## Threat Intelligence

Threat intelligence helps determine whether a domain or associated infrastructure has been reported as suspicious in public security feeds or reports.

### Search modules

```text
marketplace search threat
```

### Review module requirements

```text
info
options list
```

Some providers may require API keys or accounts. Configure them only under authorized and documented conditions.

Document the following for each domain:

- Provider or source used
- Date of lookup
- Indicator or report returned
- Whether the result was verified
- Any errors or service limitations

## Viewing and Verifying Results

Use the following commands to inspect collected data:

```text
show hosts
show domains
show contacts
db schema
```

The available tables and records depend on the modules used and the information collected. Empty output is possible and should be documented accurately.

## Useful Recon-ng Commands

| Command | Purpose |
|---|---|
| `help` | Display available commands |
| `workspaces list` | List workspaces |
| `workspaces create Demo1` | Create a workspace |
| `workspaces load Demo1` | Load a workspace |
| `modules search domains` | Search installed modules |
| `marketplace search hackertarget` | Search the marketplace |
| `marketplace install <module-path>` | Install a module |
| `modules load <module-path>` | Load a module |
| `info` | View module details |
| `options list` | View configuration options |
| `options set SOURCE kali.org` | Set the target domain |
| `run` | Execute the loaded module |
| `back` | Return to the previous prompt |
| `show hosts` | Display discovered hosts |
| `db schema` | Display database schema |
| `exit` | Exit Recon-ng |

## Troubleshooting

### No modules found

Search the marketplace and install the required module:

```text
marketplace search hackertarget
```

### Module not found

Double-check the exact module path returned by the marketplace and ensure the module is available.

### Missing API key

Read the module documentation and configure credentials only if you have authorized access.

### No hosts discovered

- Verify the target value with `options list`
- Confirm the module executed successfully
- Check internet connectivity
- Try another public source
- Record an empty result if no data is returned

### WHOIS command not found

```bash
sudo apt install whois
```

### Threat-intelligence module unavailable

Document the issue and use another supported public source if your lab environment allows it.

## Screenshots to Include

Capture the following for the lab record:

1. Kali Linux terminal and internet connectivity
2. Recon-ng installation and startup
3. Marketplace module search
4. Workspace creation and loading
5. HackerTarget module information and options
6. Module execution and discovered host records
7. Certificate Transparency module and results, if available
8. Netcraft module and results, if available
9. WHOIS command output
10. Threat-intelligence source or module results
11. Final `show hosts` output

## Results

Passive footprinting was performed using Recon-ng and public OSINT sources for the six assigned domains. The actual hostnames, domain-registration data, and intelligence findings were recorded only when returned by the source. All results were documented accurately and without fabrication.

## Conclusion

This lab introduced the use of Recon-ng for passive footprinting and OSINT collection. It provided hands-on experience with installing modules, managing workspaces, configuring target domains, and analyzing public information sources. The exercise also highlighted the importance of source verification, accurate documentation, and responsible use of reconnaissance tools.

## Ethical Considerations

- Use only public information obtained with proper authorization or educational intent.
- Perform reconnaissance only for legitimate security learning and approved assessments.
- Do not attempt unauthorized access or exploitation.
- Respect the terms of service and rate limits of external sources.
- Treat unverified intelligence as non-confirmed information until validated.

## Project Status

This repository is intended for educational and experimental use in a legal, ethical, and authorized cybersecurity context.
