PM566-assignment1
================
Leona Ma

\#Step1 Given the formulated question from the assignment description,
you will now conduct EDA Checklist items 2-4. First, download 2004 and
2019 data for all sites in California from the EPA Air Quality Data
website. Read in the data using data.table(). For each of the two
datasets, check the dimensions, headers, footers, variable names and
variable types. Check for any data issues, particularly in the key
variable we are analyzing. Make sure you write up a summary of all of
your findings.

## Reading in the datas

``` r
library(data.table)
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.2     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::between()   masks data.table::between()
    ## x dplyr::filter()    masks stats::filter()
    ## x dplyr::first()     masks data.table::first()
    ## x dplyr::lag()       masks stats::lag()
    ## x dplyr::last()      masks data.table::last()
    ## x purrr::transpose() masks data.table::transpose()

``` r
EDA04 <- data.table::fread("2004.csv")
EDA19 <- data.table::fread("2019.csv")
```

## Checking dimentions

``` r
dim(EDA04)
```

    ## [1] 19233    20

``` r
dim(EDA19)
```

    ## [1] 53086    20

## Checking headers

``` r
head(EDA04)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Date"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Source"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Site ID"],"name":[3],"type":["int"],"align":["right"]},{"label":["POC"],"name":[4],"type":["int"],"align":["right"]},{"label":["Daily Mean PM2.5 Concentration"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["UNITS"],"name":[6],"type":["chr"],"align":["left"]},{"label":["DAILY_AQI_VALUE"],"name":[7],"type":["int"],"align":["right"]},{"label":["Site Name"],"name":[8],"type":["chr"],"align":["left"]},{"label":["DAILY_OBS_COUNT"],"name":[9],"type":["int"],"align":["right"]},{"label":["PERCENT_COMPLETE"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["AQS_PARAMETER_CODE"],"name":[11],"type":["int"],"align":["right"]},{"label":["AQS_PARAMETER_DESC"],"name":[12],"type":["chr"],"align":["left"]},{"label":["CBSA_CODE"],"name":[13],"type":["int"],"align":["right"]},{"label":["CBSA_NAME"],"name":[14],"type":["chr"],"align":["left"]},{"label":["STATE_CODE"],"name":[15],"type":["int"],"align":["right"]},{"label":["STATE"],"name":[16],"type":["chr"],"align":["left"]},{"label":["COUNTY_CODE"],"name":[17],"type":["int"],"align":["right"]},{"label":["COUNTY"],"name":[18],"type":["chr"],"align":["left"]},{"label":["SITE_LATITUDE"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["SITE_LONGITUDE"],"name":[20],"type":["dbl"],"align":["right"]}],"data":[{"1":"01/01/2004","2":"AQS","3":"60010007","4":"1","5":"11.0","6":"ug/m3 LC","7":"46","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/02/2004","2":"AQS","3":"60010007","4":"1","5":"12.2","6":"ug/m3 LC","7":"51","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/03/2004","2":"AQS","3":"60010007","4":"1","5":"16.5","6":"ug/m3 LC","7":"60","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/04/2004","2":"AQS","3":"60010007","4":"1","5":"19.5","6":"ug/m3 LC","7":"67","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/05/2004","2":"AQS","3":"60010007","4":"1","5":"11.5","6":"ug/m3 LC","7":"48","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/06/2004","2":"AQS","3":"60010007","4":"1","5":"32.5","6":"ug/m3 LC","7":"94","8":"Livermore","9":"1","10":"100","11":"88502","12":"Acceptable PM2.5 AQI & Speciation Mass","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
head(EDA19)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Date"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Source"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Site ID"],"name":[3],"type":["int"],"align":["right"]},{"label":["POC"],"name":[4],"type":["int"],"align":["right"]},{"label":["Daily Mean PM2.5 Concentration"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["UNITS"],"name":[6],"type":["chr"],"align":["left"]},{"label":["DAILY_AQI_VALUE"],"name":[7],"type":["int"],"align":["right"]},{"label":["Site Name"],"name":[8],"type":["chr"],"align":["left"]},{"label":["DAILY_OBS_COUNT"],"name":[9],"type":["int"],"align":["right"]},{"label":["PERCENT_COMPLETE"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["AQS_PARAMETER_CODE"],"name":[11],"type":["int"],"align":["right"]},{"label":["AQS_PARAMETER_DESC"],"name":[12],"type":["chr"],"align":["left"]},{"label":["CBSA_CODE"],"name":[13],"type":["int"],"align":["right"]},{"label":["CBSA_NAME"],"name":[14],"type":["chr"],"align":["left"]},{"label":["STATE_CODE"],"name":[15],"type":["int"],"align":["right"]},{"label":["STATE"],"name":[16],"type":["chr"],"align":["left"]},{"label":["COUNTY_CODE"],"name":[17],"type":["int"],"align":["right"]},{"label":["COUNTY"],"name":[18],"type":["chr"],"align":["left"]},{"label":["SITE_LATITUDE"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["SITE_LONGITUDE"],"name":[20],"type":["dbl"],"align":["right"]}],"data":[{"1":"01/01/2019","2":"AQS","3":"60010007","4":"3","5":"5.7","6":"ug/m3 LC","7":"24","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/02/2019","2":"AQS","3":"60010007","4":"3","5":"11.9","6":"ug/m3 LC","7":"50","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/03/2019","2":"AQS","3":"60010007","4":"3","5":"20.1","6":"ug/m3 LC","7":"68","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/04/2019","2":"AQS","3":"60010007","4":"3","5":"28.8","6":"ug/m3 LC","7":"86","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/05/2019","2":"AQS","3":"60010007","4":"3","5":"11.2","6":"ug/m3 LC","7":"47","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"},{"1":"01/06/2019","2":"AQS","3":"60010007","4":"3","5":"2.7","6":"ug/m3 LC","7":"11","8":"Livermore","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"41860","14":"San Francisco-Oakland-Hayward, CA","15":"6","16":"California","17":"1","18":"Alameda","19":"37.68753","20":"-121.7842"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

## Checking footers

``` r
tail(EDA04)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Date"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Source"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Site ID"],"name":[3],"type":["int"],"align":["right"]},{"label":["POC"],"name":[4],"type":["int"],"align":["right"]},{"label":["Daily Mean PM2.5 Concentration"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["UNITS"],"name":[6],"type":["chr"],"align":["left"]},{"label":["DAILY_AQI_VALUE"],"name":[7],"type":["int"],"align":["right"]},{"label":["Site Name"],"name":[8],"type":["chr"],"align":["left"]},{"label":["DAILY_OBS_COUNT"],"name":[9],"type":["int"],"align":["right"]},{"label":["PERCENT_COMPLETE"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["AQS_PARAMETER_CODE"],"name":[11],"type":["int"],"align":["right"]},{"label":["AQS_PARAMETER_DESC"],"name":[12],"type":["chr"],"align":["left"]},{"label":["CBSA_CODE"],"name":[13],"type":["int"],"align":["right"]},{"label":["CBSA_NAME"],"name":[14],"type":["chr"],"align":["left"]},{"label":["STATE_CODE"],"name":[15],"type":["int"],"align":["right"]},{"label":["STATE"],"name":[16],"type":["chr"],"align":["left"]},{"label":["COUNTY_CODE"],"name":[17],"type":["int"],"align":["right"]},{"label":["COUNTY"],"name":[18],"type":["chr"],"align":["left"]},{"label":["SITE_LATITUDE"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["SITE_LONGITUDE"],"name":[20],"type":["dbl"],"align":["right"]}],"data":[{"1":"12/14/2004","2":"AQS","3":"61131003","4":"1","5":"11","6":"ug/m3 LC","7":"46","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/17/2004","2":"AQS","3":"61131003","4":"1","5":"16","6":"ug/m3 LC","7":"59","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/20/2004","2":"AQS","3":"61131003","4":"1","5":"17","6":"ug/m3 LC","7":"61","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/23/2004","2":"AQS","3":"61131003","4":"1","5":"9","6":"ug/m3 LC","7":"38","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/26/2004","2":"AQS","3":"61131003","4":"1","5":"24","6":"ug/m3 LC","7":"76","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/29/2004","2":"AQS","3":"61131003","4":"1","5":"9","6":"ug/m3 LC","7":"38","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

``` r
tail(EDA19)
```

<div data-pagedtable="false">

<script data-pagedtable-source type="application/json">
{"columns":[{"label":["Date"],"name":[1],"type":["chr"],"align":["left"]},{"label":["Source"],"name":[2],"type":["chr"],"align":["left"]},{"label":["Site ID"],"name":[3],"type":["int"],"align":["right"]},{"label":["POC"],"name":[4],"type":["int"],"align":["right"]},{"label":["Daily Mean PM2.5 Concentration"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["UNITS"],"name":[6],"type":["chr"],"align":["left"]},{"label":["DAILY_AQI_VALUE"],"name":[7],"type":["int"],"align":["right"]},{"label":["Site Name"],"name":[8],"type":["chr"],"align":["left"]},{"label":["DAILY_OBS_COUNT"],"name":[9],"type":["int"],"align":["right"]},{"label":["PERCENT_COMPLETE"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["AQS_PARAMETER_CODE"],"name":[11],"type":["int"],"align":["right"]},{"label":["AQS_PARAMETER_DESC"],"name":[12],"type":["chr"],"align":["left"]},{"label":["CBSA_CODE"],"name":[13],"type":["int"],"align":["right"]},{"label":["CBSA_NAME"],"name":[14],"type":["chr"],"align":["left"]},{"label":["STATE_CODE"],"name":[15],"type":["int"],"align":["right"]},{"label":["STATE"],"name":[16],"type":["chr"],"align":["left"]},{"label":["COUNTY_CODE"],"name":[17],"type":["int"],"align":["right"]},{"label":["COUNTY"],"name":[18],"type":["chr"],"align":["left"]},{"label":["SITE_LATITUDE"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["SITE_LONGITUDE"],"name":[20],"type":["dbl"],"align":["right"]}],"data":[{"1":"11/11/2019","2":"AQS","3":"61131003","4":"1","5":"13.5","6":"ug/m3 LC","7":"54","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"11/17/2019","2":"AQS","3":"61131003","4":"1","5":"18.1","6":"ug/m3 LC","7":"64","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"11/29/2019","2":"AQS","3":"61131003","4":"1","5":"12.5","6":"ug/m3 LC","7":"52","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/17/2019","2":"AQS","3":"61131003","4":"1","5":"23.8","6":"ug/m3 LC","7":"76","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/23/2019","2":"AQS","3":"61131003","4":"1","5":"1.0","6":"ug/m3 LC","7":"4","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"},{"1":"12/29/2019","2":"AQS","3":"61131003","4":"1","5":"9.1","6":"ug/m3 LC","7":"38","8":"Woodland-Gibson Road","9":"1","10":"100","11":"88101","12":"PM2.5 - Local Conditions","13":"40900","14":"Sacramento--Roseville--Arden-Arcade, CA","15":"6","16":"California","17":"113","18":"Yolo","19":"38.66121","20":"-121.7327"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>

</div>

\#\#Checking variable names and variables types

``` r
str(EDA04)
```

    ## Classes 'data.table' and 'data.frame':   19233 obs. of  20 variables:
    ##  $ Date                          : chr  "01/01/2004" "01/02/2004" "01/03/2004" "01/04/2004" ...
    ##  $ Source                        : chr  "AQS" "AQS" "AQS" "AQS" ...
    ##  $ Site ID                       : int  60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 ...
    ##  $ POC                           : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ Daily Mean PM2.5 Concentration: num  11 12.2 16.5 19.5 11.5 32.5 15.5 29.9 21 16.9 ...
    ##  $ UNITS                         : chr  "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" ...
    ##  $ DAILY_AQI_VALUE               : int  46 51 60 67 48 94 58 88 70 61 ...
    ##  $ Site Name                     : chr  "Livermore" "Livermore" "Livermore" "Livermore" ...
    ##  $ DAILY_OBS_COUNT               : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ PERCENT_COMPLETE              : num  100 100 100 100 100 100 100 100 100 100 ...
    ##  $ AQS_PARAMETER_CODE            : int  88502 88502 88502 88502 88502 88502 88502 88502 88502 88502 ...
    ##  $ AQS_PARAMETER_DESC            : chr  "Acceptable PM2.5 AQI & Speciation Mass" "Acceptable PM2.5 AQI & Speciation Mass" "Acceptable PM2.5 AQI & Speciation Mass" "Acceptable PM2.5 AQI & Speciation Mass" ...
    ##  $ CBSA_CODE                     : int  41860 41860 41860 41860 41860 41860 41860 41860 41860 41860 ...
    ##  $ CBSA_NAME                     : chr  "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" ...
    ##  $ STATE_CODE                    : int  6 6 6 6 6 6 6 6 6 6 ...
    ##  $ STATE                         : chr  "California" "California" "California" "California" ...
    ##  $ COUNTY_CODE                   : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ COUNTY                        : chr  "Alameda" "Alameda" "Alameda" "Alameda" ...
    ##  $ SITE_LATITUDE                 : num  37.7 37.7 37.7 37.7 37.7 ...
    ##  $ SITE_LONGITUDE                : num  -122 -122 -122 -122 -122 ...
    ##  - attr(*, ".internal.selfref")=<externalptr>

``` r
str(EDA19)
```

    ## Classes 'data.table' and 'data.frame':   53086 obs. of  20 variables:
    ##  $ Date                          : chr  "01/01/2019" "01/02/2019" "01/03/2019" "01/04/2019" ...
    ##  $ Source                        : chr  "AQS" "AQS" "AQS" "AQS" ...
    ##  $ Site ID                       : int  60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 60010007 ...
    ##  $ POC                           : int  3 3 3 3 3 3 3 3 3 3 ...
    ##  $ Daily Mean PM2.5 Concentration: num  5.7 11.9 20.1 28.8 11.2 2.7 2.8 7 3.1 7.1 ...
    ##  $ UNITS                         : chr  "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" "ug/m3 LC" ...
    ##  $ DAILY_AQI_VALUE               : int  24 50 68 86 47 11 12 29 13 30 ...
    ##  $ Site Name                     : chr  "Livermore" "Livermore" "Livermore" "Livermore" ...
    ##  $ DAILY_OBS_COUNT               : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ PERCENT_COMPLETE              : num  100 100 100 100 100 100 100 100 100 100 ...
    ##  $ AQS_PARAMETER_CODE            : int  88101 88101 88101 88101 88101 88101 88101 88101 88101 88101 ...
    ##  $ AQS_PARAMETER_DESC            : chr  "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" "PM2.5 - Local Conditions" ...
    ##  $ CBSA_CODE                     : int  41860 41860 41860 41860 41860 41860 41860 41860 41860 41860 ...
    ##  $ CBSA_NAME                     : chr  "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" "San Francisco-Oakland-Hayward, CA" ...
    ##  $ STATE_CODE                    : int  6 6 6 6 6 6 6 6 6 6 ...
    ##  $ STATE                         : chr  "California" "California" "California" "California" ...
    ##  $ COUNTY_CODE                   : int  1 1 1 1 1 1 1 1 1 1 ...
    ##  $ COUNTY                        : chr  "Alameda" "Alameda" "Alameda" "Alameda" ...
    ##  $ SITE_LATITUDE                 : num  37.7 37.7 37.7 37.7 37.7 ...
    ##  $ SITE_LONGITUDE                : num  -122 -122 -122 -122 -122 ...
    ##  - attr(*, ".internal.selfref")=<externalptr>

\#\#Checking key variables

``` r
summary(EDA04$`Daily Mean PM2.5 Concentration`)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   -0.10    6.00   10.10   13.12   16.30  251.00

``` r
summary(EDA04$DAILY_AQI_VALUE)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00   25.00   42.00   46.33   60.00  301.00

``` r
summary(EDA19$`Daily Mean PM2.5 Concentration`)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  -2.200   4.000   6.500   7.734   9.900 120.900

``` r
summary(EDA19$DAILY_AQI_VALUE)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00   17.00   27.00   30.56   41.00  185.00

There is a data issue, which is that some values in “Daily Mean PM2.5
Concentration” data from both years are less than 0.

``` r
EDA_04 <- EDA04[`Daily Mean PM2.5 Concentration` >0]
EDA_19 <- EDA19[`Daily Mean PM2.5 Concentration` >0]
```

\#\#Getting summary statistics of data

``` r
summary(EDA_04$`Daily Mean PM2.5 Concentration`)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.10    6.00   10.10   13.13   16.30  251.00

``` r
summary(EDA_04$DAILY_AQI_VALUE)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00   25.00   42.00   46.35   60.00  301.00

After deleting implausible values, the minimum value of daily mean PM2.5
concentration in 2004 is 0.10 ug/m3 LC, and the maximum value is 251.00
ug/m3 LC. The minimum daily AQI value is 0.00 in 2004, and the maximun
value is 301.00.

``` r
summary(EDA_19$`Daily Mean PM2.5 Concentration`)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.10    4.10    6.50    7.79   10.00  120.90

``` r
summary(EDA_19$DAILY_AQI_VALUE)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##    0.00   17.00   27.00   30.76   42.00  185.00

After deleting implausible values, the minimum value of daily mean PM2.5
concentration in 2019 is 0.10 ug/m3 LC, and the maximum value is 120.90
ug/m3 LC. The minimum daily AQI value is 0.00 in 2019, and the maximum
value is 185.00.

According to the decrease of maximum value of daily mean PM2.5
concentration and daily AQI value from 2004 to 2019, we can have a basic
idea that air pollution had been improved a lot in these 15 years.

\#Step2 Combine the two years of data into one data frame. Use the Date
variable to create a new column for year, which will serve as an
identifier. Change the names of the key variables so that they are
easier to refer to in your code.

\#\#Combine the two years of data into one data frame

``` r
EDA <- rbind(EDA04, EDA19)
```

\#\#Creating new column

``` r
EDA$Years <- format(as.POSIXct(EDA$Date, format = "%m/%d/%Y"), format = "%Y")
```

\#\#Rename key variables

``` r
EDA <- rename(EDA, PM2.5 = `Daily Mean PM2.5 Concentration`, AQI = DAILY_AQI_VALUE)
```

\#Step3 Create a basic map in leaflet() that shows the locations of the
sites (make sure to use different colors for each year). Summarize the
spatial distribution of the monitoring sites.

``` r
library(leaflet)

tem.pal <- colorFactor(topo.colors(4), domain = EDA$Years)
leaflet(EDA) %>% 
  addTiles() %>%
  addCircles (lat = ~SITE_LATITUDE, lng = ~SITE_LONGITUDE, color = ~tem.pal(Years),
               label = ~Years, 
               opacity=0.01, fillOpacity = 0.01, radius = 500) %>%
  addLegend('bottomleft', pal= tem.pal, values = EDA$Years,
             title ='years', opacity=1)
```


summary:According to the plot, the sites are overlapped with each other
in 2004 and 2019. So, the detections happened basically in the same
places.

\#Step4 Check for any missing or implausible values of PM in the
combined dataset. Explore the proportions of each and provide a summary
of any temporal patterns you see in these observations.

``` r
mean(is.na(EDA$PM2.5))
```

    ## [1] 0

``` r
mean(EDA$PM2.5<0)
```

    ## [1] 0.003913218

There is no missing value in this dataset. There are some implausible
values that are negative, which have a proportion of 0.4%.

\#Step5 Explore the main question of interest at three different spatial
levels. Create exploratory plots (e.g. boxplots, histograms, line plots)
and summary statistics that best suit each level of data. Be sure to
write up explanations of what you observe in these data.

``` r
library(tidyverse)
library(data.table)
library(ggplot2)
```

\#\#state

``` r
ggplot(EDA)+
  geom_boxplot(mapping=(aes(x=Years, y=PM2.5)))
```

![](Assignment1-Leona_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(EDA)+
  geom_histogram(mapping=(aes(x=PM2.5, color=Years)), breaks=seq(0, 80, by=3))
```

![](Assignment1-Leona_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

\#\#county

``` r
library(dplyr)
county <- group_by(EDA, Years, COUNTY) %>% summarize(PM2.5 = mean(PM2.5, na.rm = TRUE))
```

    ## `summarise()` has grouped output by 'Years'. You can override using the `.groups` argument.

``` r
qplot(xyear, PM2.5, data = mutate(county, xyear = as.numeric(as.character(Years))), 
       color = factor(COUNTY), 
       geom = c("point", "line"))
```

![](Assignment1-Leona_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

county&lt;- group\_by(pm2.5, year, COUNTY) %&gt;% summarize(pm25 =
mean(pm25, na.rm = TRUE)) qplot(xyear, pm25, data = mutate(county, xyear
= as.numeric(as.character(year))), color = factor(COUNTY), geom =
c(“point”, “line”)) \#\#site in Los Angeles

``` r
LA<- EDA[COUNTY_CODE == 37]
sites<- group_by(LA, Years, "Site Name") %>% summarize(PM2.5 = mean(PM2.5, na.rm = TRUE))
```

    ## `summarise()` has grouped output by 'Years'. You can override using the `.groups` argument.

``` r
qplot(xyear, PM2.5, data = mutate(sites, xyear = as.numeric(as.character(Years))), 
    color = factor("Site Name"), 
    geom = c("point", "line"))
```

![](Assignment1-Leona_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

Overall, from all of this levels, we can see that the daily mean value
of PM2.5 has been decreased a lot.
