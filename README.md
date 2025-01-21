# Home Lab Configuration: Advanced Network Management and Security

This home lab setup showcases my expertise in advanced network management and cybersecurity practices. By utilizing pfSense, VLANs, managed switches, SIEM integration, and secure remote access via a travel router and VPN, I have built a robust and secure environment that supports a wide range of network activities while ensuring optimal performance and security. This project highlights my ability to design, implement, and manage complex network infrastructures, making me well-prepared for roles in network management and cybersecurity.

![My Network](https://github.com/BrandonRoos/Home-Lab/assets/28285286/5f763551-966a-4570-b032-2314acaba761)

## Firewall: pfSense and VLANs
[![pfSense](https://img.shields.io/badge/pfSense-Website-blue)](https://www.pfsense.org/)

At the core of my network is a **pfSense firewall**, a powerful open-source solution that provides advanced security, routing, and VPN capabilities. The pfSense setup is integrated with VLAN configurations to ensure segmented and secure communication across different parts of the network. This allows precise control of traffic flow, ensuring each VLAN operates within its designated boundaries for enhanced security.

## Managed Switch: VLAN Segmentation

To optimize network management, I’ve implemented a managed switch with three distinct VLANs:

- **VLAN 1:** The default network for general traffic and device communication.
- **VLAN 2:** Dedicated to network media, ensuring that streaming and media devices operate on a separate, optimized network.
- **VLAN 3:** Specifically designed for the test bench, completely isolated from other network devices to prevent unintended interactions or security breaches.

This segmentation enables structured and secure traffic management, ensuring that different types of traffic are effectively isolated and controlled.

## Test Bench: Secure Isolation

The **test bench** is configured on VLAN 3, ensuring it remains fully isolated from other devices on the network. This isolation is critical for testing new configurations, updates, or software without affecting the stability and security of the network. It provides a controlled environment for experimentation and refinement before deployment across the entire infrastructure.

## Network Media: Dedicated VLAN

**Network media devices** are assigned to VLAN 2, ensuring that media streaming does not interfere with other network operations. This dedicated VLAN optimizes bandwidth usage and provides a smooth, uninterrupted experience, while maintaining high performance for critical tasks on other VLANs.

## SIEM: Wazuh
[![Wazuh](https://img.shields.io/badge/Wazuh-Website-blue)](https://wazuh.com/)


I have deployed **Wazuh** as my Security Information and Event Management (SIEM) solution for comprehensive security monitoring. Wazuh continuously monitors the network for potential threats and anomalies, providing real-time analysis and alerts. Additionally, I’ve integrated Wazuh with Discord for instant notifications if any devices or services experience downtime. This setup allows for rapid issue resolution and minimizes downtime.

## Wireless Access Point

The **wireless access point** extends seamless connectivity to wireless devices while maintaining security and performance standards. It supports multiple SSIDs, each mapped to a specific VLAN, ensuring wireless traffic is properly segmented and managed in line with the overall network design.

## Travel Router with VPN

I use a **travel router** that connects to my home network via a VPN, allowing secure access to my resources from anywhere. This setup ensures my data is protected when using public or untrusted internet connections. Routing all traffic through the VPN allows me to securely access my home network and media, no matter where I am.

## DNS: Secure and Privacy-Focused with Quad9

[![Quad9](https://img.shields.io/badge/Quad9-Website-blue)](https://quad9.net/) 

For DNS resolution on port 53, I leverage **Quad9** servers for both IPv4 and IPv6 :

- **IPv4:** `9.9.9.9` and `149.112.112.112`
- **IPv6:** `2620:fe::fe` and `2620:fe::9`

**Quad9** is a free DNS service focusing on security, privacy, and performance by blocking access to known malicious domains using threat intelligence from various cybersecurity partners. Key benefits include:

### Cybersecurity Benefits of Quad9:

- **Malware Blocking:** Quad9 automatically blocks domains known for distributing malware, phishing, and botnets, reducing the risk of cyberattacks.
  
- **Privacy-Focused:** Unlike many public DNS providers, Quad9 does not store personally identifiable information (PII), ensuring my browsing activity remains private.
  
- **Global Threat Intelligence:** Quad9 integrates threat intelligence from over 19 cybersecurity organizations, offering real-time protection against emerging threats.
  
- **Resilient Network:** With globally distributed infrastructure, Quad9 provides high availability and redundancy, ensuring fast and reliable DNS resolution even under heavy traffic or network disruptions.

By integrating Quad9 DNS into my home lab, I enhance overall network security and proactively block malicious domains, keeping my environment safe.

## Coming Soon

### Virtualizing My Firewall

I’m currently working on **virtualizing my firewall** to enhance testing and rollback capabilities. This will allow me to:

- Test new configurations and updates in a virtual environment without affecting my live network.
- Roll back to previous versions quickly and easily, minimizing downtime in case of issues.
- Clone my firewall setup for rapid testing and deployment of new configurations or troubleshooting scenarios.

### Add WireGuard
[![WireGuard Documentation](https://img.shields.io/badge/WireGuard-Documentation-blue)](https://docs.netgate.com/pfsense/en/latest/vpn/wireguard/index.html)



Stay tuned for more updates on this project!


  


