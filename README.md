# gwas_catalog2polygenic_risk_network
This repository contains a tutorial with instructions for synthesizing GWAS results as a putative causal gene network. 
# Purpose
This tutorial is a walk-through for generating a putative causal gene network from NHGRI/EBI GWAS results. 

## Main steps: 
#### 1. get genome-wide significant hits for a trait of interest from the GWAS catalog 
[https://www.ebi.ac.uk/gwas]
#### 2. annotate them (here we use published results from open targets genetics locus 2 gene pipeline)
[https://genetics.opentargets.org/]
#### 3. enter these genes into the string database. (Protein-Protein Interaction Networks & Functional Enrichment Analysis)
[https://string-db.org]

## Step 1: get genome-wide significant hits
1. go to NHGRI/EBI GWAS catalog: https://www.ebi.ac.uk/gwas
2. enter your trait of interest into the search bar
3. click on your trait of interest. 
_Note: if your trait of interest does not have GWAS results the rest of the tutorial will not work._
4. scroll down the page to associations.
5. click the "export data" button <img width="51" alt="image" src="https://user-images.githubusercontent.com/104035002/177649019-076356c5-dbbd-4741-a3d3-030530337632.png">
6. save all gwas associations for your trait as .csv file. 
7. open in this file in a spreadsheet or other data table manipuating software. (our example uses microsoft excel).
8. select the Location column, copy and paste into a new column
9. under data menu, select text to columns
10. keep "delimited" selection
11. unselect any delimiters already selected and in Other enter ":"
12. click finish.
13. rename new columns to chromosome and position. 
14. add a filter to chromosome column
  – unselect "mapping not available
15. in the edit menu, select all. 
16. copy and paste the contents to another sheet. 
17. convert P-value column to scientific notation.
_Note: these numbers are of the format 5 x 10-6. One can use the text to columns trick above – copy to a new column and set "x" and not ":" as in step 11 and then repeat this for the 10-6 values using "-" as the delimiter. Following this, the following forumla is_


