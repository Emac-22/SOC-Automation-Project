# Step-by-Step SOC Automation Project Guide

## Step 1: Design the Architecture
### Create a Logical Diagram:
- Use a tool like Draw.io to design a logical architecture for the SOC environment.
- Include the essential components: a Windows client, Wazuh server, TheHive, Shuffle, cloud environment, and SOC analyst endpoint.
- Establish directional data flow to illustrate interactions among these components, providing a visual reference for the subsequent steps.

## Step 2: Set Up Virtual Machines (VMs)
### Windows 10 Machine:
- Download and install VirtualBox or similar virtualization software.
- Create a Windows 10 VM, ensuring it’s configured for system monitoring.
- Install Sysmon on this VM to capture and log system-level events.

### Wazuh Server:
- Create a cloud instance, such as a DigitalOcean droplet, using an Ubuntu 22.04 image for the Wazuh server.
- Configure network security by setting up firewall rules, allowing access only to specific IP addresses, for secure monitoring.


## Step 3: Configure TheHive and Wazuh Servers
### Set Up TheHive:

- Configure Cassandra database settings in TheHive’s configuration, including cluster names and host addresses.
- Set up Elasticsearch settings for data storage and retrieval.
- Adjust TheHive’s configuration file to update paths and directory permissions as needed.

### Set Up Wazuh:

- Access the Wazuh dashboard to configure agents for client connections.
- Install the Wazuh agent on the Windows 10 VM and connect it to the Wazuh server, allowing for real-time event monitoring.

## Step 4: Configure Telemetry Data Collection
### Set Up Wazuh to Receive Sysmon Logs:

- Modify the Wazuh configuration file (ossec.conf) to enable collection of Sysmon logs from the Windows endpoint.
- Customize configuration to ensure only essential telemetry data is collected, streamlining processing.

### Simulate Suspicious Activity with Mimikatz:

- Adjust Windows Defender and security settings to permit the download of Mimikatz, a post-exploitation tool.
- Run Mimikatz in PowerShell as an administrator to simulate real-world threat behavior and generate telemetry for detection testing.

### Verify Detection of Mimikatz Events in Wazuh:

- Confirm that Wazuh logs Mimikatz-related activities by creating a custom rule in Wazuh to detect and flag these events.
- Use Filebeat to archive logs in Wazuh for tracking and analysis.

## Step 5: Automate Workflows with Shuffle.io
### Set Up Integration with Wazuh and TheHive:

- Create a Shuffle.io account and configure a workflow to automate incident detection and response.
- Set up a webhook in Shuffle to receive alerts from Wazuh and link it to TheHive for incident management.

### Build Mimikatz Detection Workflow:

- Develop a workflow in Shuffle to process Mimikatz detection alerts. The workflow should:
--- Extract key information, such as the file hash, and check it against a threat intelligence source like VirusTotal.
--- Route the alert to TheHive for case creation and notify an analyst via email.

### Validate Automation Workflow:

- Test the Shuffle workflow by generating a Wazuh alert and confirming that Shuffle correctly logs the event in TheHive.
- Ensure the workflow triggers the appropriate notifications to the designated security analyst, validating end-to-end automation.

## Final Review and Testing
### Conduct End-to-End Testing:
- Run additional suspicious activity simulations to verify the accuracy and reliability of detection in Wazuh, case creation in TheHive, and automated workflows in Shuffle.

### Document the Environment:
- Capture screenshots and document settings for each configuration step, from VM creation to workflow integration, for future reference and troubleshooting.
