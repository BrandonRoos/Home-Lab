# Home Lab Configuration: Advanced Network Management and Security

This home lab setup demonstrates my proficiency in advanced network management and security practices. By leveraging pfSense, VLANs, managed switches, SIEM integration, and secure remote access via a travel router and VPN, I have created a robust and secure environment that supports various network activities while ensuring optimal performance and security. This experience highlights my ability to design, implement, and manage complex network infrastructures, making me well-suited for roles in network and cybersecurity.

![My Network](https://github.com/BrandonRoos/Home-Lab/assets/28285286/5f763551-966a-4570-b032-2314acaba761)



## Firewall: pfSense and VLANs

I have implemented a pfSense firewall at the core of my home lab network. This powerful open-source firewall provides robust security, advanced routing, and VPN capabilities. The pfSense setup is integrated with VLAN configurations to ensure segmented and secure communication across different network parts. This lets me control and manage traffic flow precisely, ensuring each VLAN operates within its designated boundaries.

## Managed Switch: VLAN Segmentation
To further enhance network management, I have incorporated a managed switch configured with three distinct VLANs:

-  **VLAN 1:** The default network for general traffic and device communication.
-  **VLAN 2:** Dedicated to network media, ensuring that streaming and media devices operate on a separate, optimized network.
-  **VLAN 3:**  Specifically designed for the test bench, completely isolated from other network devices to prevent unintended interactions or security breaches.

  This segmentation ensures that different types of traffic are effectively managed and isolated, providing a structured and secure network environment.

  ## Test Bench: Secure Isolation

  The test bench is configured on VLAN 3, ensuring it remains completely segregated from other devices on the network. This isolation is crucial for testing new configurations, updates, or software without risking the stability and security of the entire network. It provides a controlled environment where I can experiment and refine network setups before deploying them across the rest of the infrastructure.

  ## Network Media: Dedicated VLAN
 
  Network media devices are assigned to VLAN 2. This separation ensures that media streaming does not interfere with other network operations, providing a smooth and uninterrupted experience. By isolating media traffic, I can optimize bandwidth usage and maintain high performance for critical tasks on other VLANs.

  ## SIEM: Wazuh with Discord Alerts
  
I have deployed Wazuh as my Security Information and Event Management (SIEM) solution for comprehensive security monitoring. Wazuh continuously monitors the network for potential threats and anomalies, providing real-time analysis and alerting. Additionally, I have integrated Wazuh with Discord to receive instant notifications if any devices or services go down. This integration ensures that I am immediately aware of any issues, allowing for prompt resolution and minimizing downtime.

## Wireless Access Point

The wireless access point in my home lab ensures seamless connectivity for wireless devices, extending the network's reach while maintaining security and performance standards. The access point is configured to support multiple SSIDs, each mapped to a specific VLAN, ensuring wireless traffic is properly segmented and managed in line with the overall network design.

## Travel Router with VPN

I use a travel router that connects to my house via a VPN to maintain secure access to my home network while on the go. This setup allows me to securely access my media and other resources from anywhere, providing peace of mind when using potentially untrusted public internet connections. By routing all traffic through the VPN, I ensure that my data remains protected and my home network is accessible no matter where I am.

## Coming Soon

### Virtualizing My Firewall

I'm working on virtualizing my firewall to enhance testing and rollback capabilities. This will allow me to:

- Test new configurations and updates in a virtual environment without affecting my live network.
- Rollback to previous versions quickly and easily, ensuring minimal downtime in case of issues.
- Clone my firewall setup for rapid testing and deployment of new settings or troubleshooting scenarios.


Stay tuned for more updates on this project!

  


