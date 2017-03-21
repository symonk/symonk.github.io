

# Database Definition Language (DDL) Vs. Database Manipulation Language (DML)

Database Definition Language is essentially the collective statements that are used to define the database structure or the schema.
Some examples of these statements are:

- CREATE: Create Objects in the database.
- ALTER: Modify the structure of the database.
- DROP - Remove/Delete objects from the database.
- TRUNCATE - Remove all records from a table.
- COMMENT - Add comments to the data dictionary.
- RENAME - Rename an object in the database.
    
**note: ** Truncate Vs. Drop - Both Drop & Truncate *cannot* be rolled back as they are DDL, Delete is DDM and can be rolled back.

Database Manipulation Language is essentially the collective statements that are used to manage data within schema objects. 
Some examples of these statements are:

- SELECT: Retrieve data from a database
- INSERT: Insert data into a table 
- UPDATE: Update existing records in a database with new content
- DELETE: Delete all records from a particular table 
