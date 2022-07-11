# gwas_catalog2polygenic_risk_network
This repository contains a tutorial with instructions for synthesizing GWAS results as a putative causal gene network. 
# Purpose
This tutorial is a walk-through for generating a putative causal gene network from NHGRI/EBI GWAS results. 

## Main steps: 
### 1. get genome-wide significant lead variants for a trait of interest from the GWAS catalog 
[https://www.ebi.ac.uk/gwas]
### 2. annotate them (here we use published results from open targets genetics locus 2 gene pipeline)
[https://genetics.opentargets.org/]
### 3. enter these genes into the string database. (Protein-Protein Interaction Networks & Functional Enrichment Analysis)
[https://string-db.org]

## Step 1: get genome-wide significant lead variants
### download table of published GWAS variants
1. go to NHGRI/EBI GWAS catalog: https://www.ebi.ac.uk/gwas
2. enter your trait of interest into the search bar
3. click on your trait of interest. 
_Note: if your trait of interest does not have GWAS results the rest of the tutorial will not work._
4. scroll down the page to associations.
5. click the "export data" button <img width="51" alt="image" src="https://user-images.githubusercontent.com/104035002/177649019-076356c5-dbbd-4741-a3d3-030530337632.png">
6. save all gwas associations for your trait as .csv file. 
7. open in this file in a spreadsheet or other data table manipuating software. (our example uses microsoft excel).
### make columns for chromosome and position, eliminating rows with missing information
8. select the Location column, copy and paste into a new column
9. under data menu, select text to columns
10. keep "delimited" selection
11. unselect any delimiters already selected and in Other enter ":"
12. click finish.
13. rename new columns to chromosome and position. 
14. add a filter to chromosome column
  – unselect "mapping not available
### Filter for genome-wide significant variants
15. in the edit menu, select all. 
16. copy and paste the contents to another sheet. 
17. convert P-value column to scientific notation.

_Note: these numbers are of the format 5 x 10-6. One can use the text to columns trick above – copy to a new column and set "x" and not ":" as in step 11 and then repeat this for the 10-6 values using "-" as the delimiter. Following this, the following forumla is_

18. Copy the new P-value column and paste it in place using "Paste Special" and select values (not formulas)
19. Delete intervening columns. 
20. add filter to P value column by selecting "less than or equal to" and entering 5E-8
21. select all. 
22. copy the genome-wide significant filtered variants to a new sheet. 
### Filter for Trait or subphenotype of interest
23. add filter to "Trait(s)" column 
– unselect all, then select your trait of interest
24. copy genome-wide significant variants for your trait of interest to a new sheet.
25. Sort by chromosome and then position
### Define Regions
26. Make a Region column
27. enter the value 1 in first row of the Region column.
28. In the second row of the Region column, enter the following formula to specify a window of 250,000 base pairs around each lead variant: 
`=IF(N2=N3, IF(O3<(O2+250000), Q2, Q2+1), Q2+1)`

_Note1: You may need to modify the formula so that it points to the correct column – In our example N is the chromosome column, O is the position column and Q is the Region column._

_Note2: the correctness of this formula depends on the rows being sorted by chromosome and position and on the first row having Region #1 in it._

_Note3: this formula works as follows If N2 equals N3, it means the chromosome has not changed, so check to see if the position is within the window. If so, extend the region, if not, start a new region. If N2 does not equal N3, we are at a new region, so the region counter (Q2) should be increased._ 

29. copy and paste this formula into each of the rows in the Region column except after the first row. 
### Select Lead variants
31. copy Regions column and paste as values into the same column
32. sort by Region, then P-value
33. Make a "Lead Variant" column
34. In the second row of the Lead Variant column, enter this forumla to specify the lead variant: 
`=IF(Q1=Q2, True, False)`

_Note: You may need to modify the formula so that it points to the correct column – In our example Q is the Region column._

35. copy Lead Variant column and paste as values into the same column
36. filter on "TRUE". 
37. copy filtered values to a new worksheet.
38. You now have all of the genome-wide significant regions and the correpsonding reported lead variant for your trait of interest.





