# Ethical Hacking Lab: Network Traffic Capture and Analysis with Wireshark

A practical lab focused on capturing, inspecting, and analyzing network traffic using Wireshark in a controlled and authorized environment.

This project introduces the fundamentals of packet-level analysis, helping learners understand how network communication works at the protocol level and how tools like Wireshark can be used for troubleshooting and security analysis.

## Overview

Wireshark is a network protocol analyzer used to capture and inspect packets on a local network. It helps identify:

- source and destination IP addresses
- protocols in use
- packet timestamps and lengths
- TCP, UDP, DNS, ICMP, and HTTP traffic
- application-level and transport-level behavior

In this experiment, live traffic is captured, filtered, and analyzed to understand the structure of network communication. The goal is educational and ethical, limited to authorized networks and systems.

## Objectives

- Understand the basics of packet capture and analysis.
- Install and open Wireshark in Kali Linux.
- Select an appropriate network interface.
- Capture live traffic safely and ethically.
- Identify key packet fields such as source, destination, protocol, and length.
- Apply Wireshark display filters for TCP, UDP, DNS, ICMP, and HTTP traffic.
- Save the capture in `.pcapng` format for later review.
- Document observations from the packet analysis.

## Tools and Technologies

- Wireshark
- Kali Linux
- Network interface (Wi-Fi or Ethernet)
- Terminal
- Authorized local network or test environment

## Requirements

- A Kali Linux installation or compatible system
- Wireshark installed and configured
- An active network connection
- Permission to capture traffic on the network being analyzed
- Optional internet access for general browsing and traffic generation

## Installation

On Kali Linux, install Wireshark using:

```bash
sudo apt update
sudo apt install wireshark -y
```

Launch Wireshark:

```bash
wireshark
```

## Capturing Network Traffic

### 1. Start Wireshark

Open the application and choose an active interface such as:

- Wi-Fi
- Ethernet
- Virtual network adapter

Double-click the interface to begin capturing packets.

### 2. Generate network traffic

Open a browser or perform a normal network activity on an authorized system, such as:

- loading a page
- performing a DNS lookup
- sending a ping request

Then return to Wireshark to observe the captured traffic.

> Only capture network traffic on networks and devices that you own or are authorized to analyze.

### 3. Observe captured packets

The packet list shows fields such as:

| Field | Description |
|---|---|
| No. | Packet number |
| Time | Capture time |
| Source | Sender address |
| Destination | Receiver address |
| Protocol | Network protocol used |
| Length | Packet size |
| Info | Brief summary of the packet |

### 4. Inspect individual packets

Select a packet and review:

- Packet Details pane
- Ethernet information
- IP header
- TCP or UDP details
- DNS, ICMP, or HTTP details if present

## Display Filters

Use the display filter bar to narrow the traffic shown.

### TCP packets

```text
tcp
```

### DNS packets

```text
dns
```

### ICMP packets

```text
icmp
```

### UDP packets

```text
udp
```

### HTTP packets

```text
http
```

### Traffic involving a specific IP

```text
ip.addr == 192.168.1.10
```

Replace the IP address with one relevant to your lab environment.

> Display filters do not remove packets from the capture; they only hide or show specific ones.

## Analysis Steps

1. Apply a few display filters.
2. Compare packet source and destination addresses.
3. Inspect packet timing and lengths.
4. Review DNS requests and responses.
5. Observe TCP connection behavior.
6. Record findings relevant to the lab.

The packets shown depend on your network activity. Some protocols may not appear in every capture.

## Stopping and Saving the Capture

### Stop the capture

Click the red stop button in the Wireshark toolbar.

### Save the file

1. Go to File → Save As
2. Choose a destination folder
3. Name the file, for example:

```text
experiment1_capture.pcapng
```

4. Save in `.pcapng` format

The capture can be reopened later for further review.

## Common Display Filters

| Purpose | Filter |
|---|---|
| TCP | `tcp` |
| UDP | `udp` |
| DNS | `dns` |
| ICMP | `icmp` |
| HTTP | `http` |
| HTTPS / TLS | `tls` |
| IPv4 | `ip` |
| IPv6 | `ipv6` |
| ARP | `arp` |
| Specific IP | `ip.addr == 192.168.1.10` |

## Sample Observation Table

| Sl. No. | Protocol | Source | Destination | Observation |
|---|---|---|---|---|
| 1 | DNS | Local system | DNS resolver | Query or response observed |
| 2 | TCP | Local system | Remote host | Communication observed |
| 3 | UDP | Local system | Remote host | UDP packet observed |
| 4 | ICMP | Test system | Target host | Ping packet observed |

> Use actual data from your capture rather than sample values when preparing the report.

## Result

Network traffic was successfully captured and analyzed using Wireshark. Protocols were observed through packet inspection, display filters were applied, and packet details were reviewed to understand the network communication occurring on the authorized test environment.

## Conclusion

This experiment introduced practical packet analysis using Wireshark. It helped demonstrate how network traffic is captured, how protocols are identified, and how packet data can be inspected to understand communication behavior in a network.

## Learning Outcomes

- Learned how to capture live network traffic.
- Understood packet list information.
- Practiced Wireshark display filters.
- Examined protocol headers and packet details.
- Saved packet captures for later analysis.
- Gained a foundational understanding of network analysis.

## Safety and Ethical Guidelines

- Capture traffic only on networks and devices you own or are authorized to test.
- Do not collect or share other people's private network data.
- Store packet captures securely because they may contain sensitive information.
- Use this lab only for educational, troubleshooting, or authorized security testing purposes.

## References

- Wireshark Official Website: https://www.wireshark.org/
- Wireshark User's Guide: https://www.wireshark.org/docs/wsug_html_chunked/
- Wireshark Display Filter Reference: https://www.wireshark.org/docs/dfref/

## Project Summary

- Project: Network Traffic Capture and Analysis Using Wireshark
- Platform: Kali Linux
- Tool: Wireshark
