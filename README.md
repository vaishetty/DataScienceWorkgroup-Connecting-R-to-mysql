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

- Install the `RMySQL` R package and load the library in your R session.

`install.packages("RMySQL")`

`library(RMySQL)`

- Establish the connection between your RStudio and MySQL like so - 

`con = dbConnect(MySQL(), user="root", rstudioapi::askForPassword("Database password"), dbname="sample_db", host="localhost")`

(When prompted to enter your password, enter the password created above).

- Now, we can query data from MySQL using R, like so -

`dbGetQuery(con, 'select * from user_details limit 10')`

Above query will display 10 records from the *user_details* table.

<img width="827" alt="Screen Shot 2021-02-28 at 11 54 15 PM" src="https://user-images.githubusercontent.com/55261637/109467643-59db0480-7a20-11eb-83cc-899e201096d8.png">

- We can also write/export an R dataframe to MySQL. 
  
  To illustrate, let us create a sample dataframe in R containing 2 columns `x` (Containing 10 numbers) & `y` (Containing 10 letters), like so -  
  
  `x <- 1:10`
  
  `y <- letters[1:10]`
  
  `sample_table <- data.frame(x,y)`
  
  <img width="71" alt="Screen Shot 2021-03-01 at 12 00 50 AM" src="https://user-images.githubusercontent.com/55261637/109468372-5300c180-7a21-11eb-8aba-f0e2393811f3.png">

- Now, we can write this dataframe *sample_table* from R as a table into *sample_db* database in MySQL.

  To do this, we need to enable write privilages, like so -
  
  `dbSendQuery(con, "SET GLOBAL local_infile = true;")`
  
- Now we can write the table *sample_table* from R to MySQL under *sample_db*. Here, we have the option to change the name of the table being written into the MySQL database. Let us call it *rtosql*, like so -

  `dbWriteTable(con, name = 'rtosql', value = sample_table, append = TRUE, temporary = FALSE)`

  
<img width="846" alt="5" src="https://user-images.githubusercontent.com/55261637/109469807-64e36400-7a23-11eb-8b8e-bb9e7c6ee648.png">

As we can see, the table *rtosql* is created under *sample_db* database.

 
# How to use dplyr in R to access, querry and write to the db ?

### Step 3: Accessing MySQL database with R via `dplyr`.

- Install the `dplyr` R package and load the library in your R session. 

`install.packages("dplyr")`

`library(dplyr)`


- We can access *user_details* table from MySQL to R using `dplyr`, like so -

`dplyr_table <- tbl(con, "user_details")`

`head(dplyr_table)`

<img width="840" alt="6" src="https://user-images.githubusercontent.com/55261637/109476064-4ed9a180-7a2b-11eb-9ff7-3017c5d3dcd0.png">

- Instead of using SQL queries, we can access/select/filter data using `dplyr`. For eg., If we need to select details of only male users from *user_details* table, we can use:

`dplyr_table %>% filter(gender == "Male")`

