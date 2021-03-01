# Data Science Workgroup: Connecting R to MySQL

## How to install mysql locally? (Applicable to MacOS)

### Step 1: Download & Install MySQL locally

- Download [MySQL Workbench](https://dev.mysql.com/downloads/workbench/). (Older version might not be compatible with the current version of MacOS). During installation, make note of the username and password. 

- MacOS might prevent you from launching it the first time, in which case it must be allowed to run manually via *System Preferences -> Security & Privacy -> Open Anyway* 

- Open MySQL Workbench and click on *Local instance 3306*. When prompted to enter your password, enter the password created above. 

<img width="1016" alt="Screen Shot 2021-02-28 at 9 23 55 PM" src="https://user-images.githubusercontent.com/55261637/109458627-0366c980-7a12-11eb-845c-19b18a3a49ee.png">

- Let us create a sample database to connect with R. Under the *Administration* tab, click on *Data Import/Restore* and then select *Import from Self-Contained File*. We can download a [sample SQL file here](https://sample-videos.com/sql/Sample-SQL-File-1000rows.sql). Once the *.sql* file has been linked, to change the *Default Target Schema* click on *New...* and enter the name of the new database to connect to R. Next, click on the *Import Progress* tab and hit *Start Progress*. 
 
<img width="1018" alt="2" src="https://user-images.githubusercontent.com/55261637/109463760-6b211280-7a1a-11eb-819d-b9b5024d3a0b.png">

- You can view the databases under the *Schemas* tab. You should see a tableA  *sys* containing a default table 
named *sys_config* containing a few records. 

- 

- How to add data to a mysql databases from R
- How to use dplyr in R to access, querry and write to the db



