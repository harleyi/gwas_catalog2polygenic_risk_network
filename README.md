# gwas_catalog2polygenic_risk_network
This repository contains a tutorial with instructions for synthesizing GWAS results as a putative causal gene network. 
# Purpose
This tutorial is a walk-through for generating a putative causal gene network from NHGRI/EBI GWAS results. 

## Main steps: 
### 1. get genome-wide significant regions and corresponding lead variants for a trait of interest from the GWAS catalog 
[https://www.ebi.ac.uk/gwas]
### 2. annotate them (here we use published results from open targets genetics locus 2 gene pipeline)
[https://genetics.opentargets.org/]
### 3. enter these genes into the string database. (Protein-Protein Interaction Networks & Functional Enrichment Analysis)
[https://string-db.org]

## Step 1: get genome-wide significant regions and corresponding lead variants
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

## Step 2. annotate the regions with putative causal genes 
_Note: here we use published results from open targets genetics locus 2 gene pipeline, using an alternative approach, such as FUMA [https://fuma.ctglab.nl/] to map SNPs to putative causal genes could also be used_

39. go to open targets genetics. 
40. search for your trait of interest.
41. one-by-one select each published GWAS:    
    42. save the tsv (tab separated values) file and open it in excel or similar spreadsheet viewer.   
    43. for each Lead Variant with an entry in the L2G column, annotate the corresponding region from the "genome-wide significant regions and the corresponding reported lead variant" file from Step 1.   
    _Note: According to Open Targets Genetics, the Lead Variants with L2G annotation represent "Genes prioritised by our locus-to-gene model with score ≥ 0.5" See L2G description [https://genetics-docs.opentargets.org/our-approach/prioritising-causal-genes-at-gwas-loci-l2g] for further details._   
    
44. Once you have done this for all published GWAS studies, you will have a list of the putative causal genes for your trait of interest. 
_Note: Your list of putative causal genes will almost certainly be less than the number of regions. In our experience, L2G has assigned a putative casual gene for approximately 50-60% of GWAS regions for several immune-mediated disease traits. An alternative is to manually annotate remaining loci as was done in Systemic Lupus as a Genetic disease [https://pubmed.ncbi.nlm.nih.gov/35149194/] DOI: 10.1016/j.clim.2022.108953 [https://doi.org/10.1016/j.clim.2022.108953]

45. copy the L2G column and paste it into a new column
46. use text to columns with "," as the separator to remove any commas which may have been used to separate putative causal genes in the scenario where L2G identified two likely putative causal genes (e.g. eQTL controlling the expression of multiple genes.)
47. copy any genes from the second column to the bottom of the list of genes. 

## Step 3. Use putative causal gene list from step 2 to query String database in order to obtain and compare disease gene protein protein interaction network(s). 
48. Go to STRING [https://string-db.org/]
49. click search
50. Click multiple proteins on the left hand side
51.	Remove commas and ensure that each putative causal gene is on a single line
52. Enter the list of putative causal genes in the “list of names” box
53. Select Homo sapiens as organism
54.	Search 
55.	Manually review gene names and descriptions to ensure that the correct mapping occurred. _Note: in some instances, the gene name and the protein name may not be the same._
56.	Click continue 
57. open cytoscape on your computer. [https://cytoscape.org/]
58. click "send network to cytoscape".

59. If you do not have additional disease networks (or other networks of interest) in cytoscape, build them and import them into cytoscape (either through STRING web interface "send network to cytoscape" or by exporting network to file and importing multiple networks of interest from files into a new cytoscape session. 

60. Merge networks of interest in cytoscape [Tools --> Merge, Networks]
   – first using intersection [this is the count of overlapping genes between the two networks]
   – then using union [this is the entire list of genes present in either network] 
   
61. You can then use these numbers to calculate whether the gene overlap is greater than expected by chance between networks of interest using the cumulative distribution function of the hypergeometric distribution. 

A simple calculator can be found: https://systems.crump.ucla.edu/hypergeometric/index.php

For our example, we will take two networks, a first network with 54 nodes and a second network with 127 nodes.

The Union of these two networks is a gene network with 172 nodes and the intersection 9 nodes. 

Since there are 19566 distinct genes in the current release (v11.5) of the STRING interaction network for _Homo sapiens_, the calculation can be setup as follows: 

   – *k = 9* (the intersection of the two disease networks is the number of successes).   
   – *s = 54* (the sample size is the number of nodes in the first gene network).   
   – *M = 127* (the number of successes in the population is the number of nodes in the second gene network).   
   – *N = 19566-54 = 19439* (the population size is the entire Homo sapiens gene network with the 54 genes in the first network removed).   


Output:   
`Parameters: 9, 54, 127, 19439`   
`expected number of successes = 0.352795925716343`   
`the results are over enriched 25.51 fold compared to expectations`   
`hypergeometric p-value = 6.755808180896782e-11`   
   





   








