---
layout: post
title:      "Rails Project"
date:       2020-07-18 01:27:43 +0000
permalink:  rails_project
---


Wow. Where to begin? I think this project was one of the most challenging project yet I think I have learned so much from this project, especially seeing everything come together and how routes work and how object relate to each other and build it into a real website. Although it is not the perfect app but I think it really helped my growth in the right direction. 
I ran into many issues while doing this project that had to be solved one by one. 
One of the earlier issues that I ran into was the has_many: :through relationships. I learned that you to have a has_many: relationship before your next line of code and have a has_many::through relationship. 
For example. 
```
class User < ActiveRecord::Base

    has_secure_password
    validates :name, presence: true
    validates :email, email: true 
    validates :email, uniqueness: true
    validates :password, presence: true


    has_many :artworks
    has_many :museums, :through => :artworks


end 
```

The user model has to have many artworks before it can know about the museums that these artworks belong in. 
It took me a few tries to understand this but it really deepened my understanding when I figured out you could directly called User.Museums because they were related through ActiveRecord. 
Another thing that we can see from this code snippet is the validates. I personally think validation is really cool and that i can control a lot of the data that I want. For example a email must be unique and there shouldn't be the same email in my database ever. 

I'm going to skip over to the database and talk about migrations. I think some of the rails ability to generate migrations/models were very helpful as well. For example typing in 
```
rails g migrations --------
```
really helped me set up a lot of migrations table easily and I can only imagine that having a lot of tables to generate how useful this action really helps. 

Now we get to the meat of the project. The CRUD of my controllers. 

```
class MuseumsController < ApplicationController
    before_action :verify_user_is_authenticated

    def index 
        @museums = current_user.museums
        
    end 


    def new
        @museum = Museum.new
    end 

    def create
        @museum = Museum.new(museum_params)
        if @museum.save
            redirect_to museum_path(@museum)
        else
            render :new
        end 
    end 

    def show 
        @museum = Museum.find_by(id: params[:id])
        if @museum
            render :show
        else
            redirect_to museums_path
        end 
    end 

    def edit
        @museum = Museum.find_by(id: params[:id])
        if @museum
            render :edit
        else
            redirect_to museums_path
        end 
    end 

    def update 
        @museum = Museum.find_by(id: params[:id])
        if @museum
            @museum.update(museum_params)
            redirect_to museum_path(@museum)
        else
            redirect_to museum_path(@museum)
        end 
    end 
    

    def destroy
        @museum = Museum.find_by(id: params[:id])
        if @museum
            @museum.destroy
            redirect_to museums_path
        else
            redirect_to museum_path(@museum)
        end
    end 

    private 

    def museum_params
        params.require(:museum).permit(
            :name,
            :location
        )
    end 

end 
```

After this project I am so much more comfortable in objects and edition objects and destroying them. Also one of the most important thing from this is the museum_params, which is what we get back from the forms and if we don't permit these tags, we will not be able to create a Museum in my case. So just learning about that was very cool and how to build out a full CRUD for the project helped me learn a lot. 

Another important learning through this project was the forms. 

```
<%= form_for @user do |f| %>
   
    <% if @user.errors.any? %>
        <ul>
            <% @user.errors.full_messages.each do |msg| %>
                <li> <%= msg %></li>
            <% end %>
        </ul>
    <% end %>

    <%= f.label :name %>
    <%= f.text_field :name %>

    <%= f.label :email %>
    <%= f.text_field :email %>

    <%= f.label :password %>
    <%= f.password_field :password %>

    <%= f.submit "Create User" %>

<% end %>
```

This produced label name, email and password and a box for user to enter in the information. Also in here was another thing that we learned which is that if there were any errors it would spit out a message telling us what the error was. But this form is what gets passed back to the Controller to create objects and i really liked how simple of a code it is but how powerful it is to generate a lot of crucial information that we needed for our project. Also learned about partials to reduce the coding that we have, I ended making the errors into a partial that way many of my forms can call upon it and use it and it becomes a one liner. It is just another very neat way to refactor the code and it was very cool to see how all that worked. 

The last part of the project I would like to talk about is the User/Session Control and authentication systems. I used Facebook Omni Authenticator and I kept running into issues for example it didn't pass a password on and therefore I could not create a User. After that I learned about SecureRandom.hex to generate random passwords to be passed in. However they were not in my originally specified password range of 6-20 characters. It was interesting to debug and solve out all the little bit of tiny issues that I had with omniauth and it was great to see the results come through. 

Another important topic has always been sessions, and I thought that after this project I am very comfortable with the ideology of users having sessions and that one should not be able to access certain data unless they are authenticated. 

All in all this project was great and I really learned a lot from it, although I ran into a bunch of problems but it all worked out in the end and I enhanced my coding skills! 
