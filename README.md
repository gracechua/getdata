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

X_train <- read.table("X_train.txt")
X_test <- read.table("X_test.txt")
Xbind <- rbind(X_train, X_test) 

y_train <- read.table("y_train.txt")
y_test <- read.table("y_test.txt") 
ybind <- rbind(y_train, y_test)

subject_train <- read.table("subject_train.txt") 
subject_test <- read.table("subject_test.txt") 
subjectbind <- rbind(subject_train, subject_test) 


data <- cbind(Xnew, ybind, subjectbind) 

2. Extracts only the measurements on the mean and standard deviation 
for each measurement - in other words, select only the columns of variables 
that have a mean AND standard deviation for that variable. those would 
be columns 1:6, 41:46, 81:86, 121:126, 161:166, 201:202, 214:215, 227:228, 
240:241, 253:254, 266:271, 345:350, 424:429, 503:504, 516:517, 529:530, 
542:543. Grep didn't seem to work for me so I did this manually. Clunky, but it gets the job done.

data2 <- data[,c(1:6, 41:46, 81:86, 121:126, 161:166, 201:202, 214:215, 227:228, 240:241, 253:254, 266:271, 345:350, 424:429, 503:504, 516:517, 529:530, 542:543, 562:563)]

Now, installs and initiates dplyr if you don't have it already. 

install.packages("dplyr")
library(dplyr) 

Now that we have only this data set, 
3. Uses descriptive activity names to name the activities in the data set
This necessitates renaming the variables in column 67, activities.

one <- (data2[,67]) %in% "1"
data2[one, 67] <- "WALKING"

two <- (data2[,67]) %in% "2"
data2[two, 67] <- "WALKING_UPSTAIRS"

three <- (data2[,67]) %in% "3"
data2[three, 67] <- "WALKING_DOWNSTAIRS"

four <- (data2[,67]) %in% "4"
data2[four, 67] <- "SITTING"

five <- (data2[,67]) %in% "5"
data2[five, 67] <- "STANDING"

six <- (data2[,67]) %in% "6"
data2[six, 67] <- "LAYING"

4. Appropriately labels the data set with descriptive variable names.
The column names are for the most part already descriptive; to maintain 
coherence with the original data set, the column names should remain as is. 
The two columns that need to be renamed are the second-to-last, activity, 
and the last, subject ID. 

colnames(data2)[colnames(data2)=="V1"] <- "Activity"
colnames(data2)[colnames(data2)=="V1.1"] <- "Subject_ID"

5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject. Does so by grouping the data by subject and activity, then summarising for the mean of each variable. This should produce a set of data with 180 rows and 68 columns. Uses write.table to write this to a text file that lives in your working directory.

data3 <- data2 %>%
      group_by(Subject, Activity) %>%
      summarise_each(funs(mean)) %>%

write.table(data3, filename="getdata-tidy.txt", row.names=FALSE)

