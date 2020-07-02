Scenario(s)

**LGICUS01.xaunit**

Two test cases

Existing customer(s)
- Read up to first three rows from table natively
- For each retrieved row
- Execute program, using the customer number retrieved natively
- verify that values returned by program match values retrieved natively

Non existing customer
- To make sure a certain (fixed) customer number does not exist delete row from table
- Execute program using customer number
- Verify that the return code indicates an error situation