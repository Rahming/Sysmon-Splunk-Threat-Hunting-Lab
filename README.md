# Sysmon-Splunk-Threat-Hunting-Lab


## Overview
<img width="522" height="102" alt="Untitled Diagram" src="https://github.com/user-attachments/assets/57e21ac9-d56a-4f1a-a0f8-43eee67a1cb4" />

Deploy Sysmon, forward logs to Splunk, simulate malicious activity, and investigate endpoint events using Splunk SPL.

## Lab Environment
| Component         | Purpose        |
|-------------------|----------------|
|Kali linux(VMware) |Test Executable |
|Windows 11(Vmware) |Endpoint monitored by Sysmon|
|Sysmon | Endpoint telemetry generation|
|Splunk Universal Forwarder| Log forwarding|
|Ubuntu Server(VMware)| Splunk Enterprise SIEM|

## Objectives
1. Downlaod Sysmon using the SwiftOnSecurity configuration

2. Configure Splunk Universal Forwarder

3. Forward Sysmon logs to Splunk Enterprise

4. Simulate adversary activity

5. Investigate endpoint telemetry

6. Correlate Sysmon events

## Lab Setup
1. Downloaded Sysmon with SwiftOnSecurity configuration

<img width="799" height="293" alt="Screenshot (304)" src="https://github.com/user-attachments/assets/2fd2e2b0-c120-4a02-beb3-8f5ace50aa6c" />

2. Made HelloSysmon.exe on Kali(VM IP:192.168.112.132)

<img width="522" height="103" alt="Screenshot (307)" src="https://github.com/user-attachments/assets/444c2aee-e13f-4cd9-84b8-18c7473f5cd7" />

3. Downloaded the executable to Windows 11(VM IP:192.168.112.133) and Executed the file
<img width="319" height="609" alt="Screenshot (310)" src="https://github.com/user-attachments/assets/6f994ca8-5cbd-411a-9b8d-f0a829cff889" />
<img width="481" height="84" alt="Screenshot (309)" src="https://github.com/user-attachments/assets/3d737d7e-6e21-464c-a693-abe16aa062db" />
 
4. Generated outbound network traffic

<img width="1231" height="111" alt="Screenshot (314)" src="https://github.com/user-attachments/assets/adc5bd55-72de-42aa-b9b2-bb44abf0769a" />

5. Collected telemetry with Sysmon

<img width="713" height="987" alt="Screenshot (332)" src="https://github.com/user-attachments/assets/f303c39b-3357-4824-81ab-c416124a52a7" />

6. Investigated activity in splunk

<img width="438" height="92" alt="Screenshot (311)" src="https://github.com/user-attachments/assets/77f431d3-920e-4367-a74f-6f34793519f7" />

Configuration for the Splunk Universal Forwarder


## Dectection Results
Event 15 - File Download
<img width="1598" height="458" alt="Screenshot (328)" src="https://github.com/user-attachments/assets/eb9eb3d5-bb44-47c0-a667-9d10702ab9d4" />
Recorded the creation of HelloSysmon.exe. Included download URL and hashes in the SPL 

Event ID 1 - Process Creation
<img width="1598" height="328" alt="Screenshot (330)" src="https://github.com/user-attachments/assets/e501df29-81a0-4e2a-8f72-695a4de044c4" />
Confirmed execution of HelloSysmon.exe. Included parent process in the SPL to show that the executable was lauched by a user(Explorer.exe)

Event ID 3 - Network Connection
<img width="1465" height="337" alt="Screenshot (327)" src="https://github.com/user-attachments/assets/fd7fe84d-13dd-4bb5-ae3a-69d55dbb69df" />
Shows HelloSysmon.exe conection to the windowsVM(192.168.112.132) on port 31337

## TimeLine

|Time|Event|
|----|----|
|23:00:20|HelloSysmon.exe downloaded|
|23:00:33|HelloSysmon.exe executed|
|23:00:34|Network connection established|

## Relevant MITRE ATT&CK Techniques
|Technique|Description|
|---------|-----------|
|T1105| Ingress Tool Transfer|
|T1204| User Execution|
|T1071| Application Layer Protocol
## Skills Learned
- Sysmon deployment and configuration
- Splunk administration
- Log forwarding
- Threat hunting
- Endpoint monitoring
- Event correlation
- IOC analysis
- SPL query development

# Conclusion
This project demonstrated how Sysmon and Splunk can be used together to detect and investigate endpoint activity. By correlating file download, process creation, and network connection events, it was possible to reconstruct the full attack chain and validate telemetry collection through centralized logging.
