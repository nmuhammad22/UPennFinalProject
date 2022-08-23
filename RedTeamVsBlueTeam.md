# Red Team: Summary of Operations

## Table of Contents
- Exposed Services
- Critical Vulnerabilities
- Exploitation

### Exposed Services
Nmap scan results for each machine reveal the below services and OS details:

```bash
$ nmap ... #nmap 192.168.1.0/24 -sV
```

![nmapfinal1](https://user-images.githubusercontent.com/97314199/186032100-fe3e3961-b730-479a-a2c7-8b1038b59859.png)

![nmapfinal2](https://user-images.githubusercontent.com/97314199/186032272-bf6b8815-541e-4e3a-8bc1-e6fb5002e957.png)

This scan identifies the services below as potential points of entry:
- Target 1
  - Port 22 - Open SSH
  - Port 80 - Open HTTP

The following vulnerabilities were identified on each target:
- Target 1
  - CVE-2019-15653 HTML Password Hash Disclosure
  - CVE-2018-1000030 Python Privilege Escalation
  - CVE-2021-28041 SSH Remote Login
  - CVE-2017-7760 Exposed Username And Weak Password
  - CVE-2018-1000030 Python Privilege Escalation

### Exploitation

The Red Team was able to penetrate `Target 1` and retrieve the following confidential data:
- Target 1
  - `flag1.txt`: b9bbcb33e11b80be759c4e844862482d
    - **Exploit Used** 
      - HTML Password Hash Disclosure 
      - wpscan --url http://192.168.1.110/wordpress -eu

![Attacking - 3(flagcapture)](https://user-images.githubusercontent.com/97314199/186032444-387f748c-2cb3-4569-b523-ecc6abedf85f.png)

 - `flag2.txt`: fc3fd58dcdad9ab23faca6e9a36e581c
    - **Exploit Used**
      - Open SSH Exploit/ SSH Remote Login
      - wpscan --url http://192.168.1.110/wordpress -eu 

![Attacking - 3(wpscan)](https://user-images.githubusercontent.com/97314199/186032615-30ea1cd1-1a94-4899-8737-1172a698d90a.png)

![Attacking - 4(sshentry)](https://user-images.githubusercontent.com/97314199/186032858-758c2c3f-5df1-4629-bdc4-6aab03371c85.png)

![Attacking - 4(flag1)](https://user-images.githubusercontent.com/97314199/186032934-c7482f7a-9305-40c7-b7b2-f3d10417a24d.png)

- `flag3.txt`: afc01ab56b5059e7dccf93122770cd2
    - **Exploit Used**
      - SSH Remote Login
      - ssh michael@192.168.1.110/ steven@localhost

![Attacking - 7(pink84)](https://user-images.githubusercontent.com/97314199/186033142-70ebc1b2-180c-41b9-9125-5f2448f9209c.png)

- `flag4.txt`: 715dea6c055b9fe3337544932f2941ce
    - **Exploit Used**
      - Python Privilege Escalation
      - sudo python -c ‘import pty;pty.spawn(“bin/bash”);’

![Attacking - 9(FinalFlag)](https://user-images.githubusercontent.com/97314199/186033805-fb38d15c-d895-4888-8d04-657b299f6e4c.png)








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
  - **Operating System**: Windows
  - **Purpose**: Connection to Host VMs
  - **IP Address**: 192.168.1.1(10.0.0.8)
- ELK
  - **Operating System**: Ubuntu
  - **Purpose**: Helps to view alerts and reports 
  - **IP Address**: 192.168.1.100
- Kali
  - **Operating System**: Debian Kali
  - **Purpose**: Used as Attack VM
  - **IP Address**: 192.168.1.90
- Target 1
  - **Operating System**: Linux
  - **Purpose**: Used to host vulnerable wordpress 
  - **IP Address**: 192.168.1.110
- Target 2
  - **Operating System**: Linux
  - **Purpose**: Optional Attack Target
  - **IP Address**: 192.168.1.115
- Capstone
  - **Operating System**: Linux
  - **Purpose**: Testing alerts and logs from the ELK VM
  - **IP Address**: 192.168.1.105


### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

#### Excessive HTTP Errors Alert

Excessive HTTP Errors Alert is implemented as follows:
  - **Metric**: Top 5 HTTP status codes over 400 for the last 5 minutes.
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
  - **Metric**: CPU Usage Percentage over all documents.
  - **Threshold**: Over 0.5
  - **Vulnerability Mitigated**: Malicious Script
  - **Reliability**: Low Reliability

![CPU Usage Monitor Alert](https://user-images.githubusercontent.com/97314199/186034571-d526f2a2-f9bb-49ad-a9cb-d4cb32fe718d.png)



