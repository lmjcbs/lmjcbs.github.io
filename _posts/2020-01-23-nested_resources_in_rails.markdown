---
layout: post
title:      "Nested Resources in Rails"
date:       2020-01-23 11:16:42 +0000
permalink:  nested_resources_in_rails
---


Resources are sets of routes that map requests made with HTTP verbs to actions (usually CRUD) in a controller, for a table which is represented by a particular Model in a rails application.  In the context of my rails Project Taskr, this could be described as 

A Project model which has an associated table in the database, that also has a projects controller to handle its CRUD actions.

In the routes.rb file of my project I first need to establish the routes for this with,

```ruby
#routes.rb
Rails.application.routes.draw do

	root to: 'static#index'
	
	resources :projects
end
```

We can view the routes this has created by entering ```rake routes``` into the terminal from our project directory.

```bash
~/development/code/projects/taskr   rake routes
	
									projects GET       /projects(.:format)                                                                         projects#index
																	POST      /projects(.:format)                                                                         projects#create
					new_project GET       /projects/new(.:format)                                                               projects#new
					 edit_project GET       /projects/:id/edit(.:format)                                                         projects#edit
											project GET      /projects/:id(.:format)                                                                  projects#show
																	PATCH    /projects/:id(.:format)                                                                  projects#update
                                      PUT      /projects/:id(.:format)                                                                  projects#update
																	DELETE  /projects/:id(.:format)                                                                  projects#destroy
```

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
#config/routes.rb
Rails.application.routes.draw do

	root to: 'static#index'
	
	resources :projects do
		resources :tasks
	end
end
```

Now if we head back to our terminal to view the routes for the porject with the rake routes commands we can see the additional routes that have been added to the project. 

```bash
~/development/code/projects/taskr   rake routes
	
							project_tasks GET      /projects/:project_id/tasks(.:format)                                        tasks#index
																				POST     /projects/:project_id/tasks(.:format)                                         tasks#create
		 new_project_task GET      /projects/:project_id/tasks/new(.:format)                                tasks#new
			edit_project_task GET      /projects/:project_id/tasks/:id/edit(.:format)                          tasks#edit
								 project_task GET      /projects/:project_id/tasks/:id(.:format)                                  tasks#show
																				PATCH    /projects/:project_id/tasks/:id(.:format)                                  tasks#update
																						PUT     /projects/:project_id/tasks/:id(.:format)                                   tasks#update
																			DELETE   /projects/:project_id/tasks/:id(.:format)                                   tasks#destroy
												 projects GET      /projects(.:format)                                                                            projects#index
																				POST     /projects(.:format)                                                                             projects#create
								new_project GET      /projects/new(.:format)                                                                   projects#new
								 edit_project GET      /projects/:id/edit(.:format)                                                             projects#edit
														project GET     /projects/:id(.:format)                                                                      projects#show
																			PATCH    /projects/:id(.:format)                                                                       projects#update
																					PUT      /projects/:id(.:format)                                                                       projects#update
																		DELETE   /projects/:id(.:format)                                                                       projects#destroy
``` 

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
	end
	```


