getdata
=======

Course project submission for the Getting &amp; Cleaning Data course on Coursera: how the run_analysis.R script works

1. Merges the training and the test sets to create one data set. Here's how: 
Assume that the sets are in the same folder, which is your working directory. 
Turn X_train.txt and X_test.txt into tables, and rbind them together. 
Turn features.txt into a table called features, treat features as variable names and stick them on top.  
Turn y_train.txt and y_test.txt into tables, rbind them together, and treat this set as activity labels
Turn subject_train.txt and subject_test.txt into tables, rbind them together. treat this set as identifiers
Then cbind those new entities.  


2. Extracts only the measurements on the mean and standard deviation 
for each measurement - in other words, select only the columns of variables 
that have a mean AND standard deviation for that variable. those would 
be columns 1:6, 41:46, 81:86, 121:126, 161:166, 201:202, 214:215, 227:228, 
240:241, 253:254, 266:271, 345:350, 424:429, 503:504, 516:517, 529:530, 
542:543. Grep didn't seem to work for me so I did this manually. 

Now, installs and initiates dplyr if you don't have it already. 

Now that we have only this data set, 
3. Uses descriptive activity names to name the activities in the data set
This necessitates renaming the variables in column 67, activities.

4. Appropriately labels the data set with descriptive variable names.
The column names are for the most part already descriptive; to maintain 
coherence with the original data set, the column names should remain as is. 
The two columns that need to be renamed are the second-to-last, activity, 
and the last, subject ID. 

5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject. Does so by grouping the data by subject and activity, then summarising for the mean of each variable. This should produce a set of data with 180 rows and 68 columns. 


