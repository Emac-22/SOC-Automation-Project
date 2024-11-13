# SOC-Automation-Project

## Executive Summary
The SOC Automation Project was developed to create a functional Security Operations Center (SOC) environment capable of automatically detecting, analyzing, and responding to security threats. By integrating open-source tools like Wazuh (SIEM and XDR), The Hive (case management), and Shuffle (SOAR for workflow automation), this project demonstrates how security processes can be streamlined to improve incident response times, reduce manual workload, and ensure a more resilient security
posture.

The automation workflows designed in this project enable the SOC to handle threats in realtime, leveraging integration between various components to detect and respond to suspicious activities effectively. This documentation provides a breakdown of the project setup, configuration steps, testing processes, and key insights for anyone looking to build a similar automated SOC environment.


## Introduction
### Background
Security operations centers play a crucial role in protecting organizations from cyber threats, but traditional SOCs often rely heavily on manual processes, leading to delays in threat detection and response. The goal of SOC automation is to reduce response times, minimize human error, and allow security analysts to focus on complex incidents by automating repetitive tasks.

### Objective
The primary goal of this project is to set up a comprehensive SOC environment that combines detection, case management, and automated response workflows. By implementing a range of open-source tools, this project seeks to demonstrate the benefits of automation in SOC operations, specifically in improving efficiency, accuracy, and overall threat management.

### Scope
The project utilizes Wazuh for security monitoring, The Hive for incident case management, and Shuffle for automating incident workflows. It focuses on configuring a system to detect, analyze, and respond to suspicious activities in a controlled environment, with specific attention to testing Mimikatz detections and implementing custom response workflows.


## Project Overview
### Architecture Design
The SOC Automation environment was architected with multiple components interacting seamlessly to facilitate threat detection and response. The architecture diagram (included in the appendix) provides a logical view of the system’s data flow, showing how alerts from monitored endpoints are processed by Wazuh, escalated to The Hive for case management, and routed through Shuffle for automated responses.

### Components
- Windows Client VM: Acts as the monitored endpoint, running Sysmon to generate system-level telemetry.
- Wazuh Server: Serves as the SIEM platform, collecting logs, analyzing them, and generating alerts based on predefined rules.
- The Hive: A case management tool where incidents are documented, assigned, and tracked.
- Shuffle: Automates the response workflows, connecting to Wazuh and The Hive to initiate actions based on alert criteria.

### Components Used
- Wazuh: An open-source SIEM and extended detection and response (XDR) platform, Wazuh is used for real-time security monitoring, intrusion detection, and data aggregation. It collects logs from the endpoint, detects anomalous behavior, and generates alerts.
- The Hive: This incident response and case management platform helps organize and track security incidents. It allows analysts to collaborate, manage alerts, and document investigation processes.
- Shuffle: As a security orchestration, automation, and response (SOAR) platform, Shuffle integrates with Wazuh and The Hive to automate alert-based actions and streamline incident response workflows.

### Methodology
- Designing the Architecture: Planning and diagramming the logical layout of components (Refer to Figure 1).
- Setting Up Virtual Machines: Establishing VMs for endpoint monitoring and deploying the Wazuh server.
- Configuring The Hive and Wazuh: Connecting Wazuh to The Hive for seamless alerting and case management (Refer to Figure 2).
- Generating and Configuring Telemetry: Creating logs with Sysmon on the endpoint and configuring Wazuh to receive and interpret these logs (Refer to Figure 3).
- Integrating Shuffle for Automation: Building workflows to automate detection and response processes using Shuffle (Refer to Figure 4).


## Testing and Validation
### Detecting Mimikatz Activity
After configuring Sysmon on the endpoint, we ran Mimikatz (a well-known post-exploitation tool) to simulate suspicious activity. Wazuh successfully detected this activity based on predefined rules and triggered an alert, which was routed to The Hive for case creation (Refer to Figure 5).

### Shuffle Workflow Validation
The Shuffle workflows were tested to verify that, upon receiving a Wazuh alert, they initiated the appropriate actions—logging the incident in The Hive and notifying analysts (Refer to Figure 6).

## Conclusion
The SOC Automation Project demonstrates the power of automation in security operations, enabling faster, more accurate incident response. By integrating Wazuh, The Hive, and Shuffle, we created a system that minimizes manual work for analysts and improves response times. Testing confirmed that the automated workflows detect and respond to simulated threats, validating the effectiveness of the system. This project highlights the importance of SOC automation in maintaining a strong cybersecurity posture and offers a template for implementing similar solutions in other environments.

### Key Takeaways
- SOC automation can significantly reduce response times and improve efficiency
- Open-source tools like Wazuh, The Hive, and Shuffle provide robust functionality for detecting, managing, and responding to threats.
- Automation allows SOC analysts to focus on higher-level tasks, improving overall security management.



## Figures

#Figure 1.
This diagram illustrates the logical layout of the components involved in the SOC Automation project. It
visualizes the flow of data between key components such as the Windows client, Wazuh manager, The
Hive, Shuffle, and the SOC analyst. The diagram is essential for understanding the project’s architecture
and serves as a blueprint for the subsequent setup and integration steps.


<img width="330" alt="LS9" src="https://github.com/user-attachments/assets/610909e9-ccdf-4b49-b1e8-296e5aba1eaf">



#Figure 2.
This screenshot displays the Wazuh dashboard showing the droplets created for the Wazuh
server and TheHive server. The droplets are virtual machines (VMs) that have been set up to host the
Wazuh and TheHive platforms, which are integral to the SOC Automation project. The configuration of
these droplets allows for the management and monitoring of security events, enabling effective incident
response and automation workflows.


<img width="929" alt="LS8" src="https://github.com/user-attachments/assets/7508e216-b537-4d1d-9dbb-d2c5b5e8a45a">


#Figure 3.
This screenshot shows the execution of the Mimikatz command in PowerShell with
administrative privileges. Mimikatz is used here to simulate a security event, which is then captured by
Wazuh for telemetry configuration. The command demonstrates the process of generating test events to
help validate the functionality of the Wazuh platform’s detection capabilities for specific threats, such as
credential dumping. This step is crucial in configuring and fine-tuning the telemetry within the SOC
automation workflow.


<img width="450" alt="LS6" src="https://github.com/user-attachments/assets/7db1b387-6294-4c61-82df-0b63d513cdbe">

#Figure 4.
This screenshot showcases the workflow built in Shuffle.io for automating the detection and
response processes. The workflow integrates Wazuh alerts with The Hive, enabling automated responses
when a threat is detected. In this case, the workflow specifically handles Mimikatz detection, extracting
file hashes and checking their reputation on VirusTotal, before sending the data to The Hive for further
case management. This step demonstrates how Shuffle.io is utilized to streamline incident response and
automate security processes within the SOC environment.


<img width="895" alt="LS2" src="https://github.com/user-attachments/assets/45218820-8f00-4c80-995a-913fa6d23777">


#Figures 5.
This screenshot illustrates the alert that was automatically created in The Hive dashboard as
part of the Shuffle workflow integration. Upon detecting Mimikatz activity on the endpoint—simulated
by running Mimikatz in PowerShell as part of the test—Wazuh triggered an alert. This alert was then
routed to The Hive, where a case was automatically generated for further investigation and response.
This process demonstrates the seamless integration of Wazuh, Shuffle, and The Hive for automated
incident management in the SOC environment.


<img width="954" alt="LS4" src="https://github.com/user-attachments/assets/64624018-31ee-4c9f-b2b7-755a147095db">



#Figure 6.
This screenshot demonstrates the email notification sent to analysts as part of the Shuffle
workflow. Upon receiving a Wazuh alert, the Shuffle automation workflow not only logged the incident
in The Hive but also triggered an email notification to the designated analyst team. This step validates
the integration of Shuffle in automating response actions, ensuring that analysts are promptly notified of
security events for faster incident handling and response.


<img width="484" alt="LS3" src="https://github.com/user-attachments/assets/00f2cde8-7f75-440b-84ba-056bf3977760">






























