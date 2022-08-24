# Blue Team: Summary of Operations


## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further


### Network Topology


The following machines were identified on the network:
- Azure
  - **Operating System**:Windows
  - **Purpose**: Connection to Host VMs
  - **IP Address**:192.168.1.1(10.0.0.8)
- ELK
  - **Operating System**: Ubuntu
  - **Purpose**: Helps to view alerts and reports 
  - **IP Address**:192.168.1.100
- Kali
  -**Operating System**:Debian Kali
  -**Purpose**: Used as Attack VM
  -**IP Address**:192.168.1.90
- Target 1
  -**Operating System**:Linux
  -**Purpose**: Used to host vulnerable wordpress 
  -**IP Address**: 192.168.1.110
-Target 2
  -**Operating System**: Linux
  -**Purpose**: Optional Attack Target
  -**IP Address**:192.168.1.115
-Capstone
  -**Operating System**: Linux
  -**Purpose**: Testing alerts and logs from the ELK VM
  -**IP Address**: 192.168.1.105




### Description of Targets


The target of this attack was: `Target 1` (192.168.1.110).


Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:


### Monitoring the Targets


Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:


#### Excessive HTTP Errors Alert
_TODO: Replace `Alert 1` with the name of the alert._


Excessive HTTP Errors Alert is implemented as follows:
  - **Metric**: TODO Top 5 HTTP status codes over 400 for the last 5 minutes.
  - **Threshold**: 400 for every 5 Minutes
  - **Vulnerability Mitigated**: Brute Force
  - **Reliability**: Medium to High reliability depending on the size of the company.


![Excessive HTTP Errors Alert](https://user-images.githubusercontent.com/97314199/186034369-c0595181-45f9-43f4-8b4e-a08774dc2650.png)




  



#### HTTP Request Size Monitor Alert
HTTP Request Size Monitor Alert is implemented as follows:
  - **Metric**: Total of all HTTP request bites on all documents over 3500 bites in the last minute.
  - **Threshold**: Over 3500 bites
  - **Vulnerability Mitigated**: Denial of Service Attacks
  - **Reliability**: High Reliability


![HTTP Request Size Monitor Alert (EDIT)](https://user-images.githubusercontent.com/97314199/186034496-cef7b664-7c7b-454b-acc0-d4a9412a77f7.png)




  



#### CPU Usage Monitor Alert
CPU Usage Monitor Alert is implemented as follows:
  - **Metric**: TODO CPU Usage Percentage over all documents.
  - **Threshold**: TODO Over 0.5
  - **Vulnerability Mitigated**: TODO Malicious Script
  - **Reliability**: Low Reliability


![CPU Usage Monitor Alert](https://user-images.githubusercontent.com/97314199/186034571-d526f2a2-f9bb-49ad-a9cb-d4cb32fe718d.png)