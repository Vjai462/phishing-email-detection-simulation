Problem	Phase	Difficulty	Solution	Date	Status	Learning
Windows Server 2022 can’t install .NET Framework 3.5 through Windows Features	Phase 1	Medium	Use Server Manager → Add roles and features OR PowerShell Enable-WindowsOptionalFeature.
Alternative: Manual .NET download + install.	Sept 6, 2025	✅ Done	Legacy apps need old frameworks. hMailServer relies on legacy .NET.
Forgotten Admin Account Password (lost admin@sber.local
)	Phase 1	Easy	Reset password in hMailServer Administrator under Domains → Accounts. Enter new password.	Sept 7, 2025	✅ Done	Lab admins can reset passwords directly; always document test creds.


# 🐞 Problems & Solutions

| Problem | Phase | Difficulty | Solution | Date | Status | Learning |
|---------|-------|------------|----------|------|--------|----------|
| Windows Server 2022 can’t install .NET Framework 3.5 through Windows Features | Phase 1 | Medium | Use **Server Manager** → Add roles and features OR PowerShell `Enable-WindowsOptionalFeature`. <br> Alternative: Manual .NET download + install. | Sept 6, 2025 | ✅ Done | Legacy apps need old frameworks. hMailServer relies on legacy .NET. |
| Forgotten Admin Account Password (lost admin@sber.local) | Phase 1 | Easy | Reset password in hMailServer Administrator under **Domains → Accounts**. Enter new password. | Sept 7, 2025 | ✅ Done | Lab admins can reset passwords directly; always document test creds. |
