# preAIA102RelevanceAt10
Data science project assessing the percentage of pre-AIA patents in litigation and prosecution through 2021. 

Files: 
1. HarrityCleanedData.csv
 - contains data obtained through Harrity Patent Analytics. 
 - each record corresponds to a single litigation. 
 - the "first_patent" field isolates the earliest-filed patent of the patents listed in the "patents" field. 

2. May2021Applications.csv
 - contains data obtained through Harrity Patent Analytics. 
 - each record corresponds to a single patent application having a PTO Office Action during the month of May 2021. 

3. Lit_Query1_Join PatentsView
 - SQL Query, executed in Google BigQuery
 - Takes in the list of litigations
 - Filters it so that it removes
       - Cases prior to 2013
       - Cases with blanks in the Patents field
       - Cases with first patents whose patent numbers aren’t integers
 - Joins it with patentsview data to get filing dates, foreign & domestic priority dates for the patent in the first_patent field
 - After running, store this data in a table called PreAIA102Relevance_LitigationsPlusDates

4. Lit_Query2_AddBooleans
 - SQL View, executed in Google BigQuery
 - Takes the list of litigations with dates, now saved as a table in BigQuery
 - Adds three columns with booleans corresponding to whether the filing date, domestic priority date and foreign priority date are Pre-AIA or not

5. Lit_Query3_Aggregate
 - SQL Query, executed in Google BigQuery
 - Takes the View and counts its pre-AIA booleans
 - Summarizes by the year of litigation

6. Lit_Query4_ErrorCheck
 - SQL Query, executed in Google BigQuery
 - performs error-checking, displaying the records that differred between the Harrity results and the PantentsView results regarding whether the patent was pre- or post-AIA
