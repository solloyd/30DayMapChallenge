# 30DayMapChallenge 2022

This is a collection of my #30daymapchallenge for 2022! For more information on the challenge, please visit: https://30daymapchallenge.com

I chose the theme **energy** as a central thread to this challenge! This is not a requirement, I could make completely different maps each day, but would like to explore new energy datasets, and ones I haven't had an opportunity to work with recently.

| Software      | Count         | Days          |
| ------------- | ------------- | ------------- |
| R             |  1            | 1             |
| ArcGIS Online |               |               |
| QGIS          |               |               |



##### You can find my full GIS portfolio [on my website](https://solloyd.wixsite.com/gisportfolio)

## Day One

Points. Looking at the power stations in Zambia in terms of type and amount of capacity!

![dayone_map.pdf](https://github.com/solloyd/30daymapchallenge/files/9824199/dayone_map.pdf)

I set out to use this 30 Day Challenge to refamiliarize myself with mapping in R, and potentially also learn QGIS. Today I realized this is going to be a lot harder than I originally thought... In ArcPro I could've produced a basic map like this in under a half hour, but in R let's say it took me muuuuuuch longer.

Credit: [Wikipedia](https://en.wikipedia.org/wiki/List_of_power_stations_in_Zambia), [Google Maps](maps.google.com), [OpenInfraMap](https://openinframap.org/stats/area/Zambia/plants)

<details><summary>Click Here for Day One's Code!</summary>
<p>

### Find below the code used for this map, and click here for the [Zambia Power Station Dataset](https://drive.google.com/drive/u/1/folders/1Bz-Pcke20iVJmTjPsvE0Ws2ZZJZ2u3v1) I created :)

```ruby
library(ggplot2)              
library(tidyverse)           
library(viridis) #played around with these colors, but did not end up on the final
library(plotly)


PowerStation <- read.csv("~/ADD YOUR PATH HERE/PowerStations_Zambia.csv") 


mapdata <- map_data("world") 
mapdata <- right_join(mapdata, PowerStation, by="region")


dayone_map <- ggplot(PowerStation, aes(x=Long, y=Lat)) +
        geom_polygon(data = mapdata, aes(x=long, y = lat), fill="grey", color="black", alpha=0.9)+
  geom_point(aes(size=Capacity_MW, color=Type), alpha=0.5) +
  ggtitle("Power Stations in Zambia by Capacity and Type") +
  theme(axis.title.x = element_blank(),
        axis.title.y = element_blank(),
        axis.ticks = element_blank(),
        axis.text.x = element_blank(),
        axis.text.y = element_blank(),
        plot.title = element_text(size=14, face="bold.italic")) +
  scale_size_continuous(breaks=c(5, 25, 50, 100, 250, 500, 750), name="Capacity (MW)", range = c(5,20))

dayone_map

#Make the map interactive!
ggplotly(dayone_map, tooltip="all")
```

</p>
</details>

## Day Two

Lines.

## Day Three

Polygons.

## Day Four

Color Friday: Green

## Day Five

Ukraine

## Day Six

Network

## Day Seven

Raster

## Day Eight

Data: OpenStreetMap

## Day Nine

Space

## Day Ten

A bad map

## Day Eleven

Color Friday: Red

## Day Twelve

Scale

## Day Thirteen

5 minute map

## Day Fourteen

Hexagons

## Day Fifteen

Food/drink

## Day Sixteen

Minimal

## Day Seventeen

A map without a computer

## Day Eighteen

Color Friday: Blue

## Day Nineteen

Globe

## Day Twenty

"My favorite..."

## Day Twenty-One

Data: Kontour Population Dataset

## Day Twenty-Two

*NULL*

## Day Twenty-Three

Movement

## Day Twenty-Four

Fantasy

## Day Twenty-Five

Color Friday: 2 colors

## Day Twenty-Six

Island(s)

## Day Twenty-Seven

Music

## Day Twenty-Eight

3D

## Day Twenty-Nine

"Out of my comfort zone"

## Day Thirty

Remix
