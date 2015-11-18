Readme for the run analysis
===========================


###1. First, load the several txt into variable and bind into one

```{r readata, results="hide"}
activitylabel <- read.table("activity_labels.txt")
names(activitylabel) <- c("id","activity")
feature <- read.table("features.txt")

xtrain <- read.table("./train/X_train.txt")
ytrain <- read.table("./train/Y_train.txt")
subjecttrain <- read.table("./train/subject_train.txt")

xtest <- read.table("./test/X_test.txt")
ytest <- read.table("./test/y_test.txt")
subjecttest <- read.table("./test/subject_test.txt")

train <- cbind(subjecttrain,ytrain, xtrain)
test <- cbind(subjecttest, ytest, xtest)
total <- rbind(train, test)

```

###2. add column name and reorder the column of "total"

```{r organize, results="hide"}
names(total)[1] <- "subject"
names(total)[2] <- "activityid"
names(total)[3: ncol(total)] <- as.character(feature[,2])
```

###3. remove the column which is not mean() and sd(), and merge with the activitylabel

```
colmean <-grep("mean\\(\\)" , feature$V2)
colstd <-grep("std\\(\\)" , feature$V2)
colremain <- c(1,2 ,c(colmean, colstd) +2)

remain <- total[,colremain]
colsize <- ncol(remain)
merged <- merge(remain, activitylabel, by.x = "activityid", by.y = "id", all = TRUE)
merged <- merged[, c(2,colsize+1, 3:colsize)]
result <- merged[order(merged$subject, merged$activity),]
```

###4. Aggregate data by mean ,and write to txt
```
tidyresult <- aggregate(. ~ subject + activity, result, mean)
write.table(tidyresult, "tidydata.txt",row.names = FALSE)
```
