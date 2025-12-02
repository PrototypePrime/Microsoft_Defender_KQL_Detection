# Endpoint Detections

Detection rules for Microsoft Defender for Endpoint (MDE).

## 🎯 What Goes Here
- Malware execution
- PowerShell abuse
- Process injection
- Ransomware behavior
- Persistence (Registry/Services)

## 🔍 Common MITRE Techniques
| ID | Technique | Description |
|----|-----------|-------------|
| **T1059** | Command and Scripting Interpreter | PowerShell/CMD |
| **T1055** | Process Injection | DLL Injection |

## 🚀 Sample Detection
See `Sample_T1059_PowerShell_Download.kql` for a production-ready example.
