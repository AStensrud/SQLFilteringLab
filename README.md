<h1>SQL Filtering Lab</h1>

<h2>Description</h2>
Project consisted of a simple SQL filtering excercise where I pretended that there has been suspicious login attempts in my organization and I have to figure out if the attempts were legitimate or breach attempts by a third party. I utilized the Linux Bash Shell to access SQL and ran queries against database tables related to employees and login logs.

<br />


<h2>Languages and Utilities Used</h2>

- <b>Linux termial / CLI</b> 
- <b>sqlite3</b>

<h2>Environments Used </h2>

- <b>Kali Linux</b>

<h2>Retrieving after hours failed login attempts</h2>

To begin with, I needed to find any login attempts made after office hours, which ends at 18:00, specifically any unsuccessful ones. To do this, I created a SQL query. In the top part of the screenshot below, you can see my query, and beneath it, the output. 

The organization keeps track of any login attempts in a table called <code>log_in_attempts</code> so I selected everything from that table, and used the <code>WHERE</code> clause with the <code>AND</code> operator to filter my results to output the attempts made after 18:00 that was not successful, by specifying the criteria <code>login_time > '18:00'</code> and <code>success = FALSE</code>. As the success column is a binary data type, either 0 or FALSE are accepted inputs for specifying failed attempts, and 1 or TRUE for successful attempts.


![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/7908ffab-a40d-4007-a3da-3fcfc5b3d6f7)

<h2>Retrieve login attempts on specific dates</h2>

On 2022-05-09 a suspicious event occurred, and we need to investigate any activity on this date and the day before. Below you can see the query I wrote to output the attempts on these two dates:

![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/fb338f50-bcf9-41d4-9854-a71114e216ce)

In order to structure the output, I specified that the output should be sorted by username, then login_date in ascending order, then finally login_time in descending order by adding the following to my query: <code>ORDER BY username, login_time ASC, login_time ASC</code>. This gave me the results in a chronological order for each user. To specify the date range, I used the <code>BETWEEN</code> operator and the <code>AND</code> operator.

<h2>Retrieve login attempts outside of Mexico</h2>

After investigating the data further, I believed there was an issue with login attempts made outside of Mexico, as all the users in Mexico succeeded to log in, while that was not the case for the other countries, so I investigated the login attempts made outside of Mexico further:

![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/f21c80dc-ed26-4c04-92e0-576b571573e1)

In order to filter out the results that were not in Mexico, I utilized the NOT and LIKE operators, to specify that I would not like results that were <code>LIKE 'MEX%'</code>. I specifically used the <code>LIKE</code> operator with the percentage sign (<code>%</code>) after the third letter in Mexico, as the table contains both ‘Mex’ and ‘Mexico’ entries. As the percentage sign is a placeholder for anything after the third letter in the word in this case, all results starting with Mex would be included in the condition.


<h2>Retrieve employees in Marketing</h2>

My team wanted to update computers for certain employees in the Marketing department. To do this, I had to get information on which employee machines to update. I created a SQL query to easily fetch the needed information, like shown in the first part of the screenshot below:

![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/1879e6ac-9941-4d9c-9ab2-7b16dd5d3c37)

As the employees that needed updates for their computers were the employees located in the East building, I specified that I wanted the results where the office started with the word <code>'East%'</code> by utilizing the percentage sign again together with the LIKE operator.

<h2>Retrieve employees in Finance or Sales</h2>

Likewise, the Finance and Sales employees also needed a machine update, although as they needed a different type of update, I created a SQL query to fetch the employees in these two departments specifically:

![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/32b63c45-b97b-4063-8178-486d823cbf04)

By utilizing the <code>OR</code> operator, I was allowed to fetch the users where the department was either Finance or Sales. 

<h2>Retrieve all employees not in IT</h2>

Lastly, we needed to push an update to the machines of every employee that was not a part of the Information Technology department:

![image](https://github.com/AStensrud/SQLFilteringLab/assets/126564741/c3b777a0-6262-4eda-8712-abad65457943)

Similarly to when we needed to find login attempts that were not made in Mexico, I utilized the <code>NOT</code> operator in conjunction with the <code>WHERE</code> clause, to specify that I wanted a list of employees that were not a part of the 'Information Technology' department.

<h2>Summary</h2>

By utilizing filters in SQL queries, I was able to get specific information on login attempts and employee machines. I ran these queries against the relevant database tables, log_in_attempts and employees. By using <code>AND</code>, <code>OR</code>, and <code>NOT</code> operators, I could filter for the specific information I needed for each task. I also utilized the LIKE operator and percentage sign, in order to filter the results for specific patterns.
