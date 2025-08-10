# Data-Visualization-Project
This is an example of a data visualization project that I have done in the past. 

 Data Visualization
#
library(tidyverse)
library(ggthemes)
#
# Importing penguin file
#
mypenguins <-read.csv(file.choose(), header=T)   #read.csv("penguinData.csv")
glimpse(mypenguins)

ggplot(
  data = mypenguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point()

# add aesthetics and layers
ggplot(
  data = mypenguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g, color = species)
) +
  geom_point()

# add linear model
ggplot(
  data = mypenguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g, color = species)
) +
  geom_point() +
  geom_smooth(method = "lm")

# one instead of three linear models
ggplot(
  data = mypenguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point(mapping = aes(color = species)) +
  geom_smooth(method = "lm")

# add lots of elements including titles, axis labels, shapes vs points

ggplot(
  data = mypenguins,
  mapping = aes(x = flipper_length_mm, y = body_mass_g)
) +
  geom_point(aes(color = species, shape = species)) +
  geom_smooth(method = "lm") +
  labs(
    title = "Body mass and flipper length",
    subtitle = "Dimensions for Adelie, Chinstrap, and Gentoo Penguins",
    x = "Flipper length (mm)", y = "Body mass (g)",
    color = "Species", shape = "Species"
  ) +
  scale_color_colorblind()

# multiple plots at one time
ggplot(data=mpg) + 
  geom_point(mapping=aes(x=displ, y=hwy)) +
  facet_wrap(~ class, nrow=2)

ggplot(data=mpg) + 
  geom_point(mapping=aes(x=displ, y=hwy)) +
  facet_grid(. ~ mpg$cyl)

ggplot(data=mpg) + 
  geom_point(mapping=aes(x=displ, y=hwy)) +
  facet_grid(mpg$drv ~ .)

# interactive map
library(leaflet)
r_birthplace_map <- leaflet() %>%
  addTiles() %>%  # use the default base map which is OpenStreetMap tiles
  addMarkers(lng=174.768, lat=-36.852,
             popup="The birthplace of R")
r_birthplace_map

