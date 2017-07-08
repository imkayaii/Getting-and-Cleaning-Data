---
title: "CodeBook"
output: html_document
---

This document describes the data and transformations used in this assignment by the R code and the definition of variables in TidyData.txt.

(1) Data Set Used

The data set used for this assigment can be downloaded from https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip. A full description is available at the site http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones. This data is obtained from "Human Activity Recognition Using Smartphones Data Set". The data linked are collected from the accelerometers from the Samsung Galaxy S smartphone.


(2) Input Data Set

It contains the following data files:
- "X_train.txt" (the variable features that are intended for training)
- "y_train.txt" (the activities corresponding to the variable features in "X_train.txt")
- "subject_train.txt" (information on the subjects from whom data is collected)
- "X_test.txt" (the variable features that are intended for testing)
- "y_test.txt" (the activities corresponding to the variable features in "X_test.txt")
- "subject_test.txt" (information on the subjects from whom data is collected)
- "activity_labels.txt" (metadata on the different types of activities)
- "features.txt" (the name of the features in the data sets)


(3) Transformations of Input Data Set

Transformations are performed on the input dataset to create the following:
- "merge_subject" (combined subjects in training and test data, and the column name is SubjectID)
- "merge_y" (combined activities in training and test data, and the column name is ActivityID)
- "merge_X" (all features of test and training and the name of the features are set in features from featureNames)
- "full_data" (a complete merged data for all features, activities and subjects)
- "all_Mean_STD" (subset of columns with std or mean from "full_data")
- "subset_data" (adding SubjectID and ActivityID to "all_Mean_STD")
- "required_data" ("subset_data" with SubjectID and ActivityID)
- ActivityID column in "required_data" is updated with descriptive names of activities taken from "activity_labels.txt". Activity column is expressed as a factor variable. Acronyms in variable names like 'Acc', 'Gyro', 'Mag', 't' and 'f' are replaced with descriptive labels such as 'Accelerometer', 'Gyroscpoe', 'Magnitude', 'Time' and 'Frequency'
- "tidy_data" (subset of "required_data" with average for each activity and subject. Entries in "tidy_data" are ordered based on SubjectID and ActivityID
- "TidyData.txt" (the text file of "tidy_data")


(4) Output Data Set

The output data "TidyData.txt" is a a space-delimited value file. The header line contains the names of the variables (see below). It contains the mean and standard deviation values of the data contained in the input files. The header is restructued in an understandable manner.


Variable names of Output Data Set:
 [1] "SubjectID"                                        
 [2] "ActivityID"                                       
 [3] "TimeBodyAccelerometerMean()-X"                    
 [4] "TimeBodyAccelerometerMean()-Y"                    
 [5] "TimeBodyAccelerometerMean()-Z"                    
 [6] "TimeBodyAccelerometerSTD()-X"                     
 [7] "TimeBodyAccelerometerSTD()-Y"                     
 [8] "TimeBodyAccelerometerSTD()-Z"                     
 [9] "TimeGravityAccelerometerMean()-X"                 
[10] "TimeGravityAccelerometerMean()-Y"                 
[11] "TimeGravityAccelerometerMean()-Z"                 
[12] "TimeGravityAccelerometerSTD()-X"                  
[13] "TimeGravityAccelerometerSTD()-Y"                  
[14] "TimeGravityAccelerometerSTD()-Z"                  
[15] "TimeBodyAccelerometerJerkMean()-X"                
[16] "TimeBodyAccelerometerJerkMean()-Y"                
[17] "TimeBodyAccelerometerJerkMean()-Z"                
[18] "TimeBodyAccelerometerJerkSTD()-X"                 
[19] "TimeBodyAccelerometerJerkSTD()-Y"                 
[20] "TimeBodyAccelerometerJerkSTD()-Z"                 
[21] "TimeBodyGyroscopeMean()-X"                        
[22] "TimeBodyGyroscopeMean()-Y"                        
[23] "TimeBodyGyroscopeMean()-Z"                        
[24] "TimeBodyGyroscopeSTD()-X"                         
[25] "TimeBodyGyroscopeSTD()-Y"                         
[26] "TimeBodyGyroscopeSTD()-Z"                         
[27] "TimeBodyGyroscopeJerkMean()-X"                    
[28] "TimeBodyGyroscopeJerkMean()-Y"                    
[29] "TimeBodyGyroscopeJerkMean()-Z"                    
[30] "TimeBodyGyroscopeJerkSTD()-X"                     
[31] "TimeBodyGyroscopeJerkSTD()-Y"                     
[32] "TimeBodyGyroscopeJerkSTD()-Z"                     
[33] "TimeBodyAccelerometerMagnitudeMean()"             
[34] "TimeBodyAccelerometerMagnitudeSTD()"              
[35] "TimeGravityAccelerometerMagnitudeMean()"          
[36] "TimeGravityAccelerometerMagnitudeSTD()"           
[37] "TimeBodyAccelerometerJerkMagnitudeMean()"         
[38] "TimeBodyAccelerometerJerkMagnitudeSTD()"          
[39] "TimeBodyGyroscopeMagnitudeMean()"                 
[40] "TimeBodyGyroscopeMagnitudeSTD()"                  
[41] "TimeBodyGyroscopeJerkMagnitudeMean()"             
[42] "TimeBodyGyroscopeJerkMagnitudeSTD()"              
[43] "FrequencyBodyAccelerometerMean()-X"               
[44] "FrequencyBodyAccelerometerMean()-Y"               
[45] "FrequencyBodyAccelerometerMean()-Z"               
[46] "FrequencyBodyAccelerometerSTD()-X"                
[47] "FrequencyBodyAccelerometerSTD()-Y"                
[48] "FrequencyBodyAccelerometerSTD()-Z"                
[49] "FrequencyBodyAccelerometerMeanFreq()-X"           
[50] "FrequencyBodyAccelerometerMeanFreq()-Y"           
[51] "FrequencyBodyAccelerometerMeanFreq()-Z"           
[52] "FrequencyBodyAccelerometerJerkMean()-X"           
[53] "FrequencyBodyAccelerometerJerkMean()-Y"           
[54] "FrequencyBodyAccelerometerJerkMean()-Z"           
[55] "FrequencyBodyAccelerometerJerkSTD()-X"            
[56] "FrequencyBodyAccelerometerJerkSTD()-Y"            
[57] "FrequencyBodyAccelerometerJerkSTD()-Z"            
[58] "FrequencyBodyAccelerometerJerkMeanFreq()-X"       
[59] "FrequencyBodyAccelerometerJerkMeanFreq()-Y"       
[60] "FrequencyBodyAccelerometerJerkMeanFreq()-Z"       
[61] "FrequencyBodyGyroscopeMean()-X"                   
[62] "FrequencyBodyGyroscopeMean()-Y"                   
[63] "FrequencyBodyGyroscopeMean()-Z"                   
[64] "FrequencyBodyGyroscopeSTD()-X"                    
[65] "FrequencyBodyGyroscopeSTD()-Y"                    
[66] "FrequencyBodyGyroscopeSTD()-Z"                    
[67] "FrequencyBodyGyroscopeMeanFreq()-X"               
[68] "FrequencyBodyGyroscopeMeanFreq()-Y"               
[69] "FrequencyBodyGyroscopeMeanFreq()-Z"               
[70] "FrequencyBodyAccelerometerMagnitudeMean()"        
[71] "FrequencyBodyAccelerometerMagnitudeSTD()"         
[72] "FrequencyBodyAccelerometerMagnitudeMeanFreq()"    
[73] "FrequencyBodyAccelerometerJerkMagnitudeMean()"    
[74] "FrequencyBodyAccelerometerJerkMagnitudeSTD()"     
[75] "FrequencyBodyAccelerometerJerkMagnitudeMeanFreq()"
[76] "FrequencyBodyGyroscopeMagnitudeMean()"            
[77] "FrequencyBodyGyroscopeMagnitudeSTD()"             
[78] "FrequencyBodyGyroscopeMagnitudeMeanFreq()"        
[79] "FrequencyBodyGyroscopeJerkMagnitudeMean()"        
[80] "FrequencyBodyGyroscopeJerkMagnitudeSTD()"         
[81] "FrequencyBodyGyroscopeJerkMagnitudeMeanFreq()"    
[82] "Angle(TimeBodyAccelerometerMean,Gravity)"         
[83] "Angle(TimeBodyAccelerometerJerkMean),GravityMean)"
[84] "Angle(TimeBodyGyroscopeMean,GravityMean)"         
[85] "Angle(TimeBodyGyroscopeJerkMean,GravityMean)"     
[86] "Angle(X,GravityMean)"                             
[87] "Angle(Y,GravityMean)"                             
[88] "Angle(Z,GravityMean)" 