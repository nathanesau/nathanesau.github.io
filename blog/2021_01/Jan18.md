---	
title: Some Additional Projects	
date: 2020-01-18 22:42	
modified: 2020-01-18 22:42	
category: programming	
tags: sfu, cmpt225, projects	
Authors: Nathan Esau	
---	

## Some Additional Projects

For some reason, I was feeling really motivated to do projects in the last two weeks.

Hopefully writing them done in my blog will prevent them from getting lost.

* [chessapi](https://github.com/nathanesau/chessapi)	
* [rushhour](https://github.com/nathanesau/rushhour)
* [tfrealestate](https://github.com/nathanesau/tfrealestate)	
* [eductionblog](https://github.com/nathanesau/educationblog)	

I got pretty interested in Online Chess during the Pandemic. My initial idea was to create an API for loading chess games from PGN. It is written using Spring Boot and Thymeleaf. I also use [chessboardjs](https://chessboardjs.com/) for the interface. It is a work in progress. I thought it would be a quick project, but it turns out there are quite a few special cases to consider such as en pessant captures.

I really tried to polish the RushHour game. I did a few things here such as deploy a Qt app to the web using WebAssembly and creating docker images which are able to build the app. And I wrote a full GUI in Python and C++. The reason I got interested in RushHour in the first place, is because it was part of my first assignment for my online computing course this semester.

I spent an evening working on a real estate scraper. Selenium is used for scraping. Finding a website to scrape which didn't spam me with Captcha tests (Completed Automated Public Turing Test) was a bit of a challenge. My plan here was to scrape the website to a txt file every hour or so. The initial scrape would be slow. Subsequent scrapes would be faster since they woulds only need to process new listings. Once I have the data, I would then provide a Flask/ Django/ FastAPI backend to expose the data and a Vue.JS frontend to allow searching for data. Vue.JS would provide a table with listings near Vancouver Skytains. The site would allow users to filter results based on distance from a Skytain station (default: 2KM). Computing the distance between skytrain stations and properties is one of the trickier parts. Since we have skytrain address and property addresses, I was thinking that the Google Maps API would provide a way of figuring out the distance. I think this project has potential, I just don't have time to finish it right now.

I created an education blog using Python. Pelican is cool and I like the flex theme. It is a viable alternative to Jekyll although Jekyll is a little easier to setup in my opinion.

Also, I thought it would be fun to make a hockey pool site to use with family and friends but I haven't had time for that. And now that I got that WASM thing working for RushHour, it would be cool to put my [Rook game](https://github.com/nathanesau/RookGame) in the browser.
