---
layout: post
title:      "Sinatra Final"
date:       2020-07-12 20:39:27 +0000
permalink:  sinatra_final
---

I had a lot of fun using shotgun at localhost:9393 as I went through the labs and then with my final project for Sinatra. It was pretty cool to see my code in action displayed on a webpage. It was also a great learning experience to read the error messages on the webpage when I broke something. I am still working on getting out of my own head when something breaks and coming to terms with the fact that it indeed, is NOT the end of the world, but rather a learning experience that shows me pretty much where I need to make a change. 


I did enjoy creating the error messages for my project as well. It was not as daunting of a task once I figured out that I would just create several if/else statements. It was pretty straight forward and easy to implement.

For example:

	if params[:username].empty?
		@error_message = "Username must not be empty"
		return erb :signup
	elsif params[:password].empty? || params[:password].length < 6
		@error_message = "Password must be at least 6 characters"
		return erb :signup
	...
		
One of the difficulties I faced when working on this project was when and how to inject information in the erb files. It took me a little bit to get the hang of using <%= %>or just <% %>. If you do not want the information to be rendered you us <% %> and if you do want the information to show up on the page you use, <%= %>. For example: 

```
<% if @error_message != nil %>
    <div class="alert alert-danger" role="alert">
      <%= @error_message %>
    </div>
 <% end %>
```
	
Here the `<% if @error_message != nil %>` will not be rendered, it is only the logic for rendering the wrapped content. `<%= @error_message %>` will be rendered on the page if the error message exists.

I created a workout MVC Sinatra Application that used Active Record. A user can create an account, login and logout, add a workout, edit the workout, and delete the workout. A user who created the workout is the only one who can edit the workout, but another user has the ability to add that user's workout to their own workout history and vice versa. This allows users to share workouts with each other and keep track of the workouts that they have done. It ensures that a user can edit and delete only their own resources - not resources created by other users.
	
I was able to add some CSS Bootstrap features to make my application more eye catching and more fun to interact with.
	
Check out my full project [here](https://github.com/HGouin/workout-tracker)
	
<iframe src="https://giphy.com/embed/Q8IYWnnogTYM5T6Yo0" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/focusfeatures-brad-pitt-burn-after-reading-focus-features-Q8IYWnnogTYM5T6Yo0">via GIPHY</a></p>
	

	
	
