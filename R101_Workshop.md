R101 Exercises
================

The following exercises accompany the R101-Workshop presentation and are
intended to reinforce the learning outcomes. You are therefore
encouraged to follow along using RStudio desktop or RStudio Cloud
instance.

To follow along, type the Inputs (commands) highlighted grey into the
**editor pane** and compare the results with the expected outputs (text
highlighted grey and preceded by **\#**).

At the end of this workshop you will:

  - be familiar with the RStudio working environment.
  - have a good understanding of R data structures and datatypes.
  - be familiar with common base R functions.
  - be able to generate common data structures (vectors and dataframes).
  - be able to perform vectorised operations on common data structures.
  - be able to use common input and output functions

## R Workspace

Open [RStudio IDE](https://www.rstudio.com/products/rstudio/) on your
desktop or alternatively use [RStudio
Cloud](https://www.https://rstudio.cloud/)

  - Create a new R Script from the menu bar: ‘File \> New File \> R
    Script’.

  - Save the new R Script file to a new directory location. Example file
    path: R Workshops/R101/Exercises/Exercise\_1.R

  - Using the editor window, enter the following command, select the
    line and click **Run** or press **CTRL + ENTER** to execute the
    command.

<!-- end list -->

``` r
   x <- 24
```

  - Type <i>‘x’</i> at the command prompt in the console window and hit
    **Return** to print the output.

<!-- end list -->

``` r
   x 
```

    # [1] 24

## Data Input and Output

R can import data from flat files, from Microsoft Excel and Access, from
specialty formats like XML, and from a variety of relational database
systems amongst others.

However, for the purpose of this workshop you will focus on importing
data from flat files, MS Excel and MS SQL databases.

# Importing data from a **.csv** file.

> You will require the readr package. If it isn’t already installed, the
> package can be installed by running the command:
> *install.packages(‘readr’)* from the console.

> To begin, type *library(readr)* in the editor pane and click **Run**
> to load the package to your session.

> Next, add the following command on a new line in the editor pane and
> click **Run** to import and assign the csv data to a new variable in
> your R session environment.

    csvData <- read_csv('/path/to/csv_file.csv')

## Data Generation

Commonly used data generation functions include: c(), seq(), rep() and
data.frame(). Occasionally we may also use list() and array() to
generate data.

**c()** - aka the combine function creates a (column) vector.

``` r
   a <- c(1:5,8,6,7)
   a
```

    ## [1] 1 2 3 4 5 8 6 7

**seq(*from*, *to*)** - generates a sequence. Optional arguments are
‘*by* =’ to specify increment; ‘*length* =’ specifies desired length.
The argument ‘*along* =’ can also be used to generate a sequence (used
in loops to create ID for each element in *x*).

``` r
    seq(1, 5, by=0.5)
```

    ## [1] 1.0 1.5 2.0 2.5 3.0 3.5 4.0 4.5 5.0

``` r
    seq(1,100, length=5)
```

    ## [1]   1.00  25.75  50.50  75.25 100.00

``` r
    seq(along= c(10,7,23,19))
```

    ## [1] 1 2 3 4

**rep(*x*, *times*)** - creates a sequence that repeats x a specified
number of times. Optional argument *each =* signals to repeat first over
each element of x a given number of times.

``` r
    rep(c(1,2,3), 4)
```

    ##  [1] 1 2 3 1 2 3 1 2 3 1 2 3

``` r
    rep(c(1,2,3), each=4)
```

    ##  [1] 1 1 1 1 2 2 2 2 3 3 3 3

**data.frame()** - creates a dataframe of named or unnamed arguments.

  - You will create the sample dataframe below:
    ![](R101_Workshop_files/sample_dataframe.png)

<!-- end list -->

``` r
# 1. First, create the individual (columns) vectors
    PatientID <- c(1:4)
    AdmDate <- c("2009-10-15", "2009-11-01", "2009-10-21", "2009-10-28")
    Age <- c(25, 34, 28, 52)
    Diabetes <- c("Type1", "Type2", "Type1", "Type1")
    Status <- c("Poor", "Improved", "Excellent", "Poor")

# 2. Combine the vectors to form the sample dataframe
    Inpatients_1 <- data.frame(PatientID, AdmDate, Age, Diabetes, Status)
    Inpatients_1
```

    ##   PatientID    AdmDate Age Diabetes    Status
    ## 1         1 2009-10-15  25    Type1      Poor
    ## 2         2 2009-11-01  34    Type2  Improved
    ## 3         3 2009-10-21  28    Type1 Excellent
    ## 4         4 2009-10-28  52    Type1      Poor

``` r
# 3. Create a second dataframe matching the first by data type and length    
    Inpatients_2 <- data.frame(PatientID=c(5:7), 
                               AdmDate=c("2009-10-13","2009-10-09","2001-10-12"),
                               Age=c(30, 55, 27),
                               Diabetes=c("Type2", "Type1", "Type1"),
                               Status=c("Poor", "Improved", "Improved"))
    Inpatients_2
```

    ##   PatientID    AdmDate Age Diabetes   Status
    ## 1         5 2009-10-13  30    Type2     Poor
    ## 2         6 2009-10-09  55    Type1 Improved
    ## 3         7 2001-10-12  27    Type1 Improved

``` r
# 4. Combine the **rows** from two inpatient datasets into a single dataframe using the **rbind()** function.
    All_patients <- rbind(Inpatients_1, Inpatients_2)
    All_patients
```

    ##   PatientID    AdmDate Age Diabetes    Status
    ## 1         1 2009-10-15  25    Type1      Poor
    ## 2         2 2009-11-01  34    Type2  Improved
    ## 3         3 2009-10-21  28    Type1 Excellent
    ## 4         4 2009-10-28  52    Type1      Poor
    ## 5         5 2009-10-13  30    Type2      Poor
    ## 6         6 2009-10-09  55    Type1  Improved
    ## 7         7 2001-10-12  27    Type1  Improved

``` r
# 5. Create a third dataframe named BloodTest_Results with 7 observations and 3 columns: **PatientID**, **RequestDate** and **BloodGlucose**.
    BloodTest_Results <- data.frame(PatientID=c(1:7),
        RequestDate=seq(from=as.Date('2009-10-09'),to=as.Date('2009-10-15'),by='day'),
        BloodGlucose=rnorm(7,mean=6.5, sd=1))
      
    
    BloodTest_Results
```

    ##   PatientID RequestDate BloodGlucose
    ## 1         1  2009-10-09     5.292934
    ## 2         2  2009-10-10     6.777429
    ## 3         3  2009-10-11     7.584441
    ## 4         4  2009-10-12     4.154302
    ## 5         5  2009-10-13     6.929125
    ## 6         6  2009-10-14     7.006056
    ## 7         7  2009-10-15     5.925260

``` r
# 6. Merge the **columns** from blood test results dataframe with the Inpatients dataframe using the **cbind()** function.
    
    patientData <- cbind(All_patients, BloodTest_Results)
    
    patientData
```

    ##   PatientID    AdmDate Age Diabetes    Status PatientID RequestDate
    ## 1         1 2009-10-15  25    Type1      Poor         1  2009-10-09
    ## 2         2 2009-11-01  34    Type2  Improved         2  2009-10-10
    ## 3         3 2009-10-21  28    Type1 Excellent         3  2009-10-11
    ## 4         4 2009-10-28  52    Type1      Poor         4  2009-10-12
    ## 5         5 2009-10-13  30    Type2      Poor         5  2009-10-13
    ## 6         6 2009-10-09  55    Type1  Improved         6  2009-10-14
    ## 7         7 2001-10-12  27    Type1  Improved         7  2009-10-15
    ##   BloodGlucose
    ## 1     5.292934
    ## 2     6.777429
    ## 3     7.584441
    ## 4     4.154302
    ## 5     6.929125
    ## 6     7.006056
    ## 7     5.925260

``` r
# 7. Create a new (column) vector named **Discharge** to represent patient discharge dates, derived from AdmDate.
    
    Discharge <- as.Date(patientData$AdmDate) + sample(1:5,7,replace=T)
    
# 8. Add a new (column) vector named **DisDate** to the results dataframe using the Discharge vector.
    
    patientData$DisDate <- Discharge
    patientData
```

    ##   PatientID    AdmDate Age Diabetes    Status PatientID RequestDate
    ## 1         1 2009-10-15  25    Type1      Poor         1  2009-10-09
    ## 2         2 2009-11-01  34    Type2  Improved         2  2009-10-10
    ## 3         3 2009-10-21  28    Type1 Excellent         3  2009-10-11
    ## 4         4 2009-10-28  52    Type1      Poor         4  2009-10-12
    ## 5         5 2009-10-13  30    Type2      Poor         5  2009-10-13
    ## 6         6 2009-10-09  55    Type1  Improved         6  2009-10-14
    ## 7         7 2001-10-12  27    Type1  Improved         7  2009-10-15
    ##   BloodGlucose    DisDate
    ## 1     5.292934 2009-10-17
    ## 2     6.777429 2009-11-05
    ## 3     7.584441 2009-10-25
    ## 4     4.154302 2009-11-01
    ## 5     6.929125 2009-10-18
    ## 6     7.006056 2009-10-13
    ## 7     5.925260 2001-10-15

**list()** - creates a list of named or unnamed arguments with indexing
rule: 1 to *n* including 1 an *n*

``` r
    l <- list(a=c(1,2), b="Hello World", c=-3+2i , d=data.frame(A=letters[1:3],B=1:3))
    l
```

    ## $a
    ## [1] 1 2
    ## 
    ## $b
    ## [1] "Hello World"
    ## 
    ## $c
    ## [1] -3+2i
    ## 
    ## $d
    ##   A B
    ## 1 a 1
    ## 2 b 2
    ## 3 c 3

``` r
    # Note Complex Number -3 + 2i
```

Like vectors, use *$* to call each member in the list, and *\[\[\]\]* to
call the elements corresponding to specific index.

``` r
    l$a[[2]]
```

    ## [1] 2

``` r
    l$b
```

    ## [1] "Hello World"

``` r
    l$d[[1]]
```

    ## [1] a b c
    ## Levels: a b c

## Data Inspection

``` r
# **names(*object*)** - output the names of (columns) vectors in an object
    names(patientData)
```

    ## [1] "PatientID"    "AdmDate"      "Age"          "Diabetes"     "Status"      
    ## [6] "PatientID"    "RequestDate"  "BloodGlucose" "DisDate"

``` r
# **dim(*object*)** - output the dimensions of an object
    dim(patientData)
```

    ## [1] 7 9

``` r
# **length(*object*)** - number of elements in object  
    length(patientData)
```

    ## [1] 9

``` r
# **nrow(object)**  - number of rows present in object
    nrow(patientData)
```

    ## [1] 7

``` r
# **ncol()** - number of columns present in object
    ncol(patientData)
```

    ## [1] 9

``` r
# **str()** - structure of an object object
    str(patientData)
```

    ## 'data.frame':    7 obs. of  9 variables:
    ##  $ PatientID   : int  1 2 3 4 5 6 7
    ##  $ AdmDate     : Factor w/ 7 levels "2009-10-15","2009-10-21",..: 1 4 2 3 7 6 5
    ##  $ Age         : num  25 34 28 52 30 55 27
    ##  $ Diabetes    : Factor w/ 2 levels "Type1","Type2": 1 2 1 1 2 1 1
    ##  $ Status      : Factor w/ 3 levels "Excellent","Improved",..: 3 2 1 3 3 2 2
    ##  $ PatientID   : int  1 2 3 4 5 6 7
    ##  $ RequestDate : Date, format: "2009-10-09" "2009-10-10" ...
    ##  $ BloodGlucose: num  5.29 6.78 7.58 4.15 6.93 ...
    ##  $ DisDate     : Date, format: "2009-10-17" "2009-11-05" ...

``` r
# **summary()
    summary(patientData)
```

    ##    PatientID         AdmDate       Age         Diabetes       Status 
    ##  Min.   :1.0   2009-10-15:1   Min.   :25.00   Type1:5   Excellent:1  
    ##  1st Qu.:2.5   2009-10-21:1   1st Qu.:27.50   Type2:2   Improved :3  
    ##  Median :4.0   2009-10-28:1   Median :30.00             Poor     :3  
    ##  Mean   :4.0   2009-11-01:1   Mean   :35.86                          
    ##  3rd Qu.:5.5   2001-10-12:1   3rd Qu.:43.00                          
    ##  Max.   :7.0   2009-10-09:1   Max.   :55.00                          
    ##                2009-10-13:1                                          
    ##    PatientID    RequestDate          BloodGlucose      DisDate          
    ##  Min.   :1.0   Min.   :2009-10-09   Min.   :4.154   Min.   :2001-10-15  
    ##  1st Qu.:2.5   1st Qu.:2009-10-10   1st Qu.:5.609   1st Qu.:2009-10-15  
    ##  Median :4.0   Median :2009-10-12   Median :6.777   Median :2009-10-18  
    ##  Mean   :4.0   Mean   :2009-10-12   Mean   :6.239   Mean   :2008-08-30  
    ##  3rd Qu.:5.5   3rd Qu.:2009-10-13   3rd Qu.:6.968   3rd Qu.:2009-10-28  
    ##  Max.   :7.0   Max.   :2009-10-15   Max.   :7.584   Max.   :2009-11-05  
    ## 

## Data Selection

Vector Indexing in R

``` r
# Use x[n] to return the Nth element.
patientData[1]
```

    ##   PatientID
    ## 1         1
    ## 2         2
    ## 3         3
    ## 4         4
    ## 5         5
    ## 6         6
    ## 7         7

``` r
# Use x[-n] to return all excluding duplicated PatientID vector.
patientData <- patientData[-6]

# Confirm that the number of columns have reduced  by 1.
dim(patientData)
```

    ## [1] 7 8

``` r
# Use x[c(index1,index2,...)] to select specific elements in a specified order
patientData <- patientData[c(1,2,8,3:7)]

# Confirm that the (column) vectors have been reordered.
names(patientData)
```

    ## [1] "PatientID"    "AdmDate"      "DisDate"      "Age"          "Diabetes"    
    ## [6] "Status"       "RequestDate"  "BloodGlucose"

``` r
# Use x[name] to select named element
patientData['PatientID']
```

    ##   PatientID
    ## 1         1
    ## 2         2
    ## 3         3
    ## 4         4
    ## 5         5
    ## 6         6
    ## 7         7

## Slicing and Extracting

You can include R code in the document as follows:

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

## Including Plots

You can also embed plots, for example:

![](R101_Workshop_files/figure-gfm/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
