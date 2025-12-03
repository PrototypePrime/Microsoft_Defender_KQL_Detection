# Identity Detections

Detection rules for Azure AD and on-prem identity abuse.

## 🎯 What Goes Here
- Privilege Escalation
- Role Changes
- New Admin Accounts
- Service Principal Abuse

## 🔍 Common MITRE Techniques
| ID | Technique | Description |
|----|-----------|-------------|
| **T1098** | Account Manipulation | Role changes |
| **T1136** | Create Account | Persistence |

## 🚀 Sample Detection
See `Sample_T1098_Privileged_Role_Change.kql` for a production-ready example.
