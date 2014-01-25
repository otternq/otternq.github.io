---
layout: post
title: "Starting the EFactor API"
date: "2014-01-20 13:00:00"
tags: ["efactor", "api", "apiary.io", "apiblueprint"]
---

##Grape

Last week I started my [EFactor Project](//github.com/otternq/EFactor) and wrote about it ([here](http://blog.nickotter.com/2014/01/12/efactor.html)), and this weekend I wanted to learn more about Ruby API generation and API documentation in general.

So those were my goals Sunday: Ruby API, API Documentation.

In previous Ruby API searches, I had seen [Grape](https://github.com/intridea/grape) (self described as "An opinionated micro-framework for creating REST-like APIs in Ruby") and after some reading decided that I would use it for the EFactor API. The primary factor leading to this desission is that **Grape** runs on **Rack** which will allow me to run it along side the existing **Sinatra** interface.

For example, my *config.ru* only needed an additional 4 lines to include an API app. The file went from:

```
require 'bundler'  

Bundler.require

set :static, true
set :public_folder, 'public'

require './src/main.rb'

run MainController
```

to

```
require 'bundler'  

Bundler.require

set :static, true
set :public_folder, 'public'

require './src/app/main.rb'
require './src/api/api.rb'

# Here base URL's are mapped to rack apps.
run Rack::URLMap.new(
	"/" => MainController.new, 
    "/api" => API.new
) 
```

I also did a little restructuring so that the API and the Web App each have their own directories.

An added benifit of going with a **Rack** based solution is that I can write API endpoints just like I would with **Sinatra** or I can use the **Grape** entity/resource mixins.

##API Blueprint & Apiary.io

At this point it was really hard to stop myself from going into development mode and just coding out the api, but I had really wanted to do some proper API documentation/planning so that my API had a decent amount of quality. For a work project I'm slowly converting API documentation from a Word document to a Markdown document when I have some spare time, so I thought that I would write EFactor's documentation in Markdown and add it to the project's GitHub Wiki. I thought that would be a good delivery mechanism.

I started working on the file, just using Mou on my local computer...not using the GitHub Wiki editor and I wanted to see if there was an API format that I could use to make a table of contents. I ended up finding [API Blueprint](http://apiblueprint.org/) which provides a blueprint to follow and tools to generate a webpage based on the provided markdown. Awesome! It gets even better when I see the parent company has a service that will take that blueprint and host the generated documentation on a project specific subdomain, with Mock API endpoints.

This is great, I can write my API documentation with [Apiary.io](http://apiary.io/) which will generate and host my documentation. It will also incoorperate my GitHub repo so that when I make changes, they are saved to my repo's master branch. The inverse works as well, when I change the API documentation on my system, and merge the changes back into the master branch, a hook tells **Apiary** and the documentation website/mocks are updated.

Here is a screenshot of the generated API documentation using my API Blueprint written in *Markdown* (click to see full image):
[![EFactor Apiary Screenshot](/img/apiary-screenshot.png)](/img/apiary-screenshot.png)

This is pritty cool, I've generated detailed documenation for my API. It *should* have mock endpoints in case soemone was developing an Android app, then they would be able to use those mocks to see exactly what kind of data would be comming there way. Now I want to see just how good the mock endpoints actually are.

After starting up [Postman](https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en) I entered the API endpoint `/api/v1/worksession/52dcb465231dab2b52000002` which is the example *Work Session* in the API documentation and I recieved back:

```
{
    "_id" : "52dcb465231dab2b52000002",
    "start" : "2014-01-19T20:30:00Z",
    "end" : "2014-01-19T23:00:00Z",
    "note" : "Because TEST",
    "user_id" : "52dcb38c231dab0f97000001" 
}
```

which is the example response specified for that API endpoint.

[![EFactor Postman Screenshot](/img/postman-screenshot.png)](/img/postman-screenshot.png)

##Next Steps

My next steps with [EFactor](//github.com/otternq/EFactor) will be to code out the *Work Session* API endpoints and determinte the best way to authenticate the API. I will also look into adding SSL encryption my heroku app.

##The End

I'm glad that I spent the time the learn how **API Blueprint** and [**Apiary.io**](//apiary.io) work because I can see myself integrating it into other projects besides [EFactor](//github.com/otternq/EFactor). As far as my weekend coding goes, it was a slow from a coding view but more helpful in the long run.