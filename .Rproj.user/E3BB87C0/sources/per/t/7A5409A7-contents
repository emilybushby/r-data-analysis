## Analysing data

## Installing tidyverse
install.packages("tidyverse")

library("tidyverse")
surveys <- read_csv("data /portal_data_joined.csv")
head(surveys)
colnames(surveys)

## Use square bracket substetting to select rows from 1978 only 
surveys[surveys$year=="1978", ]

## do the same using dplyr and filter (filter - used to select rows)
filter(surveys, year == 1978)

## select - used to select coloumns 
select(surveys, year, plot_id, species_id)

## select only the three coloumns above but only from 1978
surveys_filtered <- filter(surveys, year=="1978")
select(surveys_filtered, year, plot_id, species_id)

## Stiching together with a pipe
## pipe symbol is %>%  (shift + control + m)
surveys_pipe <- 
surveys %>% 
  filter(year ==1978) %>% 
  select(year, plot_id, species_id)

## mutate - to create new coloumns based on existing coloumns or on some oporations done on existing coloumns
surveys %>% 
  select(weight, species)

surveys %>% 
  mutate(weight_kg = weight/1000) %>% 
  select(starts_with("w"))

## CHALLENGE 1 ##
## Create new dataframe from surveys that contains: 
## species_id coloumn and a new coloumn called hindfood_half containinghalf of the values from the hindfoot_length coloumn 
## all the values in hindfoot_half should be less than 30
challenge_one <- 
surveys %>% 
  mutate(hindfoot_half = hindfoot_length/2) %>% 
  select(species_id, hindfoot_half) %>% 
  filter(hindfoot_half<30)

challenge_one

## How to remove missing observations 
surveys %>% 
  mutate(weight_kg = weight/1000) %>% 
  select(starts_with("w")) %>% 
  filter(!is.na(weight)) ## filters out rows in coloumn weight that are not NA. Removing "!" will show you all the NAs

## How to get a summary overview of a dataset
table(surveys$year)
length(table(surveys$year))
range(surveys$year)
summary(surveys)

## Splitting and running calulations on groups
surveys %>% 
  group_by(year) %>% 
  summarise(mean_hindfoot_length = mean(hindfoot_length,
                                        na.rm = TRUE))
surveys %>% 
  filter(!is.na(weight)) %>% 
  group_by(sex, species_id) %>% 
  summarise(mean_weight = mean(weight),
            min_weight = min(weight),
            sd_weight = sd(weight))

surveys %>% 
  count(sex, species) %>% 
  print(n = 81)

surveys %>% 
  count(species, sort = TRUE)

## arrange - used to arrange rows
surveys %>% 
  count(sex, species) %>% 
  arrange(species, desc(n))


## CHALLENGE 2 ##
## How many individuals were caught in each plot_type. Answer in 2 ways (using group_by and count)
surveys %>% 
  count(plot_type)

surveys %>% 
  group_by(plot_type) %>% 
  tally()


## CHALLENGE 3 ##
## What is the heaviest animlal mesured in each year? 
## Return coloumns year, genus, species_id, and weight. Do not return missing observations
surveys %>% 
  filter(!is.na(weight)) %>% 
  group_by(year) %>% 
  filter(weight == max(weight)) %>% 
  select(year, genus, species_id, weight) %>% 
  arrange(desc(weight))


## Keep the species for which there are more than 50 observations   
surveys_complete <- 
  surveys %>% 
  filter(!is.na(weight),
         !is.na(hindfoot_length),
         !is.na(sex))

species_counts <- surveys_complete %>% 
  count(species_id) %>% 
  filter(n>=50)

## Reduce the surveys_complete object so that it only contains species with at least 50 observations
## (these species are in object species_counts)
surveys_complete <- 
  surveys_complete %>% 
  filter(species_id %in% species_counts$species_id)

### How to plot with ggplot ###
# geom_point() is scatter plot
ggplot(data = surveys_complete, mapping = aes(x = weight, y = hindfoot_length)) + geom_point()

surveys_plot <- ggplot(data = surveys_complete, mapping = aes(x = weight, y = hindfoot_length))
surveys_plot + geom_point()


##### Day Three - GRAPHS #####  

## Recap ##
num_species <- 
  surveys_complete %>% 
  count(species_id) %>% 
  filter(n >= 1000)

surveys_complete %>% 
  filter(species_id %in% num_species$species_id)

animals <-c("pig", "cat", "dog", "donkey", "gorilla", "mouse")
other_animals <-c("zebra", "parrot", "donkey", "cat", "camel")
animals <- c(animals, "zebra", "parrot", "camel") ## expand/add to original animals vercor 

# shows what is  common, compares the 2 but only one way around
animals %in% other_animals
other_animals %in% animals

# tells you what is in both data sets 
intersect(animals, other_animals)  

## ##

## ggplot needs data, aesthetics or mapping of variables from the data to the plot
#geom_point(alpha = 0.1) makes points more transparent 
#geom_point(es(colour=species_id)) makes each different species a different colour 

ggplot(data=surveys_complete, mapping = aes(x=weight, y=hindfoot_length)) + geom_point(alpha = 0.1, aes(colour=species_id))

## geom_boxplot to make boxplot ##
ggplot(data=surveys_complete, mapping = aes(x=species_id, y=hindfoot_length)) + geom_boxplot()

## Add scatter plot over the top of the boxplot using geom_hitter or geom_point ##
ggplot(data=surveys_complete, mapping = aes(x=species_id, y=hindfoot_length)) + geom_boxplot() + geom_jitter(alpha=0.1, 
                                                                                                             colour="tomato")
ggplot(data=surveys_complete, mapping = aes(x=species_id, y=hindfoot_length)) + geom_boxplot() + geom_point(alpha=0.1, 
                                                                                                             colour="tomato")

## Line graph using new object yearly_counts ##
yearly_counts <- 
  surveys_complete %>% 
  group_by(year, species_id) %>% 
  tally()

ggplot(data=yearly_counts, mapping = aes(x=year, y=n)) +geom_line()

#add in group variable to tell graph which species
ggplot(data=yearly_counts, mapping = aes(x=year, y=n, group=species_id)) +geom_line()

# Add colour
ggplot(data=yearly_counts, mapping = aes(x=year, y=n, group=species_id,colour=species_id)) +geom_line()

# Faceting - splitting display of data into multiple sub groups (splitting last graph into multiple graphs with only one 
# species on each)
ggplot(data=yearly_counts, mapping = aes(x=year, y=n, 
                                         group=species_id,colour=species_id))+geom_line()+facet_wrap(~species_id)

## Split by males and females ##
yearly_sex_counts <- 
  surveys_complete %>% 
  group_by(year, species_id, sex) %>% 
  tally()

yearly_sex_counts

ggplot(data=yearly_sex_counts, mapping = aes(x=year, y=n, 
                              group=species_id,colour=sex))+geom_line()+facet_wrap(~species_id)

## Add title
ggplot(data=yearly_sex_counts, mapping = aes(x=year, y=n, 
                                             group=species_id,colour=sex))+geom_line()+facet_wrap(~species_id)+ggtitle("Species counts over time")

## Add axis labels
ggplot(data=yearly_sex_counts, mapping = aes(x=year, y=n, 
                                             group=species_id,colour=sex))+geom_line()+facet_wrap(~species_id)+
  labs(title="species counts", x="Year of observation", y="Number of species")

## Change / tilt x-axis labels
ggplot(data=yearly_sex_counts, mapping = aes(x=year, y=n, 
                                             group=species_id,colour=sex))+geom_line()+facet_wrap(~species_id)+
  labs(title="species counts", x="Year of observation", y="Number of species")+theme(axis.text.x=element_text(angle=45))

## Save graph
ggsave("my_fancy_plot.pdf")
ggsave("my_fancy_plot.png", width = 15, height = 10, dpi=300)



