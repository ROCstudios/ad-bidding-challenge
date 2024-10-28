
![a0880952d25d045ebaa0bf7ec7a6f8a2](https://github.com/user-attachments/assets/930da3a3-3da6-4a92-a016-44a39d2879cb)
#### Welcome Daniel

# Ad Buying Predictions

Please read below to understand the file structure and how to orient with the task.

data/

-- self explanatory. input data, validation data, checkpoint training/test splits

data/results

-- this is the final result (the 'assignment' directory) with predictions joined to validation_data

models/

-- saved trained models associated with notebooks so they can be used _across_ notebooks

outputs/

-- images, plots, and graphs

**The Notebooks**

The approach I took to this project was to start with a small directly corrolated dataframe and expand to the categorical features to push the model's predictions.

You'll see they're versioned.

v1 = Exploring impressions, clicks, and CTR.  Numerical features so we explore plot density graphs and visualize distribution.  We plot outliers but don't take action on them then we take action to remove missing values or impute them.  We perform statistical corrolation and covariant analysis.  We StandardScale our features and train a linear regression model.  **We evaluate and get pretty poor results.**  Not enough features and we see the there is no linear correlation in our data sets.

v2 = Now we explore the categorical features for channel, location, device, etc.  We visualize count plots and try to find distribution of the different features in relation to CTR and CPM.  Find some interesting things there to meaninful information being found in rare categories so when we scale use multi-step encoding of the values to address the skew of the data.  We also upgrade to GradientBoostingRegressor model. **Greatly improving performance.**

v3 = We continue with categorical feautres here for advertising and product information.  We take the time to account for missing values and properly format the categories so they are uniform identifiers that can then be encoded.  When it comes training we decide that we want a multi-target model for the limited time we have.  This requires the gradient boost regressor model to be wrapped MultiOututRegressor.  **We see a small improvement in performance.** 

v4 = Realizing that we get good predicitions but our R2 metrics shows a low variance meaning the big driver of CPM and CTR is not in training set.  So we combine the data frames and preprocess, encode, and train/test split the same as prior notebook.  We import a larget model _XGBRegressor_ that specializes in non-linear correlations more so than previous models we try.  Bigger boost in performance.  After we get this result we perform hyper-parameter tuning with RandomizedSearchCV.  **We get the best results with this notebook.** We add the functionality to save your models and data sets.

v4.2 = we keep the data we've been working with but we take our encodinga and instead of a calculated version taking a single target feature and applying it as a constant variable to get our encoded value we use a TargetEncoder lib so we can save our encoding to the file system.  We clean up the training code and eliminate duplicates.  **Applying this new encoding greatly reduces the performance of CTR predictions but improves CPM predictions even more. ** This notebook can be label as _in progress_

v5 = This was the last (rushed) notebook that allows us to complete the assignment.  We load our validation data set associated with the assignment.  Load our encoding and most recent model and run the predictions.  the results are then reveerse encoded and added to the results dataframe that are then saved.
