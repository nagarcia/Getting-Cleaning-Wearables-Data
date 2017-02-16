# Getting-Cleaning-Wearables-Data

# The assignment was fairly straightforward. I imported the data and merged into the data farme called "dta", which I used throughout the assingment.

# I then read in the names of the variables and assigned them to data frame "feats" and added these names to dta.

# Next I converted the acvities variable into a factor variable and changed the levels from numbers to descriptive elements in dta.

# I then added descriptive variable names to dta using the feats data and assigned names to the activities and subjects variables.

# Finally, to create the new tidy data, I used a for loop and applied tapply to get the mean of each variable in dta grouped by activity and subject. Then I merged these data into one data frame called "tidymean."

>

##GETTING AND CLEANING DATA COURSE ASSIGMENT##

##1. Merges the training and the test sets to create one data set.

setwd("~/Desktop/Coursera/UCI HAR Dataset/test")
xtest <- read.table("X_test.txt")
ytest <- read.table("y_test.txt")
subjtest <- read.table("subject_test.txt")
test <- cbind(xtest, ytest, subjtest)

setwd("~/Desktop/Coursera/UCI HAR Dataset/train")
xtrain <- read.table("X_train.txt")
ytrain <- read.table("y_train.txt")
subjtrain <- read.table("subject_train.txt")
train <- cbind(xtrain, ytrain, subjtrain)

dta <- rbind(test, train)


##2. Extracts only the measurements on the mean and standard deviation for each measurement."

setwd("~/Desktop/Coursera/UCI HAR Dataset")

feats <- read.table("features.txt")
meanstd <- grep(".mean()|.std()", feats$V2)
dta <- dta[ , meanstd]



##3. Uses descriptive activity names to name the activities in the data set

activity <- rbind(ytest, ytrain)
activity <- as.factor(activity[,1])

levels(activity) <- c("walking", "walking_upstairs", "walking_downstairs", "sitting",
                  "standing", "laying")


subj <- rbind(subjtest, subjtrain)
dta <- cbind(dta, activity, subj)


##4. Appropriately labels the data set with descriptive variable names.

cnames <- feats[meanstd, 2]
cnames <- as.character(cnames)

colnames(dta) <- cnames
colnames(dta)[80] <- "activity"
colnames(dta)[81] <- "subject"

##5.From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

meanactivity <- list()

for(i in 1:79){
        meanactivity[i] <- list(tapply(dta[,i], dta$activity, mean))      

}

meanactivity

meansubj <- list()

for(i in 1:79){
        meansubj[i] <- list(tapply(dta[,i], dta$subject, mean))
}

meansubj

mna <- data.frame(meanactivity)
colnames(mna) <- cnames

mns <- data.frame(meansubj)
colnames(mns) <-cnames

tidymean <- rbind(mna, mns)

write.table(tidymean, file = "/Users/noahgarcia/Desktop/Coursera/tidymean.txt", row.name = FALSE)
