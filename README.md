# Dina VM Security Challenge: Complete Walkthrough
This project provides a detailed breakdown of the Dina virtual machine security challenge. This is an educational exercise created by Touhid Shaikh designed for beginners learning cybersecurity concepts.


#### Difficulty Level: Beginner-friendly

### Overview of the Process

The challenge involves systematically analyzing a virtual machine to identify vulnerabilities and, ultimately, gain administrative access. This follows standard security testing methodology used by professionals to assess system security.


### Phase 1: Network Discovery
The first step is to identify the target system on the network. Using network scanning tools, we determined that the target machine's IP address was 10.0.0.36. Port scanning revealed that port 80 (web services) was accessible.

<img width="844" height="452" alt="N-D" src="https://github.com/user-attachments/assets/2c1bfc79-1431-4a94-8065-74d9d9413890" />

<img width="841" height="540" alt="N-D2 " src="https://github.com/user-attachments/assets/936479f6-63da-4ad5-b8e8-10bfadf0bd22" />

<img width="995" height="729" alt="N-D3" src="https://github.com/user-attachments/assets/d78691e4-b484-4978-b7eb-583f91e02228" />
 

### Phase 2: Information Gathering
With port 80 open, we examined the web server. The initial homepage didn't reveal much, but further investigation showed a robots.txt file containing several directory paths.
Exploring these directories led us to one called "/nothing" which contained hidden information in its source code, specifically, a list of potential passwords.
To find additional directories, we conducted a comprehensive directory scan and discovered a "/secure" folder containing a file named "backup.zip".

<img width="962" height="760" alt="Information Gathering" src="https://github.com/user-attachments/assets/df1e5f11-bbc8-4432-ae7e-37ad05963bb1" /> 

<img width="961" height="246" alt="Information Garthering 3" src="https://github.com/user-attachments/assets/546b7e98-0445-4d2f-bd51-30b22d5170d5" />

<img width="954" height="462" alt="Information Gathering 2" src="https://github.com/user-attachments/assets/4386e69c-245d-4065-bdea-0d08404a40a2" />

### Phase 3: Accessing Protected Files
The backup.zip file required a password. By testing the previously discovered passwords, we found that "freedom" successfully extracted the contents.
Inside was an audio file (backup-cred.mp3) that, upon closer inspection, turned out to be a text file in disguise. This file contained:

<img width="1080" height="837" alt="Accessing " src="https://github.com/user-attachments/assets/25e37127-506f-4330-9ece-473cb0ecb567" />

<img width="995" height="368" alt="Accessing 2" src="https://github.com/user-attachments/assets/c6c3d6d9-bdbc-4f7e-a8ba-0ab404b4c0c4" />

* A username: touhid
* A hidden directory path: /SecreTgatwayLogin
<img width="961" height="536" alt="Accessing 3 " src="https://github.com/user-attachments/assets/5198d9fb-1460-4465-b481-0a903d1e8a1b" />


### Phase 4: Gaining Initial Access
Navigating to the hidden directory revealed a playSMS login interface. Using the username "touhid" and testing various passwords from our earlier list, we successfully authenticated with the password "diana".
We then researched known vulnerabilities in the playSMS application and found an exploit that allows file upload through CSV functionality. After configuring the exploit parameters with our gathered credentials, we established a remote connection to the system.

<img width="960" height="352" alt="Accessing 4" src="https://github.com/user-attachments/assets/5d0a2df2-05bc-4ddf-aef9-db082e4bfadd" />


### Phase 5: Expanding Access
Once connected with limited privileges (www-data user), we examined what permissions this account had. We discovered this user could execute Perl scripts with elevated privileges.
<img width="662" height="548" alt="Expanding " src="https://github.com/user-attachments/assets/bd1003bb-bb51-48e6-8924-a6d43436b6f7" />

<img width="1014" height="273" alt="Expanding 1" src="https://github.com/user-attachments/assets/4db62ec6-dc43-4d07-883a-ab37d051d937" />

### Phase 6: Achieving Full Control
Leveraging permissive Perl execution to escalate privileges and obtain an administrative shell. Using Nikto for a quick web vulnerability check helped confirm the attack surface, and once privileged we accessed the restricted root directory and retrieved the completion flag from flag.txt.
 * Hyphen H is what defines Nikto, that this is gonna be my target host.
  
<img width="1032" height="500" alt="Expanding 2" src="https://github.com/user-attachments/assets/8f22109a-777c-4b85-b9b5-e4236135e5c6" />


### Key Learning Points
This exercise demonstrates several important security concepts:

  * How exposed directories can leak sensitive information
  * The importance of protecting backup files
  * Why default or weak credentials create vulnerabilities
  * How seemingly minor permissions can be exploited
  * The value of systematic enumeration in security testing

This type of controlled environment helps security professionals develop skills for identifying and addressing real-world vulnerabilities.
