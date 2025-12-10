# Contributing to Microsoft Defender KQL Detection Library

First off, thank you for considering contributing! This library relies on security practitioners like you to stay ahead of emerging threats.

## 🤝 How to contribute

### 1. Add a New Detection
1.  **Fork** the repository.
2.  **Create** a branch: `git checkout -b detection/T1234-my-detection`
3.  **Copy** one of the templates:
    *   `templates/TEMPLATE_Standard_Alert.kql` (For production rules)
    *   `templates/TEMPLATE_Threat_Hunting.kql` (For hunting queries)
4.  **Write** your KQL logic.
5.  **Test** it! (See Testing Guidelines below).
6.  **Push** and submit a Pull Request.

### 2. Improve Existing Detections
*   Found a logic error?
*   Have a better way to filter false positives?
*   Want to support a new table (e.g., `IdentityLogonEvents`)?
*   **PRs are welcome!**

---

## 🧪 Testing Guidelines

We aim for **production-ready** code. Please verify the following before submitting:

*   **Syntax**: Does the KQL run in Advanced Hunting / Azure Sentinel?
*   **Performance**: Do you filter by `TimeGenerated` and indexed fields first?
*   **Schema**: Do you use standard tables (`DeviceProcessEvents`, `SigninLogs`)?
*   **Documentation**: Did you fill out the Description, Risk Level, and False Positives?

---

## 📝 Pull Request Template

When submitting a PR, please provide:

```markdown
## Detection Overview
- **Name**: [Name of detection]
- **MITRE Technique**: [T####]
- **Goal**: [What does this catch?]

## Testing Support
- [ ] I have tested this query in Defender/Sentinel.
- [ ] It returns results for the intended threat.
- [ ] It does NOT generate excessive noise.

## Screenshots (Optional)
[Paste screenshot of hunting results]
```
