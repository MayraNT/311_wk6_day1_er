# Creating an ER Diagram from the Sakila Database

## Setup

You should already have MySQL installed from last week but if you don't, please [install it now](https://dev.mysql.com/downloads/mysql/).

## Instructions

##### Disable Binary Logging (Google Cloud)

We need to alter a setting in our cloud database in order to import the dataset that we need. This setting has to do with "triggers" which we have not learned about directly but that you will look for more practice with later. 

1. Navigate to cloud.google.com and make sure you are logged in

2. Navigate to your SQL instance (Cloud SQL)

3. Under the "configuration" tab on the right side of your screen, select "edit configuration"

4. Under "Enable auto backups" DESELECT "Enable Point-in-Time Recovery"/"*enable binary logging*"

5. Save and restart the instance

##### Import data

We are going to use a sample schema given to use by MySQL.

1. Download the zip directory and extract it
  * https://dev.mysql.com/doc/sakila/en/sakila-installation.html
  * The DB is called "sakila" under the Example Databases section

2. cd into that directory
  * Likely `cd ~/Downloads/sakila-db`

3. Run the connect command followed by `< sakila-schema.sql` to load that database
  * `mysql -u root -h <HOST IP FROM WORKBENCH> -p < sakila-schema.sql`

4. After the operation is complete (may take a couple mins) you should have automatically been exited from the `mysql` command

5. Pull up MySQL Workbench so that we can work with a familiar interface

6. You should see a "sakila" database on the left hand side

7. Double-click that database

8. Open a new query and run `select * from actor;`

9. Did you see any data? If not that's ok. The schema is more important here

10. You should see many tables under this database

##### Create ER Diagram

1. With MySQL Workbench open, click the "Database" tab

2. Select "Reverse Engineer"

3. Make sure your connection information is correct and then click "continue"

4. Under "Select the schemas you want to include:" choose "sakila"

5. DESELECT everything except "Import MySQL Table Objects"

6. Click "Execute"

7. You should see a pretty comprehensive ER diagram consisting of 16 tables

8. Answer the following questions about this diagram

##### ER Diagram Diagnosis 

1. What is the relationship between the "actor" and "film_actor" tables?
The relationship is one (and only one) from the "actor" to "film_actor" tables, and one-to-many from the "film_actor" to "actor" tables. Each actor can only have one name, but a single "film_id" can be associated with one or multiple actors. 

2. What does the blue diamond next to the "last_update" column on the "inventory" table represent?
The blue filled diamond represents a simple attribute that is NOT NULL. This means the "last_update" field must contain a timestamp.

3. How many foreign keys does the "payments" table have? How can you tell?
The payments table has 3 foreign keys, because there are red diamonds next to 3 of the fields in the table. "Customer_id" and "staff_id" have red filled diamonds, meaning they are NOT NULL foreign keys. "Rental_id" has the outline of a red diamond, meaning it's a foreign key that can be NULL.

##### ER Diagram upload

1. Take a screenshot of the ER diagram you created and name it "wk6_er_diagram"

2. Copy the screenshot to this directory and upload it (git push) along with this README
