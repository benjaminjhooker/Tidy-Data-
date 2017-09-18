# The r script does the following:
1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement.
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names.
5. From the data set in step 4, creates a second, independent tidy data set with the average of each 
variable for each activity and each subject.

# Variables used:
1. `x_train`, `y_train`, and `subj_trn` are all related to the training data sets were were downloaded and parsed
2. `x_test`, `y_test`, and `subj_test` are all related to the test data sets that were downloaded and parsed
3. `x_df`, `y_df`, and `subject_df` are the combined train and test data sets via the `rbind` function
4. `features` was the variable assigned to desired feature variables in the data set
5. `act_lab` was the variable assigned to activity names for each subject
6. `complete_data` was the name for the combined data frame of all train, test, feature, and activity sets
7. `avg_tbl` is the mean of each feature by subject and activity which is then exported as "avg_table.txt"

# Values:
 1. "total_acc", a measurement in the data set, is measured in 'g.'<sup>1</sup>
 2. "body_acc" is the difference between the acceleration signal and the total_acc signal<sup>1</sup>
 3. "gyro_acc" is the "angular velocity" measured in "radians/sec"<sup>1</sup>
 
 ### Citation: 
 1. README text file as a part of the data download for the activity recognition
