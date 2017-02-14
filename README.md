# Getting-Cleaning-Wearables-Data

# The assignment was fairly straightforward. I imported the data and merged into the data farme called "dta", which I used throughout the assingment.

# I then read in the names of the variables and assigned them to data frame "feats" and added these names to dta.

# Next I converted the acvities variable into a factor variable and changed the levels from numbers to descriptive elements in dta.

# I then added descriptive variable names to dta using the feats data and assigned names to the activities and subjects variables.

# Finally, to create the new tidy data, I used a for loop and applied tapply to get the mean of each variable in dta grouped by activity and subject. Then I merged these data into one data frame called "tidymean."

