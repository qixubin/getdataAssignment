Readme for the run analysis
===========================


###1. First, load the several txt into variable

```{r readata, results="hide"}
xtrain <- read.table("./train/X_train.txt")
ytrain <- read.table("./train/Y_train.txt")
subjecttrain <- read.table("./train/subject_train.txt")

xtest <- read.table("./test/X_test.txt")
ytest <- read.table("./test/y_test.txt")
subjecttest <- read.table("./test/subject_test.txt")

```
