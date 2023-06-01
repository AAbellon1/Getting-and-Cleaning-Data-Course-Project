# Summary of Variables in run_analysis.R script

-   **activity_labels:** Contains the activities performed alongside their corresponding number code labels (e.g., 1 refers to WALKING, 2 refers to WALKING_UPSTAIRS)

-   **features:** Contains the different features or measurements that were recorded (e.g., tBodyAcc-mean()-X)

-   **req_features:** Contains the row indices of the features that are related to the mean or standard deviation

-   **req_features_names:** Contains the names of the features that are related to the mean or standard deviation

-   **subject_train, subject_test:** Contains train & test data of volunteer test subjects being observed

-   **Y_train, Y_test:** Contains train & test data of activities' number code labels

-   **X_train, X_test:** Contains values of recorded features of train & test data

-   **train_df, test_df, combined_df:** Contains values of all attributes upon merge of train & test data

-   **tidy_df:** Contains the average of each variable for each activity and each subject
