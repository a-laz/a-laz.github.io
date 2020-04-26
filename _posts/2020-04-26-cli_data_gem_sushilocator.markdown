---
layout: post
title:      "CLI DATA Gem SushiLocator"
date:       2020-04-26 19:35:30 +0000
permalink:  cli_data_gem_sushilocator
---



When i first got to the clid data gem project,  the workload was a bit daunting.  I had no idea where i wanted to start. My thoughts were all over the place and my first idea, a Corporate Tax Rate Locator per State was pretty basic. Each state would have info about its State Income Tax rate. I thought that wasn't enough info for each instance of the State Class and for me to get more info i would need to scrape multiple websites. Maybe in the future but right now i know that was biting off a bit more then i could chew.

So i thought what do i like asides from business?

Oh Yea?! SUSHI!!!!

![](https://media.giphy.com/media/OqI2ndSLj1wdi/giphy.gif)

Then the idea struck. Why don't i make a Sushi Locator app that finds the best sushi spots near you.

I decided i would need 3 employees or (classes) to make my app work.

I needed a Scraper, Restaurant, and CLI class.

The Restaurant class would be the blueprint for each sushi place and would be responsible for creating instance attributes that would store information such as , name, the state of the restaurant instance (wheter it was opened or closed), number of reviews and a link to a full review of the restaurant.

When i relaized that status of each restaurant was a "live feed", i felt super accomplished, Like i had really just made something worth something, you know?

The Scraper class would be  responsible for scraping the data off of trip advisor and creating instances based off of the data that was scraped.

Lastly the CLI class, was our customer service specialist. It would display the list of "all" Sushi Restaurants, ask our user for their choice of place and then return all the necessary information about the user chosen restaurant.

I started with the Scraper Class as i knew i needed to find out which data i need to scrape and how i would parse that data to get exactly what i was looking for. Then the Restaurant class so the scraper could use the data it scraped and initialize a new restaurant instance. FInally the CLI class to get the interface working and finally the run file in the bin folder. 

To anyone starting this project for the first time, THIS will be harder than anythjing you have done so far in the course, BUT TRUST ME, THIS is the most rewarding experience so far as once you build the functional app from nothing you will see all the prgress you have made so far and how much you have grown as a software developer. 
