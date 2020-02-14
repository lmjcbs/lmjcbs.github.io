---
layout: post
title:      "Using Serializers to Pass Data to the Frontend"
date:       2020-02-14 07:47:25 -0500
permalink:  using_serializers_to_pass_data_to_the_frontend
---


In my JavaScript Project Devboard I chose to make use of rails as an api instead of an entire rails application like in my previous rails project taskr. To use rails in api mode simply create a new rails project using the api flag.

`$ rails new devboard-api --api`

This generates the project normally however with a few key differences. Most importantly ApplicationController will inherit from ActionController::API instead of ActionController::Base and the fact that view files will no longer be generated when using scaffolding.

Within the rails project actions within the controller now need to change how we are returning the data. As we will be using JavaScript for the frontend, we need to use a common ground between Ruby and JavaScript, a format that both langauges can parse and encode to - in our case that format is JSON. 

To implement this change we simply set the actions to return the output in JSON instead of a particular view file with the following.

```ruby
  # GET /positions
  def index
    render json: Position.all
  end
```

Now we can see the result by going directly to the url `project_url/positions` which sends a get request to our index action in the positions controller, but instead of rendering the view we are now presented with an array of our position objects.

```
[
	{
		id: 1,
		title: "Lead Frontend Developer",
		company: "Amazon",
		description: "We are searching for our next lead frontend developer.",
		salary_gbp: "150000",
		experience_required: "5 years",
		location: "London",
		category: "Frontend",
		technology: "React"
	},
	...
]
```

This is all as expected, however the the position object attribute names have been sent to the frontend still using ruby naming coventions - see `experience_required: "5 years"`. This isn't the end of the world, however it then adds the additional job of  renaming on the frontend if the object keys are expected to follow JavaScript camelCase naming conventions - even more so if a team split up into backend and frontend respectively was working on a larger project.

To fix this issue we can make use of serializers in rails to define exactly what data we wish to pass to frontend when handling a request as well as how exactly to present that data. Firstly we need to enable the use of serializers in the project but uncommenting the rails serailizers gem that comes with rails in API mode.

```ruby
	#gemfile.rb
	gem 'active_model_serializers'
	
```

then run `bundle install` so it's ready to go.

Next we need to create the serializers for each model in our project we wish to serialize. To do this create the serializers in a new folder called serializers from within the app directory and the define the class with the attributes we wish to send.

```ruby
	#/app/serializers/position_serializer.rb
	class PositionSerializer < ActiveModel::Serializer
		attributes :id, :title, :company, :description, :salaryGBP, :experienceRequired, :location, :category, :technology
	end
```

Here we've formatted :experience_required to :experienceRequired, however :experienceRequired isn't an column on our positions table, to fix this we can define an attrbute method to return a desired value. in our case the experience_required attribute value.

```ruby
	#/app/serializers/position_serializer.rb
	class PositionSerializer < ActiveModel::Serializer
		attributes :id, :title, :company, :description, :salaryGBP, :experienceRequired, :location, :category, :technology
		
		def experienceRequired
			self.object.experience_required
		end
	end
```

After going ahead and changing the attribute names and adding their respective methods, if we now go back to our `project_url/positions` url, we'll see the changes in the JSON object.

```
[
	{
		id: 1,
		title: "Lead Frontend Developer",
		company: "Amazon",
		description: "We are searching for our next lead frontend developer.",
		salaryGBP: "150000",
		experienceRequired: "5 years",
		location: "London",
		category: "Frontend",
		technology: "React"
	},
	...
]
```
This formatted JSON object could now be destructured and used directly without having to rename the attributes 🙌







