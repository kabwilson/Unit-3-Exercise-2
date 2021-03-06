# Unit 3 Exercise 2
##Taking care of the missing values in different columns of the titanic data
library(plyr)

library(dplyr)

library(tidyr)

### Apply the dataframe to another name to maintain the integrity of the original data
titanic_next <- titanic_original

### Find the missing values in the embarked column and replace with "S"
titanic_next$embarked[is.na(titanic_next$embarked)] <- "S"

### Find the missing values in the age column and replace them with the mean of the entire column
titanic_next$age[is.na(titanic_next$age)] <- mean(titanic_next$age, na.rm = TRUE)

### Fill the empty slots in the boat column with a string such as 'None'
titanic_next$boat[is.na(titanic_next$boat)] <- "None"

### Create a new column 'has_cabin_number' that shows a 1 if the cabin number is there and a 0 if not
titanic_next$has_cabin_number <- titanic_next$cabin

titanic_next$has_cabin_number[!is.na(titanic_next$has_cabin_number)] <- 1

titanic_next$has_cabin_number[is.na(titanic_next$has_cabin_number)] <- 0

### Export the table to a csv file
write.csv(titanic_next, file = "titanic_clean.csv", row.names = FALSE)
