---
layout: post
title:      "has_many and belongs_to relationships"
date:       2019-12-19 10:37:49 -0500
permalink:  has_many_and_belongs_to_relationships
---


Active record offers up a whole host of associations that we can use to establish relationships between our models.

* belongs_to
* has_many
* has_one
* has_many :through
* has_one :through
* has_and_belongs_to_many

In this blog post i'll be looking into the belongs_to and has_many associations in more detail, as well as showing how to use the associations in the context of my Sinatra Project  jewel-tracker.

First we want to make sure we have ActiveRecord setup correctly in our models. To achieve this we need to inherit ActiveRecord into the models. In my case this a Jewel and a User model.

Next we want to establish the direction of the relationship. A User should be able to create instances of jewels they collect, therefore a jewel should also have a owner. Using this information we can determine that a user should have many jewels and a jewel should belong to a user.

Our two models should now look as follows.

```ruby
class Jewel < ActiveRecord::Base

  belongs_to :user

end
```

```ruby
class User < ActiveRecord::Base

  has_many :jewels

end	
```

**Note:** Ensure the model name which has the belongs_to association is pluralized when referring to the model from the has_many association, in this case **:jewels**.

The next step is to ensure ActiveRecord can make the link between the two models once their instances have been persisted to the database.  As the direction of the has_many belongs_to relationship is one way, we only need add a key to our jewels model, which should be named after the model with which it shares the realtionship. 

We can do this by adding a user_id column to our jewels table.

Our database schema file should now reflect this addition.

```ruby
ActiveRecord::Schema.define(version) do

  create_table "jewels", force: :cascade do |t|
    t.string  "name"
    t.string  "weight"
    t.string  "colour"
    t.string  "location_found"
    t.string  "value"
    t.integer "user_id"
  end

  create_table "users", force: :cascade do |t|
    t.string "username"
    t.string "password_digest"
  end

end	
```

The important part here being the user_id column we have defined in the jewels table. We don't need to include a seperate key for the users table when building this relationship as the user_id column will refer to the primary_key  or id attribute of the user model.

Which brings me onto the next step - creating the link within our application. These steps alone aren't yet enough for us to be able to use the methods made availiable to us through the relationship. Ideally we'll want  to establish the relationship by setting the the jewel.user_id attribute to the id attribute of the user, as the user instantiates a new jewel model.

If we were currently logged into a user, and wanted to create a new jewel model, we could achieve this with something like.

```ruby
user1 = User.create(name: "Jack")
jewel1 = Jewel.create(user_id: user1.id, name: "Emerald")
jewel2 = Jewel.create(user_id: user1.id, name: "Sapphire")
```

**Note:** We assign the id attribute of the user to the user_id attribute.

Now we have done all the hard work and successfully implemented a has_many belongs_to relationship.

Going forward we can now make use of the methods made availiable to us through ActiveRecord associations. Using the example above, if we wanted to get a list of all jewels that user1 has created we can use call the .jewels method on the user.

```ruby
user1 = User.create(name: "Jack")
jewel1 = Jewel.create(user_id: user1.id, name: "Emerald")
jewel2 = Jewel.create(user_id: user1.id, name: "Sapphire")

user1.jewels # => [
{id: 1, name: "Emerald", user_id:  1},
{id: 2, name: "Sapphire", user_id: 1}
]
```

Returns an array of jewel objects that belong to user1, we can then find out more information about the user from these jewel objects.

```ruby
user1.jewels.first.user # => {id: 1, name: "Jack"}
```

Returns the user object that created the jewel instance .user is being called upon.

As these methods return standard ruby data types such as arries and objects, we can also take advantage of methods available to us through ruby's standard library to retrieve more information.

```ruby
user1.jewels.size # => 2
```











