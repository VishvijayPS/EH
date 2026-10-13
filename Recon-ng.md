# ETHICAL HACKING LAB 3
# Footprinting Using Recon-ng

## 1. Aim

To perform passive footprinting using Recon-ng and collect publicly available information about target domains using OSINT (Open-Source Intelligence) sources.

## 2. Objectives

- Understand the concept of passive footprinting.
- Install and configure Recon-ng in Kali Linux.
- Create and manage workspaces.
- Search, install, and execute Recon-ng modules.
- Collect publicly available hostname and domain information.
- Explore HackerTarget, Certificate Transparency, Netcraft, WHOIS, and threat-intelligence sources.
- Analyze and document the collected results.

## 3. Requirements

### Hardware Requirements
- Computer or laptop
- Minimum 4 GB RAM recommended
- Internet connection

### Software Requirements
- Kali Linux
- Recon-ng framework
- Terminal
- Public OSINT sources
- WHOIS utility (optional)

## 4. Introduction

Footprinting is the process of collecting information about a target organization or domain before conducting a security assessment.

OSINT stands for Open-Source Intelligence. It involves gathering information from publicly accessible sources such as DNS records, certificate logs, domain registration information, and public threat-intelligence databases.

Recon-ng is an open-source reconnaissance framework that provides a modular command-line environment for collecting and organizing OSINT information.

This experiment focuses on passive reconnaissance. It does not involve exploiting vulnerabilities, bypassing authentication, or attempting unauthorized access.

## 5. Target Organizations

The following domains are used for this experiment:

| No. | Organization | Target Domain |
|---|---|---|
| 1 | Kali Linux | kali.org |
| 2 | Debian | debian.org |
| 3 | Linux Foundation | linuxfoundation.org |
| 4 | Mozilla | mozilla.org |
| 5 | Internet Engineering Task Force (IETF) | ietf.org |
| 6 | Wikipedia | wikipedia.org |

## 6. OSINT Sources

| OSINT Source | Purpose |
|---|---|
| HackerTarget | Discover publicly reported hostnames associated with a domain |
| Certificate Transparency | Identify hostnames appearing in publicly logged TLS certificates |
| Netcraft | Obtain publicly available website and hostname information where supported |
| WHOIS | Examine available domain-registration information |
| Threat Intelligence | Check public reports and indicators associated with suspicious infrastructure |

**Note:** The availability of each source depends on the current service, module version, and API requirements. Not every source is accessible through a working Recon-ng module in every installation.

## 7. Installation and Setup

### Step 1: Open Kali Linux Terminal

Press `Ctrl + Alt + T` to open the terminal.

### Step 2: Check Internet Connectivity

```bash
ping -c 4 google.com
```

Successful replies indicate that internet connectivity and DNS resolution are working.

### Step 3: Update Package Information

```bash
sudo apt update
```

### Step 4: Install Recon-ng

```bash
sudo apt install recon-ng
```

### Step 5: Verify Installation

```bash
recon-ng --version
```

If the version option is unsupported, launch Recon-ng directly:

```bash
recon-ng
```

The framework should display a prompt similar to:

```text
[recon-ng][default] >
```

## 8. Recon-ng Workspace Configuration

A workspace stores reconnaissance results separately for a particular experiment.

### Step 1: Display Available Commands

```text
help
```

### Step 2: Search for Modules

```text
modules search domains
```

### Step 3: Search the Marketplace

```text
marketplace search hackertarget
```

### Step 4: Install the HackerTarget Module

```text
marketplace install recon/domains-hosts/hackertarget
```

Use the exact module path shown by the marketplace if the path differs.

### Step 5: Create a Workspace

```text
workspaces create Demo1
```

### Step 6: List Available Workspaces

```text
workspaces list
```

### Step 7: Load the Workspace

```text
workspaces load Demo1
```

The prompt should now resemble:

```text
[recon-ng][Demo1] >
```

## 9. Footprinting Using HackerTarget

### Step 1: Load the Module

```text
modules load recon/domains-hosts/hackertarget
```

### Step 2: Read Module Information

```text
info
```

### Step 3: View Configuration Options

```text
options list
```

### Step 4: Set the Target Domain

```text
options set SOURCE kali.org
```

### Step 5: Verify the Target

```text
options list
```

Confirm that `SOURCE` is set to `kali.org`.

### Step 6: Execute the Module

```text
run
```

### Step 7: Return to the Workspace

```text
back
```

### Step 8: Display Discovered Hosts

```text
show hosts
```

The output may contain hostnames and associated information returned by the source. If the module returns no results or reports an error, record the actual outcome.

## 10. Repeat for All Target Domains

Run the following sequence for each domain.

### Kali Linux

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE kali.org
run
back
show hosts
```

### Debian

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE debian.org
run
back
show hosts
```

### Linux Foundation

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE linuxfoundation.org
run
back
show hosts
```

### Mozilla

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE mozilla.org
run
back
show hosts
```

### IETF

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE ietf.org
run
back
show hosts
```

### Wikipedia

```text
modules load recon/domains-hosts/hackertarget
options set SOURCE wikipedia.org
run
back
show hosts
```

Repeat the procedure for the remaining OSINT sources when suitable modules are available.

## 11. Certificate Transparency

Certificate Transparency provides publicly accessible logs of issued TLS certificates. Certificate records can contain domain names and subdomains.

### Step 1: Search for a Suitable Module

```text
marketplace search certificate_transparency
```

### Step 2: Install the Module

Use the exact module path returned by the marketplace. If the following path exists:

```text
recon/domains-hosts/certificate_transparency
```

install it using:

```text
marketplace install recon/domains-hosts/certificate_transparency
```

### Step 3: Load and Inspect the Module

```text
modules load recon/domains-hosts/certificate_transparency
info
options list
```

### Step 4: Configure and Execute

```text
options set SOURCE kali.org
run
back
show hosts
```

Repeat for other domains if the module supports them.

## 12. Netcraft Footprinting

Netcraft is a source of publicly available website and hosting information.

### Step 1: Search for a Module

```text
marketplace search netcraft
```

### Step 2: Install the Available Module

Use the exact module path returned by the search. For example, if available:

```text
marketplace install recon/domains-hosts/netcraft
```

### Step 3: Load and Inspect It

```text
modules load recon/domains-hosts/netcraft
info
options list
```

### Step 4: Set the Target and Execute

```text
options set SOURCE kali.org
run
back
show hosts
```

If the module is unavailable or incompatible with the current service, document the issue and use another supported public source.

## 13. WHOIS Information Gathering

WHOIS can provide registration-related information such as the registrar, registration dates, and name servers, subject to registry policies and privacy protection.

If the WHOIS utility is unavailable, exit Recon-ng:

```text
exit
```

Install the utility in the Kali terminal:

```bash
sudo apt install whois
```

Query the domain:

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

Record the information actually returned. Some domains may use privacy protection or registry services that limit the available details.

## 14. Threat Intelligence

Threat intelligence involves examining public security reports and indicators to determine whether domains or associated infrastructure have been reported as suspicious.

### Step 1: Search Recon-ng Modules

Inside Recon-ng, enter:

```text
marketplace search threat
```

Review the available modules and their documentation.

### Step 2: Check Module Requirements

```text
info
options list
```

Some providers require API keys or accounts. Configure them only according to the provider's documented requirements.

### Step 3: Record Findings

For each domain, document:

- Source or provider used
- Date of the lookup
- Indicator or report returned
- Whether the result was verified
- Any errors or unavailable services

A missing threat report does not prove that a domain or its infrastructure is completely safe.

## 15. Viewing and Verifying Results

### Display Hosts

```text
show hosts
```

### Display Domains

```text
show domains
```

### Display Contacts

```text
show contacts
```

### Display Database Schema

```text
db schema
```

The available tables and records depend on the modules used and the information collected. Empty tables are possible.

## 16. Important Recon-ng Commands

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
| `info` | View module information |
| `options list` | View configuration options |
| `options set SOURCE kali.org` | Set the target domain |
| `run` | Execute the loaded module |
| `back` | Return to the previous prompt |
| `show hosts` | Display discovered host records |
| `db schema` | Display database structure |
| `exit` | Exit Recon-ng |

## 17. Troubleshooting

### Problem 1: No Modules Found

**Solution:** Search the marketplace and install the required module.

```text
marketplace search hackertarget
```

### Problem 2: Module Not Found

**Solution:** Copy the exact module path returned by the marketplace. Check spelling and module availability.

### Problem 3: Missing API Key

**Solution:** Read the module information and configure the required provider credentials if you have authorized access.

### Problem 4: No Hosts Discovered

**Solution:**
- Verify the target using `options list`.
- Confirm that the module ran successfully.
- Check internet connectivity.
- Try another available public source.
- Record an empty result if no records are returned.

### Problem 5: WHOIS Command Not Found

**Solution:**

```bash
sudo apt install whois
```

### Problem 6: Threat-Intelligence Module Unavailable

**Solution:** Record the unavailable module and use a supported public threat-intelligence source if your lab permits it.

## 18. Screenshots to Include

Capture the following screenshots for the lab record:

1. Kali Linux terminal and internet connectivity.
2. Recon-ng installation and startup.
3. Marketplace module search.
4. Workspace creation and loading.
5. HackerTarget module information and options.
6. Module execution and discovered host records.
7. Certificate Transparency module and results, if available.
8. Netcraft module and results, if available.
9. WHOIS command output.
10. Threat-intelligence source or module results.
11. Final `show hosts` output.

Screenshots should show actual command output. Do not add fabricated hostnames or results.

## 19. Result

Passive footprinting was conducted using Recon-ng and available public OSINT sources for the six assigned domains. The actual hostnames and domain-registration or intelligence information returned by the tools were recorded for analysis. Source availability, module support, and API requirements affected the results.

## 20. Conclusion

This experiment demonstrated the use of Recon-ng for passive footprinting and OSINT collection. It provided practical experience with installing modules, managing workspaces, configuring target domains, executing reconnaissance modules, and examining collected information.

The experiment also demonstrated the importance of verifying OSINT findings and documenting source limitations during a cybersecurity assessment.

## 21. Ethical Considerations

- Use public information responsibly.
- Perform reconnaissance only for legitimate educational or authorized security purposes.
- Do not attempt unauthorized access or exploitation.
- Respect the terms of service and usage limits of external sources.
- Do not treat unverified intelligence results as confirmed security findings.
