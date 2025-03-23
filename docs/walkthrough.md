# RichTech University – Microsoft 365 SAML SSO Integration

This project demonstrates how to configure a Shibboleth Identity Provider (IdP) at RichTech University to integrate with Microsoft 365 (Azure AD) using SAML 2.0 for secure Single Sign-On (SSO).

---

## 🧭 Overview

- **Identity Provider (IdP):** Shibboleth IdP 4.x on Ubuntu Server
- **Service Provider (SP):** Microsoft 365 (Azure Active Directory / Entra ID)
- **Directory Service:** OpenLDAP (as local user store)
- **Use Case:** Authenticate RichTech University users into Microsoft 365 apps like Outlook, Teams, and OneDrive using their campus credentials.
- **Environment:** Simulated lab on VMware Workstation with self-signed certs

---

## 🖥️ Lab Setup

| VM | Hostname                          | Purpose                     |
|----|-----------------------------------|-----------------------------|
| VM1| idp.richtechuniversity.edu        | Shibboleth IdP              |
| VM2| ldap.richtechuniversity.edu      | OpenLDAP Server             |

- Bridged networking used
- Self-signed SSL certificates enabled for secure HTTPS communication

---

## 🔧 Configuration Steps

### 1. OpenLDAP (Directory Server)

- Install OpenLDAP:

```bash
sudo apt install slapd ldap-utils
```

- Reconfigure base DN:

```bash
sudo dpkg-reconfigure slapd
# Base DN: dc=richtetchuniversity,dc=org
```

- Add sample users using `docs/users.ldif`.

---

### 2. Shibboleth IdP Installation

- Install Java and unzip Shibboleth:

```bash
sudo apt install openjdk-11-jdk unzip
wget https://shibboleth.net/downloads/identity-provider/latest/shibboleth-identity-provider-4.x.x.tar.gz
```

- Run the installer and follow prompts to configure the IdP.

- Set the entityID:
```
https://idp.richtechuniversity.org/idp/shibboleth
```

- Configure LDAP connection in `ldap.properties`.

---

### 3. Azure AD (Microsoft 365) Setup

- In Azure Portal:
  - Register a new **Enterprise Application**
  - Set **SAML-based Sign-On**
  - Upload `microsoft365-idp.xml` as **IdP metadata**
  - Download Azure **SP metadata** and place in `metadata/sp-metadata.xml`

- Required attributes (set in Shibboleth):
  - `userPrincipalName`
  - `mail`
  - `givenName`
  - `sn`

---

### 4. Shibboleth IdP Configuration Files

- **idp.properties** – Defines base URLs and entityID
- **attribute-resolver.xml** – Maps LDAP attributes (e.g., uid → mail)
- **attribute-filter.xml** – Releases selected attributes to Microsoft 365
- **relying-party.xml** – Configures Microsoft 365 as a trusted relying party

---

## 🔐 Attribute Mapping

| SAML Attribute        | Source LDAP Attribute | Purpose              |
|-----------------------|------------------------|----------------------|
| `mail`                | `mail`                 | Email address        |
| `givenName`           | `givenName`            | First name           |
| `sn`                  | `sn`                   | Last name            |
| `userPrincipalName`   | `uid` + domain suffix  | Login ID for Azure   |

---

## 🧪 Testing Steps

1. Access Microsoft 365 app login
2. Redirect to `https://idp.richtechuniversity.edu/idp/profile/SAML2/Redirect/SSO`
3. Authenticate using OpenLDAP credentials
4. SAML assertion sent back to Microsoft
5. Verify login success and attribute consumption in Azure logs

---

## 📚 Official Documentation

- [Shibboleth IdP](https://shibboleth.atlassian.net/wiki/spaces/IDP5/)
- [Microsoft Entra SAML Docs](https://learn.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications)
- [OpenLDAP](https://www.openldap.org/doc/)
- [VMware Workstation](https://www.vmware.com/products/workstation-pro.html)

---

© 2025 Richie – Project built for IAM Systems Administrator portfolio.
