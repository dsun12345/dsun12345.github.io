---
layout: post
title:      "JS Project"
date:       2020-09-01 22:15:17 +0000
permalink:  js_project
---

 
Wow! It's really been a roller coaster ride. Now that We've begun to learn about Javascript it was like a whole new world. One thing that was really cool was that we didn't create and render forms within rails. It made the backend rails app a lot simpler once you got rid of the forms and all you had to do was create the database and relationships and then pass that data on and store the data. Another very neat gem we used was the FastJSON gem. It allowed us to use serializer to get a nested hash of data which we could access, and again it was so easy to set up and get everything in relationships. 
```
class ArtistSerializer
  include FastJsonapi::ObjectSerializer
  attributes :name
end

```

```
    def index
        songs = Song.all
        render json: SongSerializer.new(songs)
    end 
```
All we needed were some lines of code and some seeds in our database and we could spit back out a whole nested hash that we could use to manipulate what we need and what we don't need. 
For this project I followed the method of thinking about what I need to create and how I need to get there. I really liked music apps and so I tried to figure out how webpage version of music players like spotify/youtube music work etc. How they are able to constantly change the album/artist picture and update the content you are playing. So I decided to come up with a album/song interface, where you could enter the song name genre and link a album_picture_url and assign it to an artist. 

Throughout this project It was really interesting manipulating the DOM, I think that is what I found most interesting and I spent loads of time in debugger just to play around with DOM and see what information I can get out of the variables I was using. Things like document.querySelector to find the node/id you were looking for and how to utilize it. 
For example in the following code:
```
function updateFormHandler (e) {
    e.preventDefault();
    let id = parseInt(e.target.dataset.id);
    let card = document.querySelector(`[data-id="${id}" ]`)
    let song = Song.findById(id);
    let title = e.target.querySelector('#input-title').value;
    let genre = e.target.querySelector('#input-genre').value;
    let album_url = e.target.querySelector('#input-url').value;
    patchSong(song, title, genre, album_url)
    card.querySelector(".card-title").textContent = "Title: " + title
    card.querySelector(".card-text").textContent = "Genre: " + genre 
    card.querySelector(".card-img-top").src = album_url
}
```
As we can see I had to assign the value of card to find the specific data card I was looking for. 
My HTML for the render card looked like this. 

```
        <div class="col-md-4" data-id=${this.id}>
          <div class="card mb-4 shadow-sm">
            <img src=${this.album_url} class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">Title: ${this.title}</h5>
              <p class="card-text">Genre: ${this.genre}</p>
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group">
                  <button onclick = "myFunction()" type="button" class="btn btn-sm btn-outline-secondary" data-id=${this.id}>Edit</button>
                </div>
                <small class="text-muted">${this.artist.name}</small>
              </div>
            </div>
          </div>
        </div> `      
```

so that's why I had to then do card.querySelector(".card-title").textContent to actually update the Title of the song during my edit function. I had a lot of fun just playing around with debugger and exploring how to grab the information I want and then utilizing it in the way that I had envisioned. I also found it really fun to have event listeners listening for clicks and a certain action that the user puts on the webpage and then responding. That was very fun to see how all that worked out and how you can listen to multiple events at once was very interesting. 

This project was very challenging in the aspect that I think we had to connect front end and backend using Javascript and Rails. It was a very cool collaboration effort and now I see how the webpage can update things first and then decide whether they want to pass that data/save that data to the backend later. This project overall helped me learned a lot more Javascript and has got me started on the question whether I want to work on backend or frontend. That will be the question to answer! 

