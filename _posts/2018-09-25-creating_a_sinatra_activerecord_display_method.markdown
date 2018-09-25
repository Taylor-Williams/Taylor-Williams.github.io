---
layout: post
title:      "Creating a Sinatra+ActiveRecord #display method"
date:       2018-09-25 05:03:04 +0000
permalink:  creating_a_sinatra_activerecord_display_method
---


As i was going through and creating my views for my [Trail Tracker](https://github.com/Taylor-Williams/trail-tracker) I found myself getting annoyed by how i was displaying attributes. does this instance of a model have some attribute? display it. what about this next attribute? if yes, display; if no, do not display. not only does it feel ugly to write out, it feels worse to copy paste for your next object to try and display their traits. Each time you add this 'read' functionality to your program it means copying the same gist of pseudocode and then hand-writing each attribute to fit that specific object/model. it's not just Write Everything Twice, it can be Write Everything (Three-times-plus-add-different-boolean-checks-and-maybe-put-different-unit-information).

For instance lets say I have Users who have a: username, email, bio, and list of created Posts; then the first time i tell my web application to display that User i am fine saying the following pseudocode:

```
Username: (user.name)
Email: (user.email)
Bio: (user.bio) if user.bio?
Created Posts: (User.created_posts.each do {print post name with link to the Post}) if user.created_posts?
```

In this example i didn't give checks for the username and email attributes because i am assuming they were mandatory to create a User. Okay this is no problem, but now I should make it so that someone can actually check out the Post. So once we make the view file for seeing any given post, what do we do? copy the above code and paste it in. Then comes the manual labor of going through all the attributes i want to see. Copying the most similar line of the above code and changing all the 'user's to 'post's and changing the attribute name. When it comes to debugging errors for these views it can be a pain because depending on the way you requested information from your database you need to switch between asking for presence or asking if the collection of objects is empty. and what if you have another couple objects to do this with? or you have an object with many many attributes to display? This really seems like something we should solve elsewhere and call for each object to display themselves. My creativity knows no bounds but i like the idea of a #display_self method.

So what's the best way to do this? I am running into two lines of question, what's the best way to dynamically display the information of each object and who's responsibility is this? I think the first question is dependent on the second so lets go for finding out how I want to do this.

Let's think about what i want. I want an object to be passed into this view file and I want it to say "here's the information you have asked to be able to display, and here is all of that information in a formatted style". Is that the responsibility of the file to ask for all the attributes that you want to see? Could be, if you had a number of different ways that you wanted to display information based on levels of security. Or, if you wanted to show a small number of attributes for that object in different places around the site. But for my application I wanted all my showing views to show all of that objects' interesting information. Okay so i do not want this to be the responsibility of the file. next level up is the controller. Do i want the controller to have the responsibility of finding the objects important information and then passing that into the file? Again I'm sure that there are applications where this would make sense but I don't want my server to do all that huffing and puffing every time it just wants to display a single object. Next level up is the model, and I think this is the place that i want to implement my solution. Why? because the model should be responsible for knowing which information about itself is important to display, and it should know whether or not an object has that important information. Then it should be able to display itself in the desired format. Thematically by making this decision i am saying: It is the responsibility of an object to display its attributes rather than the responsibility of the controller or view to decide which information to display.

okay, so it's the model where i want to make a change. let me repeat what i want my solution to look like:  I want it to say "here's the information you have asked to be able to display, and here is all of that information in a formatted style". What we need is the model to know which attributes to display, which ones it has, and then create the formatted sentence for that attribute.

my current working form of that solution is this, in each model that wants to impliment it:
```
  mattr_accessor :display_attributes
	self.display_attributes= %w((insert your attributes here, not this string))

  def display_self(**options)
    make_self_display() unless @display_self
    if options
      @display_self.map do |k, v|
        options.keys.include?(k) ? v + " " + options[k] : v
      end
    else
      @display_self.values.flatten
    end
  end

  def make_self_display()
    @display_self = {}
		self.class.display_attributes.map do |attribute|
			if self.send(attribute)
				@display_self[attribute.to_sym] = "#{attribute}: #{self.send(attribute)}"
			end
		end
		if self.state
			@display_self[:state] = @display_self[:state].slice(/(.+: )/) << "<a href=\"\/states\/#{self.state.code}\">#{self.state.name}</a>"
    end
  end
```
The next step would be to make this a module which is implementable to multiple classes at a time, but... one step at a time.
