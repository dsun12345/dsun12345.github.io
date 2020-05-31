---
layout: post
title:      "Sinatra-Project"
date:       2020-05-12 16:25:12 -0400
permalink:  sinatra-project
---


Throughout this project, there were many challenges that had to be overcome, but I think it was a really good project in a sense that it brought everything together. First we began learning about how the the servers and databases interacted with one another. That is when we learned the Get request that sends the request and the server responds with data. I thought it was very interesting in how we set up our database and creating tables and then creating models so we could use them. In this project I think the most interesting thing that we learned was being able to evaluate ruby code in the view files. For example:
```
  
<h2>Welcome, <%=@user.name%></h2>	

<h3>All Songs</h3>	
<ul>	
  <% @songs.each do |song| %>	
    <li>	
      <%= song.id%>. <a href='/songs/<%=song.id%>'><%= song.name  %></a>, <%= song.artist%>, <%= song.genre %>, <%= song.release_date %>	
    </li>	
  <% end %>	
</ul>	

<a href='/songs/new'><button>Add to Song List</button></a> 

```

This view file allowed me to use the object that was created in my controller and it allowed me to pass the users name into my view file therefore when a certain user is logged in. It would recognize who it was. Also it also allowed me to take all the songs that belonged to that user and iterate it to protray the order it was created, the name, the artist, the genre and the release date. I thought this linked back to our first couple of lessons regarding object orientation and it was really cool to see how it plays into these projects and labs. 

One thing I also loved about this lab is how I started to figure out how to refactor code. For example in this part of the code: 
```
 post '/songs' do 	
    @song = Song.new(params)	
    @song.user = current_user 	
    if @song.save	
      redirect "/songs/#{@song.id}"	
    else 	
      erb :'songs/new'	
    end 	
  end 	
```

This part of the of code creates a instance variable @song that is created based on the params from our form. It then sets the instance variables, user to the current_user and if the variable could be saved we redirect it to the /songs/#{@song.id} to show it from our views. However there was a way to create method that could have been used that would refactor this code. It would look something like this: 

```
 post '/songs' do 	
    @song = current_user.songs.build(params)
    if @song.save	
      redirect "/songs/#{@song.id}"	
    else 	
      erb :'songs/new'	
    end 	
  end 	
```
This way, we are telling teh instance variable @song to build a new song that is created with the params that we took in from our form and we also used the current_user helper method so that the song knows which user it belongs to and it also shortens our code just a little bit. 

Overall this project really helped enhance the understanding of how server/database interacts and how we can create a form and get the information we want out of it and how to transfer it into new objects that we can store and use later on. It really helped enhance the understanding of how the whole web frame works. It was a tough project but I believe it was very well worth the effort and time to understand the basics of websites and how to manipulate the information. 










