---
layout: post
title:      "Sinatra Portfolio Project"
date:       2019-12-17 18:38:52 +0000
permalink:  sinatra_portfolio_project
---


For my Sinatra based project I chose to create an app where gem/jewel collectors can sign up creating their own account and from there log, track and view their findings in one location. Users have the ability to record different properties about their collection such as name/type, weight, colour and value. 

This sinatra project was the first project where I can easily see the foundations of how even some of the biggest MVC based web apps are formed and designed. Using ActiveRecord did seem like black magic that worked behind the scenes to make sure everything worked when ensuring the connections between models and tables were correct, but after working through the ActiveRecord labs in the procedural ruby section, I got an understanding of the kind of stuff that is going on underneath the hood and can see that it makes the lives of developer so much simpler.

Before starting the project I decided to plan out what I needed to create and - for the first time - what order to build the components to my project. I decided to build out this project in the following steps.

1. Database - Here I setup the two tables for my two models User and Jewel
2. Model - After defining the tables, I could then created the two models and setup the has_many and belongs_to relationships within the models after defining a user_id column in my jewel table.
3. Routes - After having the templates for my data all setup, creating the routes was the next step for structuring out the flow of my application.
4. Views - After predefining what views were to be rendered within certain routes, such as new.erb when creating a new instance of the Jewel model, it was easier to know exactly which views my application was expecting and helped indicate what data the views should be passing through to the controllers through various forms.


