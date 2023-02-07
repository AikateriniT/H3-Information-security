Task 1:

I decided to create another repository with useful vocabulary and definitions that will be extremelly useful for me during the entire class. 

The link is:
https://github.com/AikateriniT/SECURITY-VOCABULARY
____________________________________________________________________________________________
x) Read and summarize (This subtask x does not require tests with a computer. Some bullets per article is enough for your summary, feel free to write more if you like)

    € Costa-Gazcón 2021: Practical Threat Intelligence and Data-Driven Threat Hunting 
    Chapter 4: Mapping the Adversary (all but "Testing yourself", which is left as voluntary bonus)'
    
Chapter 4: Mapping the Adversary.

In the 4th chapter the author explains how to work with the MITRE ATT&CK Framework, and making reports on the topics: - The ATT&CK Framework - Mapping with ATT&CK - Testing ourselves

ATT&CK Framework

    - The ATT&CK Framework is a descriptive model used to label and study the activities that a threat 
    actor is capable of carrying out in order to get a foothold and operate inside a system.
    - It works as a common language that both offensive and defensive researchers can use to better 
    understand each other and to better communicate with people not specialized in the field.
    - Creation of tactics 
    
14 tactics that it uses:

    - Reconnaissance: gathering information about the victim information. 
    - Resource Development: The attacker makes an assessment of his resources.
    - Initial Access: description of how the attacker gets access in the victim's system.
    - Execution: It means the execution of malevolent code in the victim's system.
    - Persistence: The ability of the attacker to remain in the victim's system.
    - Privilege Escalation: Obtaining further access in the victim's system.
    - Defense Evasion: The ways that the perpetrator manages to remain invisible in the system.
    - Credential Access: The attacker manages to obtain real credentials of the victim in order 
    to gain access in other environments.
    - Discovery: The attacker gets information about victim's system constitution.
    - Lateral Movement: The attacker manages to move around victim's system.
    - Collection: The attacker gets information from the victim for future use.
    - Command and Control: Managing to communicate with the victim's system.
    - Exfiltration: Stealing personal information from the victim while he stays invisible.
    - Impact: Preventing the victim from gaining access to his own system.
    
The ATT&CK Matrix

All the information, included in the techniques, makes ATT&CK an excellent resource for planning blue and red teaming exercises, studying threat actors, crafting your own threat hunting plan, mapping defensive controls, or even a means for studying cybersecurity concepts.

    
THE ATT&CK NAVIGATOR

In this chapter there is a great description, showing how to reduce the risk of getting hacked by choosing the correct layers. 

        This tool is a great instrument for visualizing a threat actor's modus operandi, the 
        behavior of a specific tool, or to generate a security exercise.

____________________________________________________________________________________________
y) Write an answer with references (this subtask does not require tests with a computer). Answer in the context of Mitre Att&ck, and pick examples that are different from the chapter in task x.
Define tactic and give an example.
Define technique and subtechnique, and give an example of each.
Define procedure, and give an example of each.
____________________________________________________________________________________________
Define tactic and give an example.
-----------------------------------------------------------------------------------------------------------------
     - A specific malevolent behaviour which has a set of techniques
     - Each tactic represents a tactical goal, for this reason the perpetrator is showing a specific behaviour.
     - For example credential access is a tactic used by the attacker in order to get legitimate access codes 
     and credentials from the victim, in order to create more accounts with the real ID of the victim. So by 
     disguising as the victim they can exploit their financial status and place orders or exploit people from 
     their family environment, by fooling them that he is actually the victim. 

Define technique and subtechnique, and give an example of each.
------------------------------------------------------------------------------------------------------------------
    - As technique is defined the interaction the perpetrator has with the system during a malevolent operation. 
    By the time this book was written there were about 183 techniques and 372 sub-techniques. 
    - MITRE ATT&CK Techniques outline a particular way to achieve the goal of a Tactic. 
    For example: The brute force technique for credential access in the enterprise Matrix has four sub-techniques:
        - Password guessing
        - Password cracking
        - Password spraying
        - Credential stuffing
    - So as a sub-technique we can define the ways to carry out the main Technique but take advantage of different 
    mechanisms to do so.


Define procedure, and give an example of each.
-------------------------------------------------------------------------------------------------------------------

    - While procedures do not appear in the MITRE ATT&CK Framework matrices, they do occur. 
    - The procedures that which can be viewed by clicking on a particular Technique or sub-technique show with 
    detail known implementations. 
    For example they can include known malware variants that they use a known method or threat actors whose TTPs 
    include the said technique or subtechnique. 
    A Procedure is a “what”.  An example of a Procedure for Credential Access would be a password cracking tool 
    like Hashcat or John the Ripper.

A Procedure may use multiple different Sub-Techniques, and many different Procedures may implement the same 
Sub-Technique.

____________________________________________________________________________________________
WebGoat Sensitive Data Exposure: Insecure Login
____________________________________________________________________________________________

Encryption is a very important tool for secure communication. Data encryption must always be used when we send sensitive data.

    - Basic understanding of packet sniffer usage
    - The user will be able to intercept and read encrypted requests
    
I found this task rather hard to finish so I will try again after the course on wednesday

____________________________________________________________________________________________
Voluntary:
WebGoat - Injection (advanced)

The goals of this part is to teach the more advanced topics for an SQL injection by combining SQL injection techniques and the Blind SQL injection.

Task 3: Pulling data from other tables.

    CREATE TABLE user_data (userid int not null,
                           first_name varchar(20),
                           last_name varchar(20),
                           cc_number varchar(30),
                           cc_type varchar(10),
                           cookie varchar(20),
                           login_count int
                           );
                           
    CREATE TABLE user_system_data (userid int not null primary key,
                                              user_name varchar(12),
                                              password varchar(10),
                                              cookie varchar(30)
                                              );
 
6.a) Retrieve all data from the table
 
6.b) When you have figured it out... What is Dave's password?
 
For the first attempt we should try chaining and for the second attempt we should try the UNION. From the creation of the tables we already know that they are susceptible to SQL injection. For the chaining we have to think, that we don't know any name from the table (';), then we want to print all the columns included (SELECT *) inside the user_system_data (FROM user_system_data; --) 
So, as a solution we have the:

        '; SELECT * FROM user_system_data; --
        SELECT * FROM user_system_data WHERE last_name = "; SELECT * FROM user_system_data; --
        (that is the query)
        
![1](https://user-images.githubusercontent.com/113516460/217308072-1d4fd3c0-19c4-449f-8f38-a008d4ea7d68.JPG)

Then we will try to figure out how to do it by using UNION. 

    By following the syntax of UNION provided from the last task we do like that:
    ' UNION SELECT 1, user_name, password, cookie, 'A','B', 1 FROM user_system_data;--
    SELECT * FROM user_data WHERE last_name = "UNION SELECT 1, user_name, password, cookie, 'A','B', 
    1 FROM user_system_data;--
    
    
    Hint! he datatype of the first column in the first SELECT statement, must catch the datatype of the first 
    column in the second(third, fourth..) SELECT stetement. The same applies to all other columns. 
    
    The password of Dave is: passW0rD
    
![2](https://user-images.githubusercontent.com/113516460/217311180-76397ea9-0ec0-45b8-9e5f-9b79c1a7b06f.JPG)

Task 5:
_______________________________________________________________________________________________
In this task we must brute force ourselves in the system. We only know that the username is Tom and nothing more. 
I can tell you already that this task took me around 1,5 hour to complete and half a packet of cigarettes. 
But lets see how we will manage to get ourselves in. 

First I tried to log in with any variable but I was always getting an error, that 'no results matched', so then I thought that I might need to register Tom as a user. But to my surprise Tom user already exists. 

Since we are doing 'blind attacks' we gather all the information given. As true, false or error. 
So when we try to add as a user  TOM' AND '1'='1, we receive the message that {0} user already exists. We may get a hint here that the username field is susceptible to SQL injection. 

The other goal is to find out what is the name of the table that the passwords are listed. If this exersice is very basic as I am guessing, then the name of the table might be "password". So I will start a long journey guessing the letters from Tom's password. I will use the statement "User{0} already exists" as a true statement. 

Using the string from the last page and adapting it to the needs of this attempt to log in we have:

    tom' AND substring(password,1,1)='t
    
From this we understand that letter "t" is the first letter of Tom's password. 

Then I couldn't manage to figure our what was happening so I had to watch a long video about how to brute force. From my perspective the material that was given before this assignment was not enough to manage to solve this. NetworkChuck is one of my sources. 

I'll continue the explanation soon!





SOURCES
______________________________________________________________________________________________

https://www.youtube.com/watch?v=2OPVViV-GQk

https://www.youtube.com/watch?v=z4_oqTZJqCo

https://github.com/AikateriniT/SECURITY-VOCABULARY/blob/main/README.md
