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


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
