---
title: "Getting and Cleaning Data Assignment"
output: html_document
---

The objective of this assignment is to clean and extract usable data from the zip file that is available at https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip. A full description is available at the site where the data was obtained:
http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones. 

The goal is to prepare a tidy data that can be used for later analysis, and a R script called run_analysis.R is created that does the following:
- Merges the training and the test sets to create one data set
- Extracts only the measurements on the mean and standard deviation for each measurement
- Uses descriptive activity names to name the activities in the data set
- Appropriately labels the data set with descriptive variable names
- From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject

Four items are found in this repository:
- run_analysis.R : a R-code run on the data set
- TidyData.txt : a tidy data created from the original data using run_analysis.R
- CodeBook.md : a CodeBook reference to the variables in TidyData.txt
- README.md : an analysis of the code in run_analysis.R


Getting Started
  ## Set working directory to where "UCI HAR Dataset" folder is.
  ## Install "data.table" and "dplyr" packages if not already done so

	## Load the packages
	library(data.table)
	library(dplyr)

	## Load test data
	subject_test <- read.table("test/subject_test.txt", header = FALSE)
	X_test <- read.table("test/X_test.txt", header = FALSE)
	y_test <- read.table("test/y_test.txt", header = FALSE)

	## Load training data
	subject_train <- read.table("train/subject_train.txt", header = FALSE)
	X_train <- read.table("train/X_train.txt", header = FALSE)
	y_train <- read.table("train/y_train.txt", header = FALSE)

	## Load supporting data
	features <- read.table("features.txt")
	activity_labels <- read.table("activity_labels.txt", header = FALSE)

	## (1) Merge both training and test data into one data set
	merge_subject <- rbind(subject_test, subject_train)
	colnames(merge_subject) <- "SubjectID"

	merge_X <- rbind(X_test, X_train)
	colnames(merge_X) <- t(features[2])

	merge_y <- rbind(y_test, y_train)
	colnames(merge_y) <- "ActivityID"

	full_data <- cbind(merge_subject, merge_X, merge_y)

	## (2) Extract only the measurements on the mean and STD for each measurement
	all_Mean_STD <- grep(".*Mean.*|.*Std.*", names(full_data), ignore.case = TRUE)
	subset_data <- c(all_Mean_STD, 1, 563)
	required_data <- full_data[, subset_data]
 
	## (3) Use descriptive activity names to name the activities in the data set
	required_data$ActivityID <- as.character(required_data$ActivityID)
		for (i in 1:6) {
			required_data$ActivityID[required_data$ActivityID == i] <- as.character(activity_labels[i,2])
			}
	required_data$ActivityID <- as.factor(required_data$ActivityID)

	## (4) Label the data set appropriately with descriptive variable names
	names(required_data) <- gsub("Acc", "Accelerometer", names(required_data))
	names(required_data) <- gsub("Gyro", "Gyroscope", names(required_data))
	names(required_data) <- gsub("BodyBody", "Body", names(required_data))
	names(required_data) <- gsub("Mag", "Magnitude", names(required_data))
	names(required_data) <- gsub("^t", "Time", names(required_data))
	names(required_data) <- gsub("^f", "Frequency", names(required_data))
	names(required_data) <- gsub("tBody", "TimeBody", names(required_data))
	names(required_data) <- gsub("-mean()", "Mean", names(required_data), ignore.case = TRUE)
	names(required_data) <- gsub("-std()", "STD", names(required_data))
	names(required_data) <- gsub("-freq()", "Frequency", names(required_data))
	names(required_data) <- gsub("angle", "Angle", names(required_data))
	names(required_data) <- gsub("gravity", "Gravity", names(required_data))

	## (5) Create another data set from (4) with the average of each variable for each activity and subject
	required_data$SubjectID <- as.factor(required_data$SubjectID)
	required_data <- data.table(required_data)
	tidy_data <- aggregate(. ~SubjectID + ActivityID, required_data, mean)
	tidy_data <- tidy_data[order(tidy_data$SubjectID, tidy_data$ActivityID),]
	write.table(tidy_data, file = "TidyData.txt", row.names = FALSE)

