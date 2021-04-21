---
title: "Code Book"
author: "Carlos Aguilar"
output: pdf_document
---
# Code Book 

The run_analysis.R script performs the data preparation and executes the 5 steps described in the course project's definition.

## Data Preparation
The data frames are assigned to variables:

+ The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ.
 
```features <- features.txt``` : 561 rows, 2 columns

+ List of activities performed and their respective labels.

```activity_labels <- activity_labels.txt``` : 6 rows, 2 columns

+ contains test data on 9 out of 30 volunteer test subjects

```subject_test <- test/subject_test.txt``` : 2947 rows, 1 column

+ contains recorded features test data

```x_test <- test/X_test.txt``` : 2947 rows, 561 columns    

+ contains test data on code labels related to the activities

```y_test <- test/y_test.txt``` : 2947 rows, 1 columns 

+ contains train data on 21 out of 30 volunteer subjects

```subject_train <- test/subject_train.txt``` : 7352 rows, 1 column

+ contains train data on the recorded features 

```x_train <- test/X_train.txt``` : 7352 rows, 561 columns

+ contains train data on code labels related to the activities 

```y_train <- test/y_train.txt``` : 7352 rows, 1 columns

## Script preparation

1. Merges the training and the test sets to create one data set

    + ```X``` (10299 rows, 561 columns) is created by merging ```x_train``` and ```x_test``` using the ```rbind()``` function.
    + ```Y``` (10299 rows, 1 column) is created by merging ```y_train``` and ```y_test``` using the ```rbind()``` function.
    + ```Subject``` (10299 rows, 1 column) is created by merging ```subject_train``` and ```subject_test``` using the ```rbind()``` function.
    + ```merged``` (10299 rows, 563 column) is created by merging ```Subject```, ```Y``` and ```X``` using the ```cbind()``` function.

2. Extracts only the measurements on the mean and standard deviation for each measurement.
    + ```tidy_data``` (10299 rows, 88 columns) is created by subsetting ```merged```, selecting only the following columns: ```subject```, ```code```, the ```mean``` and ```std``` for each measurement.

3. Uses descriptive activity names to name the activities in the data set.
    + Numbers in code column of the ```tidy_data``` are replaced by labels taken from the second column in ```activity_labels```.

4. Labels the data set with descriptive variable names.
    + ```code``` column in ```tidy_data``` renamed as activities
    + ```Acc``` replaced by ```Accelerometer```
    + ```Gyro``` replaced by ```Gyroscope```
    + ```BodyBody``` replaced by ```Body```
    + ```Mag``` replaced by ```Magnitude```
    + Variables starting with character ```f``` replaced by ```Frequency```
    + Variables starting with character ```t``` replaced by ```Time```

5. From the data set in step 4, a new tidy data set with the average of each variable for each activity and each subject is created.
    + ```processed_data``` (180 rows, 88 columns) is created after grouping the ```tidy_data``` by subject and activity and taking the means of each variable for each activity and subject 
    + Exports ```processed_data``` into a ```processed_data.txt``` file.
