# Getting and Cleaning Data Project

This repo contains project code for `Getting and Cleaning Data` course given
by John Hopkins university on Coursera.

## Script

The script contains a function `run.analysis()` that performs the
actual job:
 * reads train and test data sets and merges them
 * processes the merged data set (extract the relevant variables,
   adds descriptive activity names, etc.)
 * writes the merged data set to `rawdata.csv`
 * generates the tidy data set
 * writes the tidy data set to `tidydata.csv`
 * returns the tidy data set

If you've a Samsung data available in the current directory, just run:

```R
source('./run_analysis.R')
run.analysis() # invoke the actual function
```

Otherwise, you can use `download.data()` function provided in the script.
The function will download the data archive and extract it.
After that you can run `run.analysis()`. The full code:

```R
source('./run_analysis.R')
download.data() # download samsung data and unzip it
run.analysis() # invoke the actual function
```

If you don't want to use `download.data()`, you should download the samsung data
manually, unzip it in the current directory and then run:

```R
source('./run_analysis.R')
run.analysis() # invoke the actual function
```

*Note*: In all the examples above, I assume that the script file
`run_analysis.R` resides in the current working directory. If it does not,
you should provide the correct path to the file to source it.

## Data sets

### Raw data set

In order to create a raw data set, the following regular expression was used:
`-(mean|std)[(]`. I.e. all variables containing `-mean(` or `-std(` in their
names were filtered.

Totally, the raw data set contains 68 variables:

 * `subject` - An identifier of the subject who carried out the experiment.
 * `label` - An activity label.

Plus 66 filtered features mined as described below.

The features selected for this database come from the accelerometer and
gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals
(prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they
were filtered using a median filter and a 3rd order low pass Butterworth filter
with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration
signal was then separated into body and gravity acceleration signals
(tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter
with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in
time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the
magnitude of these three-dimensional signals were calculated using the Euclidean
norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag,
tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals
producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag,
fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain
signals). 

These signals were used to estimate variables of the feature vector for each
pattern:  
`-XYZ` is used to denote 3-axial signals in the X, Y and Z directions.
 * `tBodyAcc-XYZ`
 * `tGravityAcc-XYZ`
 * `tBodyAccJerk-XYZ`
 * `tBodyGyro-XYZ`
 * `tBodyGyroJerk-XYZ`
 * `tBodyAccMag`
 * `tGravityAccMag`
 * `tBodyAccJerkMag`
 * `tBodyGyroMag`
 * `tBodyGyroJerkMag`
 * `fBodyAcc-XYZ`
 * `fBodyAccJerk-XYZ`
 * `fBodyGyro-XYZ`
 * `fBodyAccMag`
 * `fBodyAccJerkMag`
 * `fBodyGyroMag`
 * `fBodyGyroJerkMag`

The set of variables that were estimated from these signals are: 
 * `mean()`: Mean value
 * `std()`: Standard deviation

### Tidy data set

Tidy data set contains the same variables as the raw does, but the variables
were renamed according to following rules:
 * `All lower case when possible` - the variables names **were not** converted
   to lower case, since it would make them unreadable.
   Instead, the variable names were converted to satisfy `camlCase` rule.
 * `Descriptive (Diagnosis versus Dx)` - the variable names are descriptive,
   so nothing special should be done.
 * `Not duplicated` - the variable names are unique, so again nothing special
   had to be done.
 * `Not have underscores or dots or white spaces` - dashes and parentheses
   were removed from variable names.

To satisfy the requirements above, the following replacements were performed:
 1. Replace `-mean` with `Mean`
 1. Replace `-std` with `Std`
 1. Remove characters `-()`
 1. Replace `BodyBody` with `Body`

### Variables in raw and tidy data set

 Raw data set | Tidy data set
 -------------|--------------
 `subject` | `subject`
 `label` | `label`
 `tBodyAcc-mean()-X` | `tBodyAccMeanX`
 `tBodyAcc-mean()-Y` | `tBodyAccMeanY`
 `tBodyAcc-mean()-Z` | `tBodyAccMeanZ`
 `tBodyAcc-std()-X` | `tBodyAccStdX`
 `tBodyAcc-std()-Y` | `tBodyAccStdY`
 `tBodyAcc-std()-Z` | `tBodyAccStdZ`
 `tGravityAcc-mean()-X` | `tGravityAccMeanX`
 `tGravityAcc-mean()-Y` | `tGravityAccMeanY`
 `tGravityAcc-mean()-Z` | `tGravityAccMeanZ`
 `tGravityAcc-std()-X` | `tGravityAccStdX`
 `tGravityAcc-std()-Y` | `tGravityAccStdY`
 `tGravityAcc-std()-Z` | `tGravityAccStdZ`
 `tBodyAccJerk-mean()-X` | `tBodyAccJerkMeanX`
 `tBodyAccJerk-mean()-Y` | `tBodyAccJerkMeanY`
 `tBodyAccJerk-mean()-Z` | `tBodyAccJerkMeanZ`
 `tBodyAccJerk-std()-X` | `tBodyAccJerkStdX`
 `tBodyAccJerk-std()-Y` | `tBodyAccJerkStdY`
 `tBodyAccJerk-std()-Z` | `tBodyAccJerkStdZ`
 `tBodyGyro-mean()-X` | `tBodyGyroMeanX`
 `tBodyGyro-mean()-Y` | `tBodyGyroMeanY`
 `tBodyGyro-mean()-Z` | `tBodyGyroMeanZ`
 `tBodyGyro-std()-X` | `tBodyGyroStdX`
 `tBodyGyro-std()-Y` | `tBodyGyroStdY`
 `tBodyGyro-std()-Z` | `tBodyGyroStdZ`
 `tBodyGyroJerk-mean()-X` | `tBodyGyroJerkMeanX`
 `tBodyGyroJerk-mean()-Y` | `tBodyGyroJerkMeanY`
 `tBodyGyroJerk-mean()-Z` | `tBodyGyroJerkMeanZ`
 `tBodyGyroJerk-std()-X` | `tBodyGyroJerkStdX`
 `tBodyGyroJerk-std()-Y` | `tBodyGyroJerkStdY`
 `tBodyGyroJerk-std()-Z` | `tBodyGyroJerkStdZ`
 `tBodyAccMag-mean()` | `tBodyAccMagMean`
 `tBodyAccMag-std()` | `tBodyAccMagStd`
 `tGravityAccMag-mean()` | `tGravityAccMagMean`
 `tGravityAccMag-std()` | `tGravityAccMagStd`
 `tBodyAccJerkMag-mean()` | `tBodyAccJerkMagMean`
 `tBodyAccJerkMag-std()` | `tBodyAccJerkMagStd`
 `tBodyGyroMag-mean()` | `tBodyGyroMagMean`
 `tBodyGyroMag-std()` | `tBodyGyroMagStd`
 `tBodyGyroJerkMag-mean()` | `tBodyGyroJerkMagMean`
 `tBodyGyroJerkMag-std()` | `tBodyGyroJerkMagStd`
 `fBodyAcc-mean()-X` | `fBodyAccMeanX`
 `fBodyAcc-mean()-Y` | `fBodyAccMeanY`
 `fBodyAcc-mean()-Z` | `fBodyAccMeanZ`
 `fBodyAcc-std()-X` | `fBodyAccStdX`
 `fBodyAcc-std()-Y` | `fBodyAccStdY`
 `fBodyAcc-std()-Z` | `fBodyAccStdZ`
 `fBodyAccJerk-mean()-X` | `fBodyAccJerkMeanX`
 `fBodyAccJerk-mean()-Y` | `fBodyAccJerkMeanY`
 `fBodyAccJerk-mean()-Z` | `fBodyAccJerkMeanZ`
 `fBodyAccJerk-std()-X` | `fBodyAccJerkStdX`
 `fBodyAccJerk-std()-Y` | `fBodyAccJerkStdY`
 `fBodyAccJerk-std()-Z` | `fBodyAccJerkStdZ`
 `fBodyGyro-mean()-X` | `fBodyGyroMeanX`
 `fBodyGyro-mean()-Y` | `fBodyGyroMeanY`
 `fBodyGyro-mean()-Z` | `fBodyGyroMeanZ`
 `fBodyGyro-std()-X` | `fBodyGyroStdX`
 `fBodyGyro-std()-Y` | `fBodyGyroStdY`
 `fBodyGyro-std()-Z` | `fBodyGyroStdZ`
 `fBodyAccMag-mean()` | `fBodyAccMagMean`
 `fBodyAccMag-std()` | `fBodyAccMagStd`
 `fBodyBodyAccJerkMag-mean()` | `fBodyAccJerkMagMean`
 `fBodyBodyAccJerkMag-std()` | `fBodyAccJerkMagStd`
 `fBodyBodyGyroMag-mean()` | `fBodyGyroMagMean`
 `fBodyBodyGyroMag-std()` | `fBodyGyroMagStd`
 `fBodyBodyGyroJerkMag-mean()` | `fBodyGyroJerkMagMean`
 `fBodyBodyGyroJerkMag-std()` | `fBodyGyroJerkMagStd`

