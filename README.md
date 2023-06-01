# Getting and Cleaning Data Course Project

### 1.

```         
filename = "getdata_projectfiles_UCI HAR Dataset.zip"

if (!file.exists(filename)){
    fileURL = 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip'
    download.file(fileURL, filename, method='curl')
}  
if (!file.exists('UCI HAR Dataset')) { 
    unzip(filename) 
}
```

This code downloads the data from the given website and unzips the raw datasets.

### 2.

```         
activity_labels = read.table('UCI HAR Dataset/activity_labels.txt')
activity_labels[,2] = as.character(activity_labels[,2])
features = read.table('UCI HAR Dataset/features.txt')
features[,2] = as.character(features[,2])
```

This code loads the activity labels and features from their respective files.

### 3.

```         
req_features = grep("mean*|std*",features[,2])
req_features_names = features[req_features,2]
req_features_names = gsub('-mean','Mean',req_features_names)
req_features_names = gsub('-std','Std',req_features_names)
req_features_names = gsub('[()-]','',req_features_names)
```

This code gets the feature names which are only related to either the mean or standard deviation through the use of the grep() function.

### 4.

```         
subject_train = read.table('UCI HAR Dataset/train/subject_train.txt')
y_train = read.table('UCI HAR Dataset/train/y_train.txt')
X_train = read.table('UCI HAR Dataset/train/X_train.txt')[req_features]
train_df = cbind(subject_train,y_train,X_train)

subject_test = read.table('UCI HAR Dataset/test/subject_test.txt')
y_test = read.table('UCI HAR Dataset/test/y_test.txt')
X_test = read.table('UCI HAR Dataset/test/X_test.txt')[req_features]
test_df = cbind(subject_test,y_test,X_test)

combined_df = rbind(train_df,test_df)
colnames(combined_df) = c('Subject','Activity',req_features_names)
```

This code loads the train & test data, then merges them with the use of the cbind() and rbind() functions.

### 5.

```         
combined_df$Subject = as.factor(combined_df$Subject)
combined_df$Activity = factor(combined_df$Activity,levels=activity_labels[,1],labels=activity_labels[,2])

library(dplyr)

tidy_df = combined_df %>%
    group_by(Subject,Activity) %>%
    summarise(across(everything(),mean)) %>%
    ungroup %>%
    as.data.frame()

write.table(tidy_df,'tidy.txt',row.names=FALSE,quote=FALSE)
```

This code creates the second, independent tidy data set with the average of each variable for each activity and each subject.
