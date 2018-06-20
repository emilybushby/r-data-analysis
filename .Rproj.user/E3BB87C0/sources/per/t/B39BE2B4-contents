## Factors

sex <- factor(c("male", "female", "female", "male"))
sex
levels(sex)
nlevels(sex)

## PLot of females captured aginst males
plot(surveys$sex)

##Create a subset of the sex data
sex <- surveys$sex
levels(sex)

## Rename labels
levels(sex)[1] <- "Undetermined"
levels(sex)[2] <- "Female"
levels(sex)[3] <- "Male"

levels(sex)

## Rename both at same time
levels(sex)[2:3] <- c("Female", "Male")
levels(sex)

## Reorder the position of the factors
sex <- factor(sex, levels=c("Female", "Male", "Undetermined"))
plot(sex)
