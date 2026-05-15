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

<img width="833" height="242" alt="image" src="https://github.com/user-attachments/assets/8e80d528-e314-4705-9166-bc818d3dc677" />

The command give us the list of our ip address that looks something like inet x.x.x.x

Invoke msfconsole:
## OUTPUT:


<img width="760" height="503" alt="image" src="https://github.com/user-attachments/assets/685f1f88-a512-4de3-a187-b74f2c68b205" />

This command is used invoke the Metasploit interface.

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.




Port Scanning:
Following command is executed for scanning the systems on our local area network with a TCP scan (-sT) looking for open ports between 1 and 1000 (-p1-1000).
msf >  nmap -sT 192.168.1810/24 -p1-1000  (Replace with appropriate IP Address)
## OUTPUT:

<img width="722" height="180" alt="image" src="https://github.com/user-attachments/assets/249deb19-08c9-46f7-8ed8-19ab78ef75e6" />

This command is used for TCP scanning all the devices in the network and checks the ports from 1 to 1000.


step4:
use the db-nmap command to scan and save the results into Metasploit's postgresql attached database. In that way, you can use those results in the exploitation stage later.

scan the targets with the command db_nmap as follows.
msf > db_nmap 192.168.181.0/24
## OUTPUT:

<img width="898" height="128" alt="image" src="https://github.com/user-attachments/assets/0484d76a-a2a2-4a00-b980-c9176974e7a0" />

This commands saves the result in the metasploit database.Useful later for exploitation modules and host management.




Metasploit has a multitude of scanning modules built in. If we open another terminal, we can navigate to Metasploit's auxiliary modules and list all the scanner modules.
cd /usr/share /metasploit-framework/modules/auxiliary
kali > ls -l
## OUTPUT:

<img width="625" height="450" alt="image" src="https://github.com/user-attachments/assets/752868f4-5945-4e76-af3b-946b43c3a6c6" />

This lists scanning modules.


Search is a powerful command in Metasploit that you can use to find what you want to locate. 
msf >search name:Microsoft type:exploit
## OUTPUT:

<img width="1512" height="863" alt="image" src="https://github.com/user-attachments/assets/1caf1c6a-7b1a-42b0-9c6c-a2adc118a8a4" />



The info command provides information regarding a module or platform,

Before beginning, set up the Metasploit database by starting the PostgreSQL server and initialize msfconsole database as follows:
systemctl start postgresql
msfdb init
## OUTPUT:


<img width="917" height="433" alt="image" src="https://github.com/user-attachments/assets/3b96d790-c273-4711-b159-27cd361a9bd2" />


## MYSQL ENUMERATION
Find the IP address of the Metasploitable machine first. Then, use the db_nmap command in msfconsole with Nmap flags to scan the MySQL database at 3306 port.
db_nmap -sV -sC -p 3306 <metasploitable_ip_address>

## OUTPUT:

<img width="957" height="167" alt="image" src="https://github.com/user-attachments/assets/bb6865a4-bd70-407d-96fd-1c58e332e799" />

This command is used to detect versions, default scripts on the MySQL port.



Use the search option to look for an auxiliary module to scan and enumerate the MySQL database.
search type:auxiliary mysql

## OUTPUT:

<img width="955" height="552" alt="image" src="https://github.com/user-attachments/assets/d8d90302-26d7-46c2-aada-122c3c4b9e01" />

This lists the MySQL related modules.


use the auxiliary/scanner/mysql/mysql_version module by typing the module name or associated number to scan MySQL version details.
use 11
Or:
use auxiliary/scanner/mysql/mysql_version
## OUTPUT:

<img width="688" height="75" alt="image" src="https://github.com/user-attachments/assets/5569c1c3-4119-4aca-be76-85db4480ec08" />


Metasploit scans the machines for MySQL version info

Use the set rhosts command to set the parameter and run the module, as follows:
## OUTPUT:

<img width="947" height="226" alt="image" src="https://github.com/user-attachments/assets/7bbe7acb-85dc-41d9-994f-1b4f5ebebb57" />



After scanning, you can also brute force MySQL root account via Metasploit's auxiliary(scanner/mysql/mysql_login) module.
## OUTPUT:


<img width="947" height="226" alt="image" src="https://github.com/user-attachments/assets/1c9b3479-cd3a-40ee-b55f-83a34614cbb9" />


set the PASS_FILE parameter to the wordlist path available inside /usr/share/wordlists:
set PASS_FILE /usr/share/wordlistss/rockyou.txt
Then, specify the IP address of the target machine with the RHOSTS command.
set RHOSTS <metasploitable-ip-address>
Set BLANK_PASSWORDS to true in case there is no password set for the root account.
set BLANK_PASSWORDS true
## OUTPUT:

<img width="947" height="226" alt="image" src="https://github.com/user-attachments/assets/71edffce-63d9-47f5-a9c7-951f138ab9d2" />




The mysql_login auxiliary module attempts to authenticate to a MySQL database server using multiple username/password combinations in order to identify valid credentials.

## RESULT:
The Metasploit framework for reconnaissance is  examined successfully
