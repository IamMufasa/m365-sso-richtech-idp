
# Microsoft 365 SAML SSO with Shibboleth IdP – RichTech University

This project demonstrates a full implementation of SAML-based Single Sign-On (SSO) between **RichTech University's** on-premises **Shibboleth Identity Provider (IdP)** and **Microsoft 365 (Azure AD / Entra ID)** cloud services.

It simulates a real-world higher education environment where faculty, students, and IT staff use their campus credentials to securely access Microsoft 365 applications like Outlook, Teams, and OneDrive via SAML authentication.

---

## 🔧 What’s Included

- ✅ Shibboleth IdP configuration files (production-style)
- ✅ Azure AD (Microsoft 365) metadata setup
- ✅ Attribute mapping and filtering logic
- ✅ LDIF user data for OpenLDAP directory integration
- ✅ Full step-by-step walkthrough in Markdown format

---

## 📂 Project Structure

```
m365-sso-richtech-idp/
├── docs/                # Walkthrough and documentation
├── config/              # Shibboleth IdP configuration files
├── metadata/            # SP and IdP SAML metadata
└── README.md
```

---

## 🧠 Use Case

This project was built to showcase practical skills for an **IAM Systems Administrator** role, highlighting:

- Identity Federation (SAML 2.0)
- Shibboleth and Azure AD interoperability
- LDAP integration with IdP
- Attribute resolution and release policies
- Realistic lab simulation using `.edu` domains

---


## 🧭 Architecture Diagram

![Architecture Diagram](docs/m365-sso-architecture-diagram.png)

➡️ [View Full Walkthrough](docs/walkthrough.md)


## 🛠️ Skills Acquired

- Configuring SAML-based SSO using Shibboleth and Microsoft Entra ID
- Mapping and filtering attributes in Shibboleth IdP
- Integrating LDAP (OpenLDAP) with identity providers
- Building and managing SAML metadata for IdP and SP
- Troubleshooting SSO flows using tools like SAML-tracer
- Designing a federated identity architecture in a simulated university environment

---

## 📘 Lessons Learned

- Microsoft 365 SAML integration expects specific attributes like `userPrincipalName`, which must be mapped correctly.
- Shibboleth IdP requires careful metadata management and endpoint alignment for Azure AD trust.
- Testing SAML SSO flows using tools like SAML-tracer helps visualize the entire authentication process.
- Ensuring correct attribute release is key to a successful login flow.
- LDAP directory structure directly impacts attribute resolution and SSO success.

---

## 💡 Recommendations

- Always validate both SP and IdP metadata before enabling SSO in production.
- Use Azure AD logs to troubleshoot missing or malformed attributes during federation.
- Maintain backups of IdP configurations and metadata files.
- Test with different user types to confirm consistent attribute resolution and release.
- Keep your IdP software and trust settings updated regularly.

---

## 🏷️ Tags

`IAM` `SSO` `Shibboleth` `Microsoft365` `AzureAD` `LDAP` `OpenLDAP` `SAML` `Federation` `Cybersecurity` `HigherEd` `EntraID`

---

© 2025 Richie — Created as part of an IAM portfolio to demonstrate identity federation and enterprise SSO capabilities.
