---
layout: post
title:      "CLI Portfolio Project"
date:       2019-11-08 17:43:14 -0500
permalink:  cli_portfolio_project
---

### The Idea
The idea I had for my CLI project was to create a tool that could be used by job seekers to conduct research on which companies they would like to apply to. To achieve this I started with a website that lists the top 100 companies to work for in the united states by employee satisfaction rating. To present the information in a usable way for the user I first needed to scrape the website for all of the information on the companies - this is because I intend for the CLI application to act as a search tool where the user ultimately filters the companies based on their preferences.

### The Scraper
I enjoyed coding the scraper and it's what I began with. Because the information for a company was split across two web pages, I would first need to take the company information that was on the index page and then open the company profile link to retrieve to remaining information, merge them together into one organised hash format and store that in an array of all companies. 
The main takeaway from the scraper was that to have my CLI application functioning as I wanted, I would need to scrape 100 different sites each time the scraper was called. I had to be cautious here to not send too many requests to the website while testing my project. Therefore I decided to paste the return value from the scraper in a variable to prevent getting blocked by the website.

### The Models
All of my scraped company profiles would then be passed into the main company model that would generate a new instance for each company and assign the respective instance variables to the scraped data.
My biggest issue faced here was to do with how I wanted the user to have the ability to search the list of companies based on certain properties. I decided I wanted both location and industry as the properties and so I created two models for these properties. Upon initialization, the companies would also need to make the link with these two models by saving an instance of themselves to the respective instances for those models. 
This took some time, but once I had the bulk of the work done for one of the models, the second model was very quick to get set up - a theme I found throughout working through this project.

### CLI
The command-line interface for my project took some thinking to work out how best to achieve the control flow for my application that I wanted. It was simple to set up the search tool so that users could see the company information based on their choices. The basic flow goes as follows:

1. Choose to search either by location or industry
2. Choose a particular location or industry once receiving all of the available choices
3. Choose a particular company within their chosen location or industry

Another issue I then ran into was giving the users the option to return back to any point in this process so that they can change their search preferences, without having to restart the application and scrape all 100 sites each time (not good!). Achieving this while adhering to DRY best practices proved difficult - I Already know of a few things I want to look into possibly improving here, but it works!

### Thoughts
* I had a few issues with using bundler at the start of my project, in particular setting up my environment correctly so that everything seamlessly worked like clockwork. Although I fell down the rabbit hole a bit here and went off reading the documentation for bundler, I ultimately got my issues resolved and gained a heap of knowledge on where bundler could trip me up in the future projects.
*  Sometimes when coding part of my project I was almost certain there must be a better way to achieve what I am trying to do, and sometimes I was right. What I've learned, is the best solution is the one you know, and this proved true for me during this project. Quite often I would get hung up on finding the best way and lose sight of the bigger picture and make little progress some days when I could have easily coded a functional solution to get more of the project completed and then come back to refactor later on.
