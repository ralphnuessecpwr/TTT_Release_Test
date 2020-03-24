Scenarios

**CWXTCOB_End_Of_Month.xaunit**

This scenario is not working yet:
Execute Xchange to simulate end of month execution

**CWXTCOB_Standard.xaunit**

Execute program on a "normal" day
- Prepare mainframe input dataset EMPFILE from local data
- Execute CWXTCOB
- Read output file RPTFILE
- Verify for each detail record, that total wages equal sum of wages, overtime and commision
- Compare actual RPTFILE against expected RPTFILE

Not working yet:
Store expected RPFILE data locally and restore to mainframe