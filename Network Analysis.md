Network Analysis
Time Thieves
At least two users on the network have been wasting time on YouTube. Usually, IT wouldn't pay much mind to this behavior, but it seems these people have created their own web server on the corporate network. So far, Security knows the following about these time thieves:
* They have set up an Active Directory network.
* They are constantly watching videos on YouTube.
* Their IP addresses are somewhere in the range 10.6.12.0/24.
You must inspect your traffic capture to answer the following questions:
1. What is the domain name of the users' custom site?
   1. frank-n-ted-dc.frank-n-ted.com


2. What is the IP address of the Domain Controller (DC) of the AD network?
   1. 10.6.12.12
![Wireshark - q2a](https://user-images.githubusercontent.com/97314199/186479786-3663f20c-fa57-42ff-b29d-08690103b3fd.png)
  

3. What is the name of the malware downloaded to the 10.6.12.203 machine? Once you have found the file, export it to your Kali machine's desktop.
![Wireshark - q3](https://user-images.githubusercontent.com/97314199/186479963-318f0da4-e64d-4ffc-9022-79381e27d4d5.png)
  

GET /files/june11.dll HTTP/1


4. Upload the file to VirusTotal.com. What kind of malware is this classified as?
![Wireshark - q4a](https://user-images.githubusercontent.com/97314199/186480101-dcb8f829-8cbb-40d6-bc52-0ad40b7efc43.png)
  

This would be classified as a Trojan.
Vulnerable Windows Machines
The Security team received reports of an infected Windows host on the network. They know the following:
* Machines in the network live in the range 172.16.4.0/24.
* The domain mind-hammer.net is associated with the infected computer.
* The DC for this network lives at 172.16.4.4 and is named Mind-Hammer-DC.
* The network has standard gateway and broadcast addresses.
Inspect your traffic to answer the following questions:
1. Find the following information about the infected Windows machine:
   * Host name: ROTTERDAM-PC
   * IP address: 172.16.4.205
   * MAC address: 00:59:07:b0:63:a4


2. What is the username of the Windows user whose computer is infected?
![Wireshark - 2](https://user-images.githubusercontent.com/97314199/186480268-9cd85c65-bee9-4050-b5ba-20f15db74ee1.png)
  

The username is matthijs.devries
3. What are the IP addresses used in the actual infection traffic?
![Screenshot 2022-08-22 162412](https://user-images.githubusercontent.com/97314199/186480424-061fcc6f-f22b-4741-b6a6-c479e6ad7713.png)
  

172.16.4.4
4. As a bonus, retrieve the desktop background of the Windows host.