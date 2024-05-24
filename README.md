# Family Resources Survey & Households Below Average Income (FRS/HBAI)
The aim of this repository is to make it easier to extract and combine data for multiple years of the UK's Family Resources Survey (FRS) and the related Households Below Average Income (HBAI) data series.

* 'FRS - data read vx.Rmd' - provides the basic example; 
* other .Rmd files show different applications.

## Getting the FRS/HBAI data
Data can be downloaded from the UKDS, subject to licence conditions. We use the .sav versions (SPSSx). For each year, separate FRS files store information on the household, the benefit unit and individuals (adults or children). Other files contain information for specific groups (e.g. renters). HBAI data are provided in files covering groups of three years. These contain income and other financial information (e.g. housing costs) uprated to remove inflation. Details on how to arrange in these input data provided in the .Rmd file. 

## Rmd file
The .Rmd file reads in data from given group of '.sav' files (e.g. 'househol.sav' or 'adult.sav') for a given group of years. It is designed to identify problems with variables where the variable format ('class') changes between years, e.g. from numeric to factor. Where this occurs, the non-numeric versions are given a new name (with suffix to identify class e.g. '_factor'). This means data from different years can be combined; otherwise R throws an error trying to combine data of different classes in the same variable. The different variables can be merged later if desired. The function also stores the labels (levels) for every variable in every year so they can be checked for consistency between years at a later point and reconciled if necessary. 

The function returns a list containing: 

* one data frame with the data for all years for that group of .sav files; 
* one data frame with information on each variable in the previous data frame, capturing type or class in each year as well as any labels for the factors; there are flags to indicate whether type/class changes and whether factor levels are the same in all years; 
* one list containing each of the individual data frames read in from the .sav files (mainly for debugging so not stored).

These elements then need to be combined by the user. 
