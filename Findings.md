## Reconnaissance 

Using *nmap's* ping-sweep capabilities, a network topology was encountered with the following characteristics:

##### CHART

This report will involve further investigation into the security of the Target 1 machine at 192.168.1.110.

A SYN scan on Target 1 revealed a website on port 80 and an rpc service on port 111, among other services.

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Target_1_Nmap_Results.png "Target_1_Nmap_Results")

To learn more about the website a *dirb* scan was conducted. 
This revealed a wordpress service:

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Target_1_Dirb_Results.png "Target_1_Dirb_Results")

## Exploitation

A *wpscan* was used to gather more information on the wordpress service. 
This revealed several usernames: 

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Target_1_Wpscan_Results.png "Target_1_Wpscan_Results")

The discovered usernames allowed a focused brute-force attempt using the publicly-available *Hydra* tool.
Michael's password was successsfully revealed as shown below. 
Note: Steven's credentials were not cracked under a specified time frame.

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Successful_Hydra_Attack_On_Michael.png "Successful_Hydra_Attack_On_Michael")

Accessing Michael's account revealed a vulnerable mysql database. 
Credentials for the wordpress database were disovered in plain text. 

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Wordpress_Login_Credentials.png "Wordpress_Login_Credentials")

Acessing the mysql database revealead a chart with username and password hashes. 
In particular the password hash of Steven, a known account username, was available.

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Exposed_Wordpress_Hashes.png "Exposed_Wordpress_Hashes")

Steven's password was processed using *john*, a publicly available hash cracking tool, which revealed his password as "linux4u".
Examining Steven's account and privileges revealed python sudo access privileges, which was used to elevate to root, using a python vulnerability.

![alt-text](https://github.com/Travis-Dominguez/Attacking_a_Vulnerable_Network/blob/main/Images/Steven_Account_Access.png "Steven_Account_Access")













 

