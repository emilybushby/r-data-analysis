## Download data
download.file("https://ndownloader.figshare.com/files/2292169",
              "portal_data_joined.csv")

## Load data
surveys <- read.csv("data /portal_data_joined.csv")

## Examine first 6 lines
head(surveys)

## Look at structure
str(surveys)

## Indexing Aand subsetting  
surveys[1, 1]   ## first element in the first column
surveys[1, 6]   ## first element in the sixth coloumn 
surveys[1:3, 7] ## first three elements in the seventh coloumn 
surveys[ ,1]    ## all the values in the first coloumn
surveys[8:11, ] ## all that values in rows 8-11

## task 1: create new data frame with only row 200 from surveys data
row200 <- surveys[200,]
row200
surveys_200 <- row200
nrow(surveys_200)
tail(surveys_200)

## task 2: use nrow
nrow(surveys)
surveys[34786,]
tail(surveys)
surveys_last <- surveys[34786,]

surveys_middle <- surveys[34786/2,]
surveys_middle

n_rows <- nrow(surveys)
surveys_head <- surveys[-(7:n_rows), ]
