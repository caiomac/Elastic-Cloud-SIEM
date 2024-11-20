<h1>Elastic SIEM Setup and Monitoring </h1>

<h2>Description</h2>
This project involves setting up an Elastic SIEM instance to monitor security events. It starts by creating an Elastic Cloud deployment and configuring a Kali Linux virtual machine in Oracle VirtualBox. Logs are collected using the Elastic Agent installed on the VM, forwarding data to the SIEM. Security events, such as those generated by Nmap scans, are analyzed using queries in Elastic SIEM. Custom dashboards and visualizations are created to display patterns over time, and alerts are configured to notify of specific events, such as Nmap scans, via email.
<br/>
<br/>
<i>Estimated completion time: 2 hours</i>
<br/>
<br/>

<h2>Objectives</h2>
The objective of this lab is to provide a practical learning experience in setting up and utilizing Elastic SIEM for security monitoring and incident detection. By creating an Elastic Cloud deployment and configuring a Kali Linux virtual machine, the lab aims to teach skills such as cloud deployment, log collection, and SIEM integration. I learnt to generate and analyze security events, create visual dashboards to identify patterns, and configure alerts for real-time notifications of specific activities, such as Nmap scans, to simulate real-world cybersecurity scenarios.

<h2>Skills learned</h2>

- Cloud Deployment <br />
- Virtualization <br />
- Log Collection and Integration <br />
- Dashboard creation <br />
- Alert configuration <br />
- SIEM operations <br />


<h2>Tools Used </h2>

- Elastic Cloud: For deploying and managing the Elastic SIEM instance.<br />
- Elastic Agent: For collecting and forwarding logs to the SIEM.<br />
- Kali Linux: As the virtual machine for generating and testing security events.<br />
- Oracle VirtualBox: For setting up and running the Kali Linux VM.<br />
- Nmap: For generating security events through network scanning.<br />
- Linux Terminal (Command Line): For configuring the VM, installing Elastic Agent, and running security tools like Nmap.<br />
- Email Services: For receiving notifications triggered by configured alerts in Elastic SIEM.<br />


<h2>Program walk-through:</h2>

<h3>Step 1 - Setting up an Elastic Account:</h3> 
Before starting, I needed to create a free account to set up a cloud Elastic instance that I could run the SIEM on. To do that, I signed up for a free trial to use Elastic Cloud at <i>https://cloud.elastic.co/registration</i>. Once I had an Elastic account, I logged in to the Elastic Cloud console at <i>https://cloud.elastic.co.</i>, clicked on the <b>Create Deployment</b> button and selected <b>Elasticsearch</b> as the deployment type. I chose a region and deployment size that fitted my needs and clicked on <b>Create Deployment</b>. After it was set, environment is ready to be used.
<br/> 
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/20396965-8295-479d-9326-9bbe21ec51b9" width="700">
</div>
<br/> 
<br/> 
<h3>Step 2 - Setting up the Linux VM:</h3>  
<br/>
Next, I needed to set up the Linux VM. I used Kali Linux and Oracle VirtualBox. I started by downloading the Kali Linux VM from the official Kali website at <i>https://www.kali.org/get-kali/#kali-virtual-machines</i>. I create a new VM with the Kali VM file in VirtualBox. 
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/2ec10b85-a65c-47ef-8372-69ae98f1f9d7" width="600">
</div>
<br/>
I started the VM and followed the on-screen prompts to install Kali. Once the installation was complete, I logged in to the Kali VM using the credentials <b>kali</b> for both the username and password.
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/57c99b1d-35b1-41eb-8fce-467827617ab3" width="750">
</div>
<br/> 
<br/> 
<h3>Step 3 - Setting up the Agent to Collect Logs:</h3>
An agent is a software program that is installed on a device, such as a server or endpoint, to collect and send data to a centralized system for analysis and monitoring. In the context of Elastic SIEM, an agent was used to collect and forward security-related events from endpoints to Elastic SIEM instance.
<br />
<br />
To set up the agent to collect logs from Kali VM and forward them to the Elastic SIEM instance, I logged in to the Elastic SIEM instance and navigate to the Integrations page by: clicking on the Kibana main menu bar at the top left, then selecting <b>Integrations</b> at the bottom.
<br />
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/a1ccceef-9fbb-4cf3-8df7-20ef20fea187" width="250">
</div>
<br />
I searched for <b>Elastic Defend</b> and clicked on it to open the integration page:
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/013af2f5-fdb0-4da5-903a-b846969fb87c" width="500">
</div>
<br />
I clicked on <b>Install Elastic Defend</b> and followed the instructions provided on the integration page to install the agent on your Kali VM.
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/fdae443e-364b-4c9b-a1eb-67a05e40d44d" width="500">
</div>
<br />
I selected <b>Linux Tar</b> and then copied that command to clipboard and pasted it into the Kali terminal (command line).
<br/>
<br/>
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/ea738dee-fc01-4ebc-9e6c-897378168d63" width="400">
</div>
<br />
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/8ea87400-5f7d-4f3f-94aa-24253847a56f" width="400">
</div>
<br />
Once the agent was installed, a message that says “Elastic Agent has been successfully installed.” was prompted and it automatically started collecting and forwarding logs to the Elastic SIEM instance.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/b1be7dc1-47e4-489f-8616-cc968e4c16a5" width="400">
</div>
<br />
I verified that the agent has been installed correctly by running the command: sudo systemctl status elastic-agent.service.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/0e60e463-42e1-4247-8dfb-5f4d52f54148" width="400">
</div>
<br/> 
<br/> 
<h3>Step 4 - Generating Security Events on the Kali VM</h3>
To verify that the agent is working correctly, I generated some security-related events on the Kali VM. To do this, I used a tool like Nmap. Nmap (Network Mapper) is a free and open-source utility used for network exploration, management, and security auditing. It is designed to discover hosts and services on a computer network, thus creating a “map” of the network. Nmap can be used to scan hosts for open ports, determine the operating system and software running on the target system, and gather other information about the network.
<br />
<br />
To run an Nmap scan, it’s just necessary to run the command: sudo nmap <ip address>. 
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/e961c859-329e-41af-8f52-7d190baa81ab" width="400">
</div>
An Nmap scan of my host machine.
<br />
<br />
This scan can generate several security events, such as the detection of open ports and the identification of services running on those ports. 
<br/> 
<br/> 
<h3>Step 5 - Querying for Security Events in the Elastic SIEM</h3>
Once I was able to forward data from the Kali VM to the SIEM, I could start querying and analyzing the logs in the SIEM.
<br />
<br />
To do this, inside your Elastic Deployment, I clicked on the menu icon at the top-left with the three horizontal lines and then click on the <b>Logs</b> tab under <b>Observability</b> to view the logs from the Kali VM.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/df587710-79a3-455d-b7f4-2218d327dfc4" width="250">
</div>
<br />
In the search bar, I entered a search query to filter the logs. For example, to search for all logs related to Nmap scans, I entered the query: event.action: “nmap_scan” or process.args: “sudo”
<br />
<br />
I clicked on the “Search” button to execute the search query. The results of the search query was displayed in the table. To view details I clicked the three dots next to each event.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/0f4ee79c-f068-4552-aa34-601d77dcd119" width="500">
</div>
<br />
By generating and analyzing different types of security events in Elastic SIEM like the one above, or generating authentication failures by typing in the wrong password for a user or attempting SSH logins an incorrect password, I could gain a better understanding of how security incidents are detected, investigated, and responded to in real-world environments.
<br/> 
<br/> 
<h3>Step 6 - Creating a Dashboard to Visualize the Events</h3>
I also used the visualizations and dashboards in the SIEM app to analyze the logs and identify patterns or anomalies in the data. I created a simple dashboard that shows a count of security events over time.
<br />
<br />
To do it, I navigate to the Elastic web portal at <i>https://cloud.elastic.co/</i>, clicked on the menu icon on the top-left, then under <b>Analytics</b>, I clicked on <b>Dashboards</b>.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/bf908a2d-c742-450a-af79-321e6319935d" width="250">
</div>
<br />
I then clicked on the <b>Create dashboard</b> button on the top right to create a new dashboard.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/a1df5100-283c-4c14-b55f-bf1402ad07ce" width="500">
</div>
<br />
I clicked on the <b>Create Visualization</b> button to add a new visualization to the dashboard.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/f0264eee-94b0-4ccf-8f69-35c112bffeb4" width="500">
</div>
<br />
I selected <b>Area</b> as the visualization type, which would create a chart that shows the count of events over time.
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/6cffe27a-7512-402c-8e8a-2179cbb3b548" width="250">
</div>
<br />
In the <b>Metrics</b> section of the visualization editor on the right, I selected <b>Count</b> as the vertical field type and <b>Timestamp</b> for the horizontal field. This would show the count of events over time.
<br />
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/c1287182-c10d-4a2f-83d1-3cd914a0854c" width="300">
</div>
<br />
I clicked on the <b>Save</b> button to save the visualization and then completed the rest of the settings. In the end I had the dashboard below (which had no records because no nmap command was ran in the VM after the chart was created):
<br />
<br />
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/92da5703-17da-4a8b-bc2e-e32bacd2c08a" width="500">
</div>
<br/> 
<br/> 
<h3>Step 7 - Creating an Alert</h3>
In a SIEM, alerts are a crucial feature for detecting security incidents and responding to them in a timely manner. Alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when certain conditions are met. In this step, I walked through the steps of creating an alert in the Elastic SIEM instance to detect Nmap scans then notify me through email when they are detected.
<br />
<br />
Firstly, I clicked on the menu icon on the top-left, then under <b>Security</b>, clicked on <b>Alerts</b>. Then I clicked on <b>Manage rules</b> at the top right.
<br />
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/8077caee-0f22-4330-bf62-517f434fd5aa" width="500">
</div>
<br />
Then I clicked on the <b>Create new rule</b> button at the top right.
<br />
<br />
Under the <b>Define rule</b> section, I selected the <b>Custom query</b> option from the dropdown menu and set the conditions for the rule. I used the following query to detect Nmap scan events. This query will match all events with the action <i><b>nmap</b></i>.
<br/>
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/8279c443-92b0-4ae5-b7c8-ac124f30c462" width="500">
</div>
<br />
<br />
I clicked <b>Continue</b> and under <b>About rule</b>, I gave the rule a name and a description.
<br/>
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/156dad86-5bd3-440e-966c-4db1261540fc" width="500">
</div>
<br />
I set the severity level for the alert, which helps to prioritize alerts based on their importance. I kept all the other default settings under <b>Schedule rule</b> and clicked <b>Continue</b>.
<br/> 
In the <b>Actions</b> section, I select the action I wanted to be taken when the rule is triggered which was send an email to <i><b>caiomacedo55@gmail.com</b></i>.
<br />
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/77792548-ed67-430a-a558-65b8a159df80" width="500">
</div>
<br />
Finally, I clicked the <b>Create and enable rule</b> button to create the alert.
<br />
<br />
Once I’ve created the alert, it would monitor the logs for Nmap scan events. If an Nmap scan event was detected, the alert would be triggered and the e-mail would be sent. 
<br />
<br/> 
<div style="text-align: center;">
  <img src="https://github.com/user-attachments/assets/12fe4d17-378e-4f86-a4a3-9442a13cd59d" width="500">
</div>
<br />

<h2>Summary</h2>
I successfully completed the setup and configuration of an Elastic SIEM instance to collect, monitor, and analyze security events from a Kali Linux virtual machine. Throughout the process, I created an Elastic Cloud deployment, configured a Linux VM, installed the Elastic Agent to forward logs, generated and queried security events using tools like Nmap, and visualized these events using custom dashboards. Additionally, I implemented an alert system that detects Nmap scans and sends email notifications, ensuring a comprehensive understanding of security monitoring and incident response workflows.


  <!--
 ```diff
