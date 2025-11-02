# Dina VM Security Challenge: Complete Walkthrough
This project provides a detailed breakdown of the Dina virtual machine security challenge. This is an educational exercise created by Touhid Shaikh designed for beginners learning cybersecurity concepts.


## Difficulty Level: Beginner-friendly
Overview of the Process

The challenge involves systematically analyzing a virtual machine to identify vulnerabilities and, ultimately, gain administrative access. This follows standard security testing methodology used by professionals to assess system security.


### Phase 1: Network Discovery
The first step is to identify the target system on the network. Using network scanning tools, we determined that the target machine's IP address was 10.0.0.36. Port scanning revealed that port 80 (web services) was accessible.

<img width="845" height="528" alt="Network Discovery" src="https://github.com/user-attachments/assets/fbc486dd-246e-4446-9b7f-2decfb6ccea9" />

<img width="843" height="399" alt="Network Discovery 2" src="https://github.com/user-attachments/assets/cdaae857-0961-416c-a024-4167127bd3da" />

<img width="954" height="462" alt="Information Gathering 2" src="https://github.com/user-attachments/assets/8b77cc7b-f82e-4465-a64f-fef4263e1ea9" />

### Phase 2: Information Gathering
With port 80 open, we examined the web server. The initial homepage didn't reveal much, but further investigation showed a robots.txt file containing several directory paths.
Exploring these directories led us to one called "/nothing" which contained hidden information in its source code - specifically, a list of potential passwords.
To find additional directories, we performed a comprehensive directory scan and discovered a "/secure" folder containing a file named backup.zip.

<img width="962" height="760" alt="Information Gathering" src="https://github.com/user-attachments/assets/df1e5f11-bbc8-4432-ae7e-37ad05963bb1" /> 

<img width="961" height="246" alt="Information Garthering 4" src="https://github.com/user-attachments/assets/c65c6184-d124-4318-a338-5283f5c6b339" />

<img width="965" height="262" alt="Information Gathering 3 " src="https://github.com/user-attachments/assets/c4d2d1f7-adfb-4f6a-b6b4-f472f4cf6787" />

<img width="954" height="462" alt="Information Gathering 2" src="https://github.com/user-attachments/assets/4386e69c-245d-4065-bdea-0d08404a40a2" />

### Phase 3: Accessing Protected Files
The backup.zip file required a password. By testing the previously discovered passwords, we found that "freedom" successfully extracted the contents.
Inside was an audio file (backup-cred.mp3) that, upon closer examination, was actually a text file in disguise. This file contained:

* A username: touhid
* A hidden directory path: /SecreTgatwayLogin

### Phase 4: Gaining Initial Access
Navigating to the hidden directory revealed a playSMS login interface. Using the username "touhid" and testing various passwords from our earlier list, we successfully authenticated with the password "diana".
We then researched known vulnerabilities in the playSMS application and found an exploit that allows file upload through CSV functionality. After configuring the exploit parameters with our gathered credentials, we established a remote connection to the system.


### Phase 5: Expanding Access
Once connected with limited privileges (www-data user), we examined what permissions this account had. We discovered this user could execute Perl scripts with elevated privileges.

### Phase 6: Achieving Full Control
Leveraging the Perl execution permissions, we used a command to spawn a privileged shell, giving us administrative access. We then navigated to the restricted root directory and successfully retrieved the completion flag from flag.txt.


### Key Learning Points
This exercise demonstrates several important security concepts:

  * How exposed directories can leak sensitive information
  * The importance of protecting backup files
  * Why default or weak credentials create vulnerabilities
  * How seemingly minor permissions can be exploited
  * The value of systematic enumeration in security testing

This type of controlled environment helps security professionals develop skills for identifying and addressing real-world vulnerabilities.
