# Splunk SOC Home Lab

## Project Overview

This project demonstrates a Security Operations Center (SOC) home lab using Splunk Enterprise and Splunk Universal Forwarder.

The goal was to collect Windows Event Logs and send them to Splunk for monitoring and analysis.

## Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Windows Event Logs
- Windows 11

---

## Architecture

Windows Endpoint
|
v
Splunk Universal Forwarder
|
Port 9997
|
v
Splunk Enterprise
|
v
Search and Monitoring

---

## Installation Steps

### Step 1: Install Splunk Enterprise

1. Download Splunk Enterprise
2. Run installer
3. Create admin account
4. Access Splunk at:

http://localhost:8000 or http://127.0.0.1:8000

### Step 2: Install Universal Forwarder

1. Download Universal Forwarder
2. Install on Windows machine

### Step 3: Enable Receiving Port on Splunk

Settings → Forwarding and Receiving

Add receiving port:

9997

### Step 4: Add Forward Server

Command:

```cmd
splunk add forward-server <Splunk_Server_IP>:9997
```

Example:

```cmd
splunk add forward-server 127.0.0.1:9997
```

### Step 5: Configure inputs.conf

```ini
[WinEventLog://Security]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:Security

[WinEventLog://System]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:System

[WinEventLog://Application]
disabled = 0
index = wineventlog
sourcetype = WinEventLog:Application
```

### Step 7: Restart Forwarder

```cmd
splunk restart
```

### Step 8: Verify Logs

Search:

```spl
index=wineventlog sourcetype="WinEventLog:Security"
```

Expected Events:

- Event ID 4624
- Event ID 4625
- Event ID 4688
- Event ID 4720

## Skills Learned

- SIEM Fundamentals
- Log Collection
- Windows Event Monitoring
- Splunk Administration
- Universal Forwarder Configuration
