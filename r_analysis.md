## Course Project(CP).1
library(curl)
library(plyr)
library(stringr)


### CP.1.1 Read in all of the training data
x_train <-read.table( "./UCI HAR Dataset/train/X_train.txt")
y_train <-read.table("./UCI HAR Dataset/train/Y_train.txt")
subj_trn <- read.table("./UCI HAR Dataset/train/subject_train.txt")

### CP.1.2 Read in all of the test data
x_test <- read.table("./UCI HAR Dataset/test/X_test.txt")
y_test <- read.table("./UCI HAR Dataset/test/y_test.txt")
subj_test <- read.table("./UCI HAR Dataset/test/subject_test.txt")

### CP.1.3 'rbind' the data to assemble the data frames
x_df <- rbind(x_train, x_test)
y_df <- rbind(y_train, y_test)
subject_df <- rbind(subj_trn, subj_test)

## CP.2 
### CP.2.1 Read in the features data
features <- read.table("./UCI HAR Dataset/features.txt")
### CP.2.2 Extract the mean or standard dev from the data
### but only keep the means and stds that have a '()' immediately
### following the key words
features1 <- grep("-(mean|std)\\(\\)", features[,2])
### CP.2.3 Filter the data from the x_df
x_df <- x_df[, features1]
names(x_df) <- features[features1,2]

## CP.3 Read in and label the activity data set
act_lab <- read.table("./UCI HAR Dataset/activity_labels.txt")
y_df[,1] <- act_lab[y_df[,1],2]
names(y_df) <- "activity"


## CP.4 Rename the 'subject' variable and comdine all of the datasets into
### one to complete the tidy data set.
names(subject_df) <- "subject"
complete_data <- cbind(x_df, y_df, subject_df)

## CP.5 Genereate create a second, independent tidy data set with the average of each 
## variable for each activity and each subject
avg_tbl <- ddply(complete_data, .(subject, activity), function(x) colMeans(x[, 1:66]))

## Write to a text file:
write.table(avg_tbl, "avg_table.txt", row.names = FALSE, quote = FALSE)
