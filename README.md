# Data Science Workgroup: Connecting R to MySQL

## How to install mysql locally? (Applicable to MacOS)

### Step 1: Download & Install MySQL locally

- Download [MySQL Workbench](https://dev.mysql.com/downloads/workbench/). (Older version might not be compatible with the current version of MacOS). During installation, make note of the username and password. 

- MacOS might prevent you from launching it the first time, in which case it must be allowed to run manually via *System Preferences -> Security & Privacy -> Open Anyway* 

- Open MySQL Workbench and click on *Local instance 3306*. When prompted to enter your password, enter the password created above. 

<img width="1016" alt="Screen Shot 2021-02-28 at 9 23 55 PM" src="https://user-images.githubusercontent.com/55261637/109458627-0366c980-7a12-11eb-845c-19b18a3a49ee.png">

- Let us create a sample database to connect with R. Under the *Administration* (1) tab, click on *Data Import/Restore* (2) and then select *Import from Self-Contained File* (3). We can download a [sample SQL file here](https://sample-videos.com/sql/Sample-SQL-File-1000rows.sql). Once the *.sql* file has been linked, to change the *Default Target Schema* click on *New...* and enter the name of the new database to connect to R (For eg. *sample_db*) (4). Next, click on the *Import Progress* tab (5) and hit *Start Progress*.
 
<img width="1018" alt="2" src="https://user-images.githubusercontent.com/55261637/109464312-57c27700-7a1b-11eb-9436-90fdb3e923e7.png">

- You can view the new database under the *Schemas* tab. You should see the new *sample_db* containing a table named *user_details* (from the SQL file we uploaded). 

# How to add data to a mysql databases from R?

### Step 2: Connecting MySQL database and R

- Install package RMySQL
`install.packages("RMySQL")`

- Connect R to MySQL. When prompted to enter your password, enter the password created above. 
`con = dbConnect(MySQL(), user="root", rstudioapi::askForPassword("Database password"), dbname="sample_db", host="localhost")`

- To Access the data from MySQL in R. Below chunk of code will display 10 records from *user_details* table.
`dbGetQuery(con, 'select * from user_details limit 10')`

<img width="827" alt="Screen Shot 2021-02-28 at 11 54 15 PM" src="https://user-images.githubusercontent.com/55261637/109467643-59db0480-7a20-11eb-83cc-899e201096d8.png">

- Create/Use a dataframe in R. 
  For example:
  `x <- 1:10`
  `y <- letters[1:10]`
  `sample_table <- data.frame(x,y)`
  `head(sample_table)`
  
  <img width="71" alt="Screen Shot 2021-03-01 at 12 00 50 AM" src="https://user-images.githubusercontent.com/55261637/109468372-5300c180-7a21-11eb-8aba-f0e2393811f3.png">

- Writing table to MySQL
  In order to avoide error (*Error in (function (classes, fdef, mtable)  : 
  unable to find an inherited method for function ‘dbWriteTable’ for signature ‘"MySQLConnection", "character", "tbl_MySQLConnection"’*) we use
  
  `dbSendQuery(con, "SET GLOBAL local_infile = true;")`
  
- Creating table *rtosql* in MySQL under *sample_db*
  `dbWriteTable(con, name = 'rtosql', value = sample_table, append = TRUE, temporary = FALSE)`

  In below image we can see table *rtosql* is created.

<img width="846" alt="5" src="https://user-images.githubusercontent.com/55261637/109469807-64e36400-7a23-11eb-8b8e-bb9e7c6ee648.png">

 
- How to use dplyr in R to access, querry and write to the db



