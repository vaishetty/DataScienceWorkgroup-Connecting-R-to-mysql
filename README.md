# Data Science Workgroup: Connecting R to MySQL

## How to install mysql locally? (Applicable to MacOS)

### Step 1: Download & Install MySQL locally

- Download [MySQL Workbench](https://dev.mysql.com/downloads/workbench/). (Older version might not be compatible with the current version of MacOS). During installation, make note of the username and password. 

- MacOS might prevent you from launching it the first time, in which case it must be allowed to run manually via *System Preferences -> Security & Privacy -> Open Anyway* 

- Open MySQL Workbench and click on *Local instance 3306*. When prompted to enter your password, enter the password created above. 

- Let us create a sample database to connect with R. Under the *Administration* tab, click on *Data Import/Restore* and then select *Import from Self-Contained File*. We can download a [sample SQL file here](https://sample-videos.com/sql/Sample-SQL-File-1000rows.sql) 

<img width="1018" alt="Screen Shot 2021-02-28 at 9 35 06 PM" src="https://user-images.githubusercontent.com/55261637/109457377-9d794280-7a0f-11eb-8a3e-dca61cfb37ca.png">

- You can view the databases under the *Schemas* tab. By default, you can see one db named *sys* containing a default table 
named *sys_config* containing a few records. 

- 

- How to add data to a mysql databases from R
- How to use dplyr in R to access, querry and write to the db



