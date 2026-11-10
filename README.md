<div align="center">

# 🔐  NETWORKWALKS WK1-B084 PM1 WIRESHARK PROJECT

**ethical hacking wireshark project**
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/WIRE%20SHARK-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Iniubong%20Etido%20Usoro-C00000?style=flat-square" />
</p>

---
<br>
---

## 📌 Project Overview
This repository documents the implementation of an isolated virtual cybersecurity laboratory environment utilized for security analysis, network forensics, and penetration testing. The primary focus of this phase involves acting as a **Security Operations Center (SOC) Analyst** to investigate real-world network packet captures, identifying indicators of compromise (IoCs), malicious actors, and unauthorized data exfiltration.

### Core Core Competencies Practiced:
**Threat Hunting:** Pinpointing attacker IP addresses within massive traffic logs.
**Session Reconstruction:** Following TCP Streams to read plaintext conversations.
**Data Forensic Analysis:** Extracting hidden files and payload data.
**Credential Auditing:** Detecting plaintext HTTP credentials (usernames and passwords).
**Brute Force Detection:** Identifying high-frequency authentication tracking.
**VoIP Traffic Analysis:** Inspecting Session Initiation Protocol (SIP) and Real-time Transport Protocol (RTP) packet flows.

---

## 🔬 SOC Laboratory Modules Summary
The environment evaluates network traffic across 6 core practice capture files provided by NetworkWalks:

| Lab Module | Focus Objective | Investigation Highlights |
| :--- | :--- | :--- |
| **Lab 3** | Identify the Attacker's IP | Isolate malicious network flows from standard internal traffic. |
| **Lab 4** | Follow TCP Stream 1 | Rebuild conversation structures to verify exposed information. |
| **Lab 5** | Follow TCP Stream 2 | Advanced session tracking to discover encoded payloads and hidden data. |
| **Lab 6** | HTTP Plain Text Credentials | Detect vulnerable cleartext transmissions containing sensitive administrative logins. |
| **Lab 7** | Catch the Brute Force Attacker | Track anomalous packet volumes indicating active dictionary or password guessing attacks. |
| **Lab 8** | Catch the Call Scammer | Deep-dive into malicious VoIP systems to uncover social engineering or vishing attacks. |

---

## 📘 Case Study: Lab 8 – VoIP Call Replay Analysis

### 1. Objective
Investigate an intercepted corporate voice network capture containing a suspected fraudulent phone call. The goal is to perform a full packet dissection of the VoIP communication chain to identify the orchestrator, target, protocols used, and underlying sensitive data exfiltration.

### 2. Traffic Inspection Deep-Dive
Using advanced Wireshark filtering expressions (`sip` or `rtp`), the protocol handshake and session initiation were parsed:

* **Protocol Identification:** The communication establishes connection via the **Session Initiation Protocol (SIP)** for call setup, followed by a voice stream payload.
* **Session Handshake Architecture (Packet Analysis):**
  * `Packet 51`: `INVITE sip:202@192.168.10.52` initiates the call request.
  * `Packet 52`: `Status: 100 Trying` confirms the request processing.
  * `Packet 69`: `Status: 180 Ringing` indicates terminal alert.
  * `Packet 84`: `Status: 200 OK` confirms call acceptance and session description negotiation.
  * `Packet 85`: `ACK` completes the three-way VoIP handshake.

```text
  Caller: Ali Raza                                 Recipient: Sara
 (192.168.10.45:5060)                           (192.168.10.52)

          |                                             |
          | ----- INVITE (sip:202@192.168.10.52) -----> |
          | <---- 100 Trying -------------------------- |
          | <---- 180 Ringing ------------------------- |
          | <---- 200 OK (Session Decription) --------- |
          | ----- ACK --------------------------------> |
          |                                             |
          | <========== Voice Stream (RTP) ===========> |
```

### 3. Key Forensics Indicators Found
By inspecting the packet details header for the `INVITE` sequence:
* **Caller Identity:** `From: "Ali Raza" <sip:101@192.168.10.45>`
* **Target Identity:** `To: "Sara" <sip:202@192.168.10.52>`
* **Source Node Endpoint:** `192.168.10.45` on port `5060`
* **Target Extension:** Extension `202`

### 4. Forensic Investigation Metrics Tracked
To complete a comprehensive assessment of this incident, the lab successfully processed the following forensic parameters to achieve an **Outstanding 100/100 marks Evaluation**:
1. **Traffic Capture Verification:** Confirmed the integrity of the trace data file.
2. **Call Setup Protocol Extraction:** Standardized on SIP parameters.
3. **Voice Protocol Identification:** Analyzed RTP streams transporting media data.
4. **Caller Extension Identification:** Mapped origin extension to `101`.
5. **Caller Name Isolation:** Resolved to attacker moniker `Ali Raza`.
6. **Codec Decoding:** Extracted media payload specifications (e.g., PCMA/PCMU audio encoding profiles).
7. **Recipient Resolution:** Mapped endpoint answering string directly to `Sara`.
8. **Exfiltrated Card Numbers:** Reconstructed audio streams or DTMF tones to obtain exposed financial primary account numbers.
9. **Expiration Date Mining:** Isolated related numerical parameters from the exfiltration string.
10. **The Security Fix Execution:** Recommended mitigation frameworks (e.g., implementing SIP-TLS signaling encryption and Secure RTP (SRTP) for media encapsulation).

---

## 🚀 How to Replicate
1. Ensure **VirtualBox (v7.2+)** is configured with an internal network adapter space mirroring the target subnet structure (`10.0.0.0/24`).
2. Deploy a **Kali Linux (v2026.2)** instance within the host boundary to act as your analysis platform.
3. Load the corresponding network capture files (`.pcapng`) into Wireshark.
4. Utilize localized traffic display filters such as `http.request.method == "POST"`, `tcp.flags.syn == 1`, or `sip` to rapidly extract the indicators documented above.
# NETWORKWALKS-Iniubong-B084-WK1-PM1-WIRESHARK
below is the screenshot from the lab work
<p align="center">
  <img src="./Screenshort%201.jpeg" alt="Screenshot 1" width="600" />
  <br />
  <img src="./Wireshark%20VoIP%20Lab%20Scorecard.png" alt="Wireshark VoIP Lab Scorecard" width="600" />
</p>
