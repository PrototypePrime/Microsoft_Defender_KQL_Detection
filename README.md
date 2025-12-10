# Microsoft Defender KQL Detection Library

<div align="center">

![Microsoft Defender](https://img.shields.io/badge/Microsoft-Defender%20XDR-00A4EF?style=for-the-badge&logo=microsoft)
[![Azure Sentinel](https://img.shields.io/badge/Azure-Sentinel-0078D4?style=for-the-badge&logo=microsoftazure)](https://azure.microsoft.com/services/azure-sentinel/)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK%20Mapped-red?style=for-the-badge)](https://attack.mitre.org/)

**Enterprise KQL Detection Logic & Engineering Toolkit**

*Curated by Mathan | Senior Security Engineer*

[🚀 Quick Start](#-quick-start) • [📁 Categories](#-detection-categories) • [📖 Documentation](#-detection-engineering-workflow) • [🤝 Contributing](#-contributing)

<!-- SEO: Microsoft Defender detection rules, KQL queries, Azure Sentinel analytics, threat detection, M365 security, advanced hunting queries, Kusto query language, security analytics, cloud security detection, identity threat detection, Microsoft 365 Defender, endpoint detection, email security rules, MITRE ATT&CK Microsoft, detection engineering, SOC automation, threat hunting KQL, Azure AD security, Office 365 security, incident detection, security operations, KQL analytics -->

</div>

---

## 📋 Overview

This repository is **two things in one**:

1.  **📚 A Production Detection Library**: Battle-tested KQL queries for Microsoft's integrated security platform, covering endpoint, identity, email, and cloud threats.
2.  **🛠️ A Detection Engineering Toolkit**: A structured framework and set of rules to help you build, test, and document your *own* custom Analytics Rules with the same high standards.

**Our Philosophy:** *Don't reinvent the wheel. Use our logic where it fits, modify it where it doesn't, or use our templates to build something entirely new.*

### Key Features
✅ **Multi-platform** - Defender XDR, Defender for Endpoint, Azure Sentinel  
✅ **Cloud-native** - Optimized for M365 and Azure environments  
✅ **Identity-focused** - Azure AD and OAuth attack detection  
✅ **Automated** - Ready for analytics rules and Logic Apps  
✅ **MITRE-aligned** - Comprehensive ATT&CK coverage

---

## 📁 Detection Categories

**8 categories** optimized for Microsoft's security ecosystem:

<table>
<tr>
<td width="25%" align="center">
<h3>🔐 Authentication</h3>
<b>Identity Attack Detection</b><br/>
<sub>Impossible Travel • Password Spray • MFA</sub>
</td>
<td width="25%" align="center">
<h3>💻 Endpoint</h3>
<b>Defender for Endpoint</b><br/>
<sub>Malware • LOLBins • Process Injection</sub>
</td>
<td width="25%" align="center">
<h3>🌐 Network</h3>
<b>Network Anomalies</b><br/>
<sub>C2 • Suspicious Connections</sub>
</td>
<td width="25%" align="center">
<h3>☁️ Cloud</h3>
<b>Azure & M365 Security</b><br/>
<sub>Privilege Escalation • API Abuse</sub>
</td>
</tr>
<tr>
<td width="25%" align="center">
<h3>📧 Mail</h3>
<b>Defender for Office 365</b><br/>
<sub>Phishing • BEC • Email Rules</sub>
</td>
<td width="25%" align="center">
<h3>🌍 Web</h3>
<b>Browser & Web Threats</b><br/>
<sub>Drive-by Downloads • Malicious Extensions</sub>
</td>
<td width="25%" align="center">
<h3>📊 Data</h3>
<b>DLP & Exfiltration</b><br/>
<sub>Cloud Storage • Mass Downloads</sub>
</td>
<td width="25%" align="center">
<h3>👤 Identity</h3>
<b>Azure AD & IAM</b><br/>
<sub>OAuth Abuse • Role Changes</sub>
</td>
</tr>
</table>

---

## 🚀 Quick Start

### Prerequisites
- Microsoft 365 E5 / A5, OR Microsoft Defender for Endpoint Plan 2 + Azure AD Premium P2
- Access to Defender XDR (`security.microsoft.com`) or Azure Sentinel

### How to Use This Library

#### Option A: Deploy Existing Rules (Fastest) ⚡
1.  **Browse** the categories above (e.g., `Authentication/T1078_Impossible_Travel.kql`).
2.  **Copy** the KQL query.
3.  **Run** it in specific environment:
    *   **Defender XDR:** Go to **Hunting** → **Advanced Hunting**.
    *   **Azure Sentinel:** Go to **Logs**.
4.  **Create** an Analytics Rule or Custom Detection policy from the query.

#### Option B: Build Custom Rules (Flexible) 🛠️
1.  **Navigate** to the `templates/` directory.
2.  **Choose** a template:
    *   `TEMPLATE_Standard_Alert.kql` for standard production alerts.
    *   `TEMPLATE_Threat_Hunting.kql` for exploratory queries.
3.  **Customize** the logic.

#### Option C: Modify Our Logic (Hybrid) 🔄
1.  **Start** with an existing KQL query from this library.
2.  **Adjust** thresholds (e.g., `... | where failed_count > 20`).
3.  **Add** environmental filters (e.g., `... | where DeviceName !startswith "Dev-"`).

---

## 📖 Detection Engineering Workflow

Whether you are using our rules or building your own, we recommend this standard workflow:

```mermaid
graph TD
    A[1. Select Logic] --> B{Source?}
    B -->|Our Library| C[3. Test Query Performance]
    B -->|Custom Template| D[2. Write KQL Query]
    D --> C
    C --> E{Slow?}
    E -->|Yes| F[4. Optimize Query]
    F --> C
    E -->|No| G[5. Configure & Monitor]
    G --> H{FP Rate?}
    H -->|High| I[6. Tune for Environment]
    I --> G
    H -->|Low| J[7. Deploy to Prod]
    
    style A fill:#2563eb,color:#fff,stroke:#1e40af,stroke-width:3px
    style J fill:#16a34a,color:#fff,stroke:#15803d,stroke-width:3px
    style E fill:#ea580c,color:#fff,stroke:#c2410c,stroke-width:3px
```

### 1. The Logic Core (KQL)
Efficient KQL usage is critical for cloud-scale data.

**Example Logic:**
```kql
let timeframe = 24h;
SigninLogs
| where TimeGenerated >= ago(timeframe)
| where ResultType == "0"
| project TimeGenerated, UserPrincipalName, IPAddress, Location
| order by UserPrincipalName, TimeGenerated asc
| serialize
| extend prev_location = prev(Location)
| where UserPrincipalName == prev(UserPrincipalName) and Location != prev_location
// [logic continues to calculate impossible travel]
```

### 2. Testing & Validation
Use **Event-Horizon** (our sister project) or Microsoft's own Attack Simulator.

**Recommended Tool:** [Event-Horizon](https://github.com/PrototypePrime/Event-Horizon)

---

## 📊 Essential Tables

| Table | Data Source | Common Use Cases |
|-------|-------------|------------------|
| `SigninLogs` | Azure AD | Authentication attacks, impossible travel |
| `DeviceProcessEvents` | MDE | Process execution, command lines |
| `DeviceNetworkEvents` | MDE | Network connections, C2 detection |
| `EmailEvents` | MDO | Phishing, BEC, email threats |
| `CloudAppEvents` | MDCA | SaaS app activity, file operations |

---

## 🤝 Contributing

We welcome contributions! If you've created a rule using our templates or optimized one of ours:

1.  **Fork** this repository.
2.  **Create** a feature branch.
3.  **Submit** a Pull Request with your detection logic and testing results.

---

## 👤 About

### Implementation & Maintenance
**PrototypePrime (Mathan Subbiah)**  
*Senior Security Engineer | Detection Engineering Specialist*

Focused on cloud and identity threat detection for Microsoft security stack.

[![GitHub](https://img.shields.io/badge/GitHub-PrototypePrime-181717?logo=github&style=flat-square)](https://github.com/PrototypePrime)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Mathan%20Subbiah-0A66C2?logo=linkedin&style=flat-square)](https://www.linkedin.com/in/mathan-subbiah-0bb47aa8/)
[![Email](https://img.shields.io/badge/Email-mathan1702%40gmail.com-D14836?logo=gmail&style=flat-square)](mailto:mathan1702@gmail.com)

### Related Projects
- [Event-Horizon](https://github.com/PrototypePrime/Event-Horizon) - Production-quality security log generator
- [Splunk SPL Detection](https://github.com/PrototypePrime/Splunk_SPL_Detection)
- [Cortex XDR XQL Detection](https://github.com/PrototypePrime/Cortex_XDR_XQL_Detection)

---

## 📄 License
MIT License - see [LICENSE](LICENSE) file for details.

<div align="center">

### ⭐ Star This Repository!
*Help the community discover these KQL detection rules*

![Visitors](https://visitor-badge.laobi.icu/badge?page_id=PrototypePrime.Microsoft_Defender_KQL_Detection)

</div>
