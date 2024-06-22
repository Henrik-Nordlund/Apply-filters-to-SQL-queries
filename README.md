<b>Project description</b><br>
I am a security analyst working at a larger organization, tasked with keeping the system secure. I have recently discovered some potential security issues having to do with suspicious failed login attempts, or machines held throughout the organization – various departments, various employees – that could pose a security risk.

<b>Objective: retrieve after hours failed login attempts</b><br>
There was a potential security accident that happened after hours (18:00). To investigate this, a SQL query in the Maria DB table was run , looking for records of all login attempts after 18:00. This is the query I used.
A star stands for “retrieve all”, and of course all numeric values need to have (‘’) around them since in our organization we take the threat of SQL injection seriously,
and having the retrieved value(s) converted to strings also reduces the risk for excessive server load stemming from that.

SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = ‘0’;

The reason for the last zero (0) is that login success is a Boolean value that is either TRUE (stored as 1) or FALSE (stored as 0). There were 19 such attempts.

<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Failed%20attempts%20to%20log%20in%20after%20hours.PNG"/>

<b>Objective: retrieve login attempts on specific dates</b><br>
There was a suspicious event on 2022-05-09. To investigate this, All login attempts on this day, and the day before was reviewed. A SQL query in the Maria DB table for records of all login attempts on those two days was run.
This is the query used, to retrieve both using the OR keyword.

SELECT * 
 FROM log_in_attempts 
 WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';

Note that all login attempts are of interest in this case.
<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Retrieve%20login%20attempts%20on%20specific%20dates.PNG"/>

<b>Objective: retrieve login attempts outside of Mexico</b><br>
There has been much suspicious activity with login attempts, but my organization has determined that those did originate from outside of Mexico. To retrieve those login attempts that needed further investigation, a query on the company was run on Maria DB in the table log_in_attempts.
To make sure that no attempts originating from Mexico was included by mistake, a % sign was added since the system log the country both as MEXICO and as MEX.
LIKE is a keyword that allows for searches using similar values rather than exact values, and of course NOT is a keyword that filters out all those values.

SELECT * FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';


<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Retrieve%20login%20attempts%20outside%20of%20Mexico.PNG"/>
The snapshot covers a part of the list. The full list shows 144 such attempts.<br>

<br>
<b>Objective: retrieve employees in Marketing</b><br>
There were security updates needed for some, but not all, machines in the Marketing department. Those needing attention were all situated somewhere in the East building.
To find them in the employee table this query was used. The dollar sign is to ensure that no affected machine in East building with all its offices gets missed, and no other marketing personnel gets needlessly affected. AND is the keyword that ensure that both conditions must be met to retrieve that value.

SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';

<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Retrieve%20employees%20in%20Marketing.PNG"/>

<b>Objective: retrieve employees in Finance or Sales</b><br>
Our team needs to perform an additional security update for all employees in the Sales and in the Finance departments. To find the employees in those departments this Maria DB SQL query in the employee table was run,
and filtered, for employees in the Finance and Sales departments, respectively. OR is a keyword that ensures that if any condition is met then that value should be retrieved. 

SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';

<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Retrieve%20employees%20in%20Finance%20or%20Sales.PNG"/>
The snapshot covers a part of the list. The full list is of 71 employees.<br><br>

<b>Objective: retrieve all employees not in IT</b><br>
There was a need to perform a security update on all computer machines. Every employee in Information Technology department had already received that update,
so this SQL query to find all other employees in the organization was effective so that those machines too could be updated.
This was the query used in the employee data table, using the NOT keyword to filter out all employees in the IT department.

SELECT * 
FROM employees
WHERE NOT department = 'Information Technology'; 


<img src = "https://github.com/Henrik-Nordlund/Apply-filters-to-SQL-queries/blob/947cd6b2799336adbcbc48b28e0ab7e8ad44f7b6/Retrieve%20all%20employee%20not%20in%20IT.PNG"/>
The snapshot covers a part of the list. The full list is of 161 employees.

<b>Summary</b><br>
This project illustrates how filters can be applied to SQL queries, AND, OR and NOT to get more precise answers. I also used LIKE and the % sign to search for patterns in my searches.
