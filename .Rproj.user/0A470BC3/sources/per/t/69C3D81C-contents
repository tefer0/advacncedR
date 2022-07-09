#advanced R
#Tidyverse
install.packages("tidyverse")
library(tidyverse)

tidyverse_conflicts() #

tidyverse_deps() #

tidyverse_logo()

tidyverse_packages()

tidyverse_update()

#dplyr
#Commonly used functions
select()
filter()
group_by()
summarize()
mutate()

library(datasets)

library(gapminder)

attach(iris)
#select()
sepal <- select(iris, Sepal.Length, Sepal.Width)
#Let's use the pipe operator
sepal <- iris %>% select(Sepal.Length, Sepal.Width)
#To remove one column only from the dataset
less_sepal <- select(sepal, -Sepal.Length)
#Renaming column names
tidy_sepal <- iris %>%rename(sepal_width=Sepal.Width)

#filter()
#allows you to select a subset of rows in a data frame.
iris_virginica <- iris %>% filter(Species=="virginica")
iris_virginica_sepal <- iris %>% filter(Species=="virginica", Sepal.Length > 6)
iris_sesota_sepal <- iris %>% filter(Species=="setosa") %>%
  select(Sepal.Length, Sepal.Width)
#group_by()
#Reduces error prone repetitiveness
#Split original data frame into multiple pieces
str(iris) #check the properties of the dataset
str(iris %>% group_by(Species))

#summarize ()
#Turn many observations into a single data point
#To group per species and get the mean of Sepal.Width
gdp_byspecies <- iris %>% group_by(Species) %>% summarize(mean_species 
                                                          = mean(Sepal.Width))
#To group per two variable
gdp_byspecies1 <- iris %>% group_by(Species, Petal.Length) %>%
  summarize(mean_sepal_width = mean(Sepal.Width))
#To calculate multiple single data points
gdp_byspecies2 <- iris %>% group_by(Species, Petal.Length) %>%
summarize(mean_sepal_width = mean(Sepal.Width), mean_petal_length = 
            mean(Petal.Length), sd_sepal_length = mean(Sepal.Length))

#challenge
#Use group_by(), summarize(), mean(), sd(), min(), max() to calculate the mean,
#standard deviation, get maximum value, minimum value of each Species’
#Sepal.Width
gdp_byspecies3 <- iris %>% group_by(Species) %>% summarise(mean_m = 
    mean(Sepal.Width), min_m = min(Sepal.Width), max_m = max(Sepal.Width), 
    sd_m = sd(Sepal.Width))

#mutate()
#updates or creates new variables of a data frame
#Changing Sepal.Length to millimetre(update)
iris_SLMm_<-iris %>% mutate(Sepal.Length=Sepal.Length*10)
#Creating a new column called SLMm
iris %>% mutate(SLMm=Sepal.Length*10)
#Challenge
#Use group_by(), mutate(), summarize(), mean(), sd(), min(), max() to calculate the
#mean, sd, find maximum and minimum of a new column of variable called
#SPlength where the Sepal.Length is divided by Petal.Length
newsum <- iris %>% group_by(Species) %>% mutate(SLMm=Sepal.Length/Petal.Length) %>% 
  summarise(mean_m = mean(SLMm), min_m = min(SLMm), max_m = 
  max(SLMm), sd_m = sd(SLMm))
newsum

#ggplot2
#built on the grammar of graphics
#most effective for creating publication quality graphics
#Common plots
#Scatterplots,Line Plots,Bar plots,Histogram,Boxplot

#Scatterplots
#Scatter plots allow you to compare two variables within your data.
#To do this with ggplot2, you use geom_point()
#Create a subset of iris using Sepal.Length>5 as a condition
iris_small <- iris %>% filter(Sepal.Length > 5)
#Create a scatter plot that compares petal width and length
ggplot(iris_small, aes(x=Petal.Length, y=Petal.Width)) + geom_point()
#Adding color
ggplot(iris_small, aes(x=Petal.Length, y=Petal.Width, color=Species)) + geom_point()
#Using different size for different variable
ggplot(iris_small, aes(x=Petal.Length, y=Petal.Width, color=Species,
                         size=Sepal.Length)) + geom_point()
#Faceting
ggplot(iris_small, aes(x=Petal.Length, y=Petal.Width)) + geom_point()+
  facet_wrap(~Species)

#Line Plot
#Create a sub-data
by_year <- gapminder %>% group_by(year) %>%
  summarize(medianGdpPerCap=median(gdpPercap))
#Create a line plot
ggplot(by_year, aes(x=year, y=medianGdpPerCap))+ geom_line()+
  expand_limits(y=0)

#Bar Plots
#Create a sub data
by_species <- iris %>% filter(Sepal.Length>6) %>% group_by(Species) %>%
  summarize(medianPL=median(Petal.Length))
#Create a bar plot
ggplot(by_species, aes(x=Species, y=medianPL)) + geom_col()

#Histogram
ggplot(iris_small, aes(x=Petal.Length))+ geom_histogram()
#Boxplot
ggplot(iris_small, aes(x=Species, y=Sepal.Width))+ geom_boxplot()

#Shiny Apps
#A Shiny app is a web page (UI) connected to a computer running a live R
#session (Server)
install.packages("shiny")
#  App template
library(shiny)
ui <- fluidPage()
server <- function(input, output){}
shinyApp(ui = ui, server = server)

ui <- fluidPage( numericInput(inputId = "n", "Sample size", value = 25),
                 plotOutput(outputId = "hist") )
server <- function(input, output) { output$hist <- renderPlot({ hist(rnorm(input$n)) })
}
shinyApp(ui = ui, server = server)