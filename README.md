# Omnissa Horizon SAML Tool

The **Omnissa Horizon SAML Tool** is a specialized utility for administrators of Omnissa Horizon environments. It simplifies the configuration of SAML Service Provider (SP) metadata and certificate lifetimes by providing a graphical interface to modify LDAP attributes, eliminating the need for manual edits via ADSI Edit.

## 🌟 Key Features

* **Intelligent LDAP Path Detection**: The tool automatically discovers and connects to the correct LDAP path, supporting both legacy and modern Omnissa structures:
    * `DC=vdi,dc=vmware,dc=int`
    * `DC=vdi,DC=horizon,DC=internal`
* **Version Awareness**: The tool queries the Windows Registry to identify the installed "Omnissa Horizon Connection Server" version. Advanced features, such as SAML Key Sharing Version 3, are conditionally enabled only if Horizon 2512 (minimum version `8.17.0.20167542520`) or later is detected.
* **SAML Metadata Sharing Configuration**: Easily manage the `pae-SAMLKeySharingEnabled` attribute:
    * **UNSET (Delete)**: Removes the sharing configuration.
    * **Version 1**: For Horizon 2503 and later.
    * **Version 3**: For Horizon 2512 and later, enabling shared Entity IDs and ACS URLs across the pod.
* **Certificate Validity Management**: Directly set the expiration period (in days) for SAML Encryption and Signing keys via the `pae-NameValuePair` property.

## 🚀 How to Use

1.  **Run as Administrator**: The tool requires elevated privileges to access the local LDAP service (Port 389) and read registry keys on your Connection Server.
2.  **Local Execution Required**: This tool **must** be run directly on one of the Connection Servers within your Horizon farm to establish a connection to the local LDAP instance (`localhost:389`).
3.  **Verify Status**: Upon startup, the status bar displays the detected LDAP path and current saved state.
4.  **Adjust Configuration**:
    * Select the **Metadata Sharing Version** appropriate for your Horizon build.
    * Define the **Validity Days** (1–9999) for your keys or choose **Delete (UNSET)** to revert to default values.
5.  **Save Changes**: Click **Apply Config** to commit the updates to the Horizon Global Properties.

## 🛠 Technical Specifications

* **Target Framework**: .NET Framework 4.8.
* **Security**: Uses `Signing`, `Sealing`, and `Secure` authentication types for LDAP directory entries.
* **Registry Monitoring**: Scans `SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` for Connection Server metadata.

## 📖 References & Documentation

* [Omnissa: Enabling Common Service Provider Metadata](https://docs.omnissa.com/bundle/Horizon-AdministrationV2512/page/EnablingCommonServiceProviderMetadatainConnectionServers.html)
* [Omnissa: Change the Expiration Period for Service Provider Metadata](https://docs.omnissa.com/bundle/Horizon-AdministrationV2512/page/ChangetheExpirationPeriodforServiceProviderMetadataonConnectionServer.html)

---
**Developer**: Stefan Gourguis  
**Blog**: [https://blog.vmguru.io](https://blog.vmguru.io)  
**Contact**: stg78@outlook.de
