# Forensics-IR

# 🔍 [Network Forensic Analysis](https://github.com/DDMetoyer/Forensics-IR/blob/main/Network%20forensic%20analysis.pdf)

## 📖 Overview
This project involves a detailed network forensic analysis using the Volatility Framework. The goal was to investigate a memory dump (`TORNBERG.dmp`) to uncover network connections, detect signs of process injection, and identify suspicious processes involved in malicious activity.

## 🎯 Objectives
- Analyze memory dump to identify active network connections.
- Detect and analyze process injection using memory artifacts.
- Identify and attribute malicious activities based on memory forensic data.

## 🛠️ Tools & Techniques
- **Volatility Framework**: Memory forensic analysis
- **Kali Linux** (WSL): Execution environment
- **Notepad++**: Analyzing extracted data

## ⚙️ Methodology
### Step 1: Network Connection Analysis
- **Command Used:**
  ```bash
  volatility -f TORNBERG.dmp --profile=Win8SP1x64 netscan -v > torn_netscan.txt
  ```
- Identified an established connection from the local IP (`10.252.9.131:49633`) to remote IP (`10.139.205.204:4444`) associated with `powershell.exe` (PID: 1748).

### Step 2: Process Injection Detection
- Used the `malfind` plugin to detect suspicious memory regions indicating malicious injections.
- Used the `apihooks` plugin to identify suspicious hooking activities.
- Used the `ldrmodules` plugin to identify loaded malicious DLLs across processes, finding PID 5012 responsible for injecting malicious code into PID 1748.

### Step 3: Remote Desktop Protocol (RDP) Analysis
- Confirmed the presence of an established RDP connection on port `3389` managed by the `svchost.exe` process.
- Verified the host IP address as `10.252.9.131`.

## 🚩 Key Findings
- **Malicious Activity Identified:** Process injection targeting `powershell.exe` (PID: 1748).
- **Responsible Process:** PID 5012 identified as responsible for malicious DLL injection.
- **RDP Connection Established:** Host was acting as an RDP server.

## 📑 Conclusion
This analysis successfully identified the processes involved in malicious activity and established detailed evidence of network connections and unauthorized process injections. Such forensic analysis provides critical insights into attacker behavior and helps refine defense strategies.

## 📌 Disclaimer
This project is for educational and research purposes only. Misuse of tools or information presented here is strictly prohibited.

---

*Developed by Devante Metoyer, University of Arizona - CYBV 400: Active Cyber Defense*
