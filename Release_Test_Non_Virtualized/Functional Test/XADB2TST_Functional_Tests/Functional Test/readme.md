Scenarios

**XADB2TST_CRUD.xaunit**

Scenario to test the "life cycle" of a record using all four functions in a row
Scope "Initialization"
- read data to be used from local file
- use variables for table name and creator name of DB2 table
- use variables for old values from local input file
- use variables for "fixed" expected values

Scope "Determine DB2 Table Row Id"
- retrieve highest existing row id from the table and calculate next possible id

Next scopes - successively use program to
- insert new record into table and verify results (see XADB2TST_Insert.xaunit for details)
- get the new record verify results (see XADB2TST_Get.xaunit for details)
- modify the new record and verify results (see XADB2TST_Modify.xaunit for details)
- delete the new record and verify results (see XADB2TST_Delete.xaunit for details)

Scope "Clean Up Database"
- delete inserted row from the table to clean up database after test

**XADB2TST_Delete.xaunit**

Program receives a "function code" and data via linkage section. Based on the function code it executes different functions against DB2 table XAEMPLOYEE like
Insert, Get, Delete, Modify

Scenario to test Delete function - the program will not delete the record physically. Instead it will set the status code to "D"

Scope "Initialization"
- read data to be used from local file
- use variables for table name and creator name of DB2 table
- use variables for old values from local input file
- use variables for "fixed" expected values

Scope "Determine DB2 Table Row Id"
- retrieve highest existing row id from the table and calculate next possible id

Scope "Add row to table"
- use the next row id to insert new row into table natively using the data from local file

Two tests
Scope "Positive Tests" - Existing row(s)
Sub Scope "Execute Tests"
- Use next row id function code "delete" to execute program
Sub Scope "Verification"
- use the next row id again and retrieve data natively from table
- verify that the status in the tabe has been set to "D"

Scope "Negative Tests" - Non existing row
Sub Scope "Set up"
- Calculate new row id
- retrieve data from table natively, using new row id 
- verify that no data was retrieved, otherwise abort test
Sub Scope "Execute Tests"
- execute program using new row id and "after" data from local file
- Verify that return code indicates error

Scope "Clean Up Database"
- delete inserted row from the table to clean up database after test


**XADB2TST_Get.xaunit**

Program receives a "function code" and data via linkage section. Based on the function code it executes different functions against DB2 table XAEMPLOYEE like
Insert, Get, Delete, Modify

Scenario to test Get function
Scope "Initialization"
- use variables for table name and creator name of DB2 table

Scope "Determine DB2 Table Row Id"
- retrieve highest existing row id from the table and calculate next possible id

Scope "Check that row exists"
- use the highest row id and retrieve data natively from table
- verify that a result was returned, otherwise the scenario will abort

Execute two test cases
Scope "Positive Tests" - Existing row(s)
Sub Scope "Execute Tests and Verify"
- Use highest row id and function code "get" to execute program
- verify that data returned ba program matches data retrieved natively

Scope "Negative Tests" - Non existing row
Sub Scope "Check that row does not exist"
- Use next row id to retrieve data from table natively
- Verify that no data was retrieved, otherwise abort test
Sub Scope "Execute Negative Tests and Verify"
- Use next row id and function code "get" to execute program
- Verify that return code indicates an error

**XADB2TST_Insert.xaunit**

Program receives a "function code" and data via linkage section. Based on the function code it executes different functions against DB2 table XAEMPLOYEE like
Insert, Get, Delete, Modify

Scenario to test Insert function
Scope "Initialization"
- read data to be inserted from local file
- use variables for table name and creator name of DB2 table
- use variables for "fixed" exepected values

Scope "Determine DB2 Table Row Id"
- retrieve highest existing row id from the table and calculate next possible id

Scope "Check table before"
- use the next row id and retrieve data natively from table
- verify that no result was returned, i.e. the row does not exist and can be inserted

Scope "Execute Tests"
- Use next row id function code "insert" to execute program

Scope "Verification"
- use the next row id again and retrieve data natively from table
- verify that this time a result was returned, otherwise abort test
- verify fields retrieved via program matches data from intial local file

Scope "Clean Up Database"
- delete next row id from the table to clean up database after test

**XADB2TST_Modify.xaunit**

Program receives a "function code" and data via linkage section. Based on the function code it executes different functions against DB2 table XAEMPLOYEE like
Insert, Get, Delete, Modify

Scenario to test Modify function
- read data to be used from local file: Before modify and after modify
- use variables for table name and creator name of DB2 table
- use variables for old values from local input file
- use variables for "fixed" expected values
- retrieve highest existing row id from the table and calculate next possible id

- use the next row id insert new row into table natively using the "before" data from local file
- verify that no result was returned, i.e. the row does not exist and can be inserted

Execute two test case
Positive - Existing row
- Use next row id function code "modify" to execute program, using "after" data from local file
- use the next row id again and retrieve data natively from table
- verify that data retrieved from table matches the "after" data from local file

Negative - Non existing row
- Calculate new row id
- retrieve data from table natively, using new row id 
- verify that no data was retrieved, otherwise abort test
- execute program using new row id and "after" data from local file
- Verify that return code indicates error

Clean up
- delete inserted row from the table to clean up database after test