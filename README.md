# 30DayMapChallenge 2022 :world_map:

This is a collection of my #30daymapchallenge for 2022! For more information on the challenge, please visit: https://30daymapchallenge.com 

I chose the theme :low_brightness:**energy**:low_brightness: as a central thread to this challenge! This is not a requirement, I could make completely different maps each day, but would like to explore new energy datasets, and ones I haven't had an opportunity to work with recently. Additionally, I'm setting out to use this challenge as a way to strengthen my R mapping skills, and completely learn QGIS, as basically all of my formal education was taught using ArcMap and then ArcPro from ESRI.

| Software      | Count         | Days          |
| ------------- | ------------- | ------------- |
| R             |  3            | 1,3,4             |
| QGIS          |               |               |
| ArcPro        |   1            |  2             |


##### You can find my publically available GIS portfolio [on my website](https://solloyd.wixsite.com/gisportfolio)

## Day One

📍 Points. 

Looking at the power stations in Zambia in terms of type and amount of capacity!

![dayone_map.pdf](https://github.com/solloyd/30daymapchallenge/files/9824199/dayone_map.pdf)

I set out to use this 30 Day Challenge to refamiliarize myself with mapping in R, and potentially also learn QGIS. Today I realized this is going to be a lot harder than I originally thought... In ArcPro I could've produced a basic map like this in under a half hour, but in R let's say it took me muuuuuuch longer.

Data Credits: [Wikipedia](https://en.wikipedia.org/wiki/List_of_power_stations_in_Zambia), [Google Maps](maps.google.com), [OpenInfraMap](https://openinframap.org/stats/area/Zambia/plants)

<details><summary>Click Here for Day One's Code!</summary>
<p>

#### Find below the code used for this map, and click here for the [Zambia Power Station Dataset](https://drive.google.com/file/d/1K6_roQEkf_d_DC8YL2-iIxy61s8S8yHB/view?usp=sharing) I pulled together :)

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

〰️ Lines. 

I am reusing a map I made while working in the [FUEL Lab](fuel.seas.umich.edu) because this is such a cool concept (S/O Cheryl Weyant for trusting me with the execution!). This depicts the electricity lines in Zimbabwe over nighttime lights imagery, so you can see where energy is being used and how that corresponds to the grid!

<img src="https://user-images.githubusercontent.com/116127236/199527752-52128ffb-c1b8-4553-845d-e84f90f56d17.jpg" width="400" >

Data Credits: [SEDAC](https://sedac.ciesin.columbia.edu/data/set/sdei-viirs-dmsp-dlight), [EnergyData.Info](https://energydata.info/dataset/zimbabwe-electricity-transmission-network-2017)

## Day Three

🔲 Polygons.

The US uses a lot of energy... that is no surprise to anyone, but how much are Americans using in each state? The top five states based on consumption per capita are (in million BTU): Louisiana (903), Alaska (874), Wyoming (874), North Dakota (804), and Iowa (479). I used a diverging color palette for this map to show the wide range of values - you can see the top three states clearly in the green, followed by a handful of light yellow states, and many light and dark orange states. This is the importance of colors scales... (hint for a future day)

Check out Day Three's map to find out more! 

![daythree_map.pdf](https://github.com/solloyd/30DayMapChallengeDRAFT/files/9890470/daythree_map.pdf)

Data Credit: [US Energy Information Administration](https://www.eia.gov/state/?sid=US)

<details><summary>Click Here for Day Three's Code!</summary>
<p>

### Find below the code used for this map, and click here for the [Consumption per Cpatia Dataset](https://drive.google.com/file/d/1pOy9N37P7k5RFaZ_V14dy0a5OBG55C-n/view?usp=sharing) :)

```ruby
library(ggplot2)              
library(tidyverse)           

EnergyConsumption <- read.csv("~/ADD YOUR PATH HERE/SelectedStateRankingsData.csv") 

mapdata3 <- map_data("state") ##ggplot2
mapdata3 <- right_join(mapdata3, EnergyConsumption, by="region")


daythree <- ggplot(mapdata3, aes(x=long, y=lat, group=group)) +
        geom_polygon(aes(fill=consumption_capita), color="black", alpha=0.9)+
  coord_fixed() +
  theme_light()+
  ggtitle("Energy Consumption per Capita (2020)") +
  theme(axis.line = element_blank(),
        axis.title.x = element_blank(),
        axis.title.y = element_blank(),
        axis.ticks = element_blank(),
        axis.text.x = element_blank(),
        axis.text.y = element_blank(),
        panel.grid.major = element_blank(), panel.grid.minor = element_blank(),
        plot.title = element_text(size=14, face="bold.italic", hjust = 0.5),
        legend.title = element_text(size=10), legend.text = element_text(size = 8),
        legend.position = "right") +
  scale_fill_distiller(name="Consumption per Capita\n(million BTU)",
                       palette = "RdYlGn",
                       direction = 1)

daythree
        
```

</p>
</details>

## Day Four

💚 Color Friday: Green

To many, EVs are seen as the future of the car industry, but how much momentum is the EV industry having as compared to "traditional" vehicles? In 2020, EV sales made up 4% of all vehicle sales. IEA's [Stated Policies Scenario (STEPS)](https://www.iea.org/reports/global-energy-and-climate-model/stated-policies-scenario-steps), which is described as "a more conservative benchmark for the future", shows that EV sales share for cars by 2025 is 15%, and by 2030 this increases to only 22%🥲

In the US, where [over 90% of adults commute to work in a personal vehicle](https://www.bts.gov/archive/publications/highlights_of_the_2001_national_household_travel_survey/section_01), by 2030 we are just below the world average at 21% od EV sales share for cars.

According to a [2021 article by McKinsey & Co](https://www.mckinsey.com/industries/automotive-and-assembly/our-insights/leaving-the-niche-seven-steps-for-a-successful-go-to-market-model-for-electric-vehicles), the biggest challenges facing manufacturers are:
- Regulatory Environment
- Customers
- EV Infrastructure
- EV Business Case and Profitability

<img src="https://user-images.githubusercontent.com/116127236/198754238-1a44ed1f-0649-446f-88e9-c6633fa291d1.jpeg" width="800" >

Data Credit: IEA (2021), Clean Energy Transition Indicators, IEA, Paris https://www.iea.org/data-and-statistics/data-tools/clean-energy-transition-indicators; [IEA Global EV Data Explorer](https://www.iea.org/articles/global-ev-data-explorer)

## Day Five

🇺🇦 Ukraine.

## Day Six

🌐 Network

## Day Seven

🖼️ Raster

## Day Eight

📖 Data: OpenStreetMap

## Day Nine

👾 Space

## Day Ten

🙃 A bad map

## Day Eleven

🔴 Color Friday: Red

## Day Twelve

⚖️ Scale

## Day Thirteen

⏲️ 5 minute map

## Day Fourteen

💠 Hexagons

## Day Fifteen

🥘/🍹 Food/drink

## Day Sixteen

🪧 Minimal

## Day Seventeen

🌲 A map without a computer

## Day Eighteen

🚙 Color Friday: Blue

## Day Nineteen

🗺️ Globe

## Day Twenty

🤟 "My favorite..."

## Day Twenty-One

💻 Data: Kontour Population Dataset

## Day Twenty-Two

:o: *NULL* 

## Day Twenty-Three

🏃‍♀️ Movement

## Day Twenty-Four

✴️ Fantasy

## Day Twenty-Five

💕 Color Friday: 2 colors

## Day Twenty-Six

🇮🇨 Island(s)

## Day Twenty-Seven

🎼 Music

## Day Twenty-Eight

🎉 3D

## Day Twenty-Nine

:basecamp: "Out of my comfort zone"

## Day Thirty

💿 Remix
