---
layout: post
title:      "Nested Resources in Rails"
date:       2020-01-23 06:16:42 -0500
permalink:  nested_resources_in_rails
---


Resources are sets of routes that map requests made with HTTP verbs to actions (usually CRUD) in a controller, for a table which is represented by a particular Model in a rails application.  In the context of my rails Project Taskr, this could be described as 

A Project model which has an associated table in the database, that also has a projects controller to handle its CRUD actions.

In the routes.rb file of my project I first need to establish the routes for this with,

```ruby
#/config/routes.rb
Rails.application.routes.draw do

	root to: 'static#index'
	
	resources :projects
end
```

We can view the routes this has created by entering ```rake routes``` into the terminal from our project directory.

![](https://i.imgur.com/jp9vrWS.png?1)


And then define the Controller to handle these newly defined actions. 

```ruby
class ProjectsController < ApplicationController
	...
	
	def index
	@projects = Project.all
	end
	
	def new
	@project = Project.new
	end
	
	def create
	@project = Project.new(project_params)
	if @project.save
		redirect_to @project
	else
		rendrer 'new'
	end
	
	...
end
```

And within these actions we have now defined we can place the logic to get our actions working as inteded with the views.

Now we have the basis of a CRUD rails application, we can now go deeper and look at the nested aspect - in this case, adding an additional tasks resource to the projects, which in plain english will allow us to have all the crud functionality that we just created, but for tasks which will be associated to their parent Project resource. 

To better understand what this will look like we can go ahead and define the nested resource in our routes.rb file again. 

```ruby
#/config/routes.rb
Rails.application.routes.draw do

	root to: 'static#index'
	
	resources :projects do
		resources :tasks
	end
end
```

Now if we head back to our terminal to view the routes for the porject with the rake routes commands we can see the additional routes that have been added to the project. 

```rake routes```

![](https://i.imgur.com/9QMiVHn.png?1)

Here we can see that instead of the standard prefix for the routes being used for tasks, all task routes have a project prefix indicating we have correctly setup the nested routes.

After ensuring we have set up the controller with appropriate actions to handle the crud functionality of the tasks, we also need to remember to define the association between the two models, in this case a Project has many tasks and a task belongs to a project. 


```ruby
#/models/project.rb
class Project
	has_many :tasks
	...
end

#/models/task.rb
class Task
	belongs_to :project
	...
end
```


