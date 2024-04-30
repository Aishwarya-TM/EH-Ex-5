# Metasploit-for-reconnaissance
# Metasploit
Metasploit for reconnaissance in pentesting

# AIM:

To get introduced to Metasploit Framework and to  perform reconnaissance  in pentesting .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find out the ip address of the attackers system
## OUTPUT:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_13_40_09](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/e46a6003-bc16-4c63-80b3-31c0e444780f)


Invoke msfconsole:
## OUTPUT:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_13_39_39](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/d53b71dc-203b-4ac1-aaeb-5ac44c93b496)

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_13_40_09](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/147be9f4-e8ca-4420-b93d-5748ebb2667f)

Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
msf >  nmap -sT 192.168.1810/24 -p1-1000
## OUTPUT:

 ![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_13_42_05](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/018452ae-b2cb-4547-9c9a-3f60598a4ce0)

use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
msf > db_nmap 192.168.181.0/24
## OUTPUT:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_13_53_35](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/31e69bda-ad08-47c0-9a29-55f22c2459c0)

Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
cd /usr/share /metasploit-framework/modules/auxiliary
kali > ls -l
## OUTPUT:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_19_46](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/00e1bbd0-8a38-4ce7-a720-cf5207dde883)

Search is a powerful command in Metasploit that you can use to find what you want to locate. 
msf >search name:Microsoft type:exploit

## OUTPUT:

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_07_00](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/d12f04ea-fd21-48d4-aa6c-7526335745a4)

The info command provides information regarding a module or platform,

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_13_20](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/24788786-db37-4f8f-a3fb-44535d6fe7de)

Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
systemctl start postgresql
msfdb init
## MYSQL ENUMERATION
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_10_42](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/33108a63-c04f-4fa7-a947-e0e2b1f3de5b)

Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
search type:auxiliary mysql

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_11_32](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/36ec126d-fd48-4d07-86f1-cb399bbf9744)

use the auxiliary/scanner/mysql/mysql_version module by typing the module name or associated number to scan MySQL version details.
use 11
Or:
use auxiliary/scanner/mysql/mysql_version

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_12_15](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/3222eb72-b199-49e2-bf70-d0091f2a80b2)

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_13_02](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/d9b7a736-0d2f-4fd5-bd97-fd35657b23bb)

After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_14_49](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/c827f340-5f12-48dd-a5ac-77a6cdd2656f)

set the PASS_FILE parameter to the wordlist path available inside /usr/share/wordlists:
set PASS_FILE /usr/share/wordlistss/rockyou.txt
Then, specify the IP address of the target machine with the RHOSTS command.
set RHOSTS <metasploitable-ip-address>
Set BLANK_PASSWORDS to true in case there is no password set for the root account.
set BLANK_PASSWORDS true

![VirtualBox_kali-linux-2023 4-virtualbox-amd64_27_04_2024_14_18_28](https://github.com/Aishwarya-TM/EH-Ex-5/assets/127846109/5bfab096-cea4-4193-b01d-4bf6bd173e01)

## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
