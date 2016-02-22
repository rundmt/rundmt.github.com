---
layout: post
title:  "Using Postman and Clarifai to tag photos"
date:   2016-02-10 12:56:37
categories: clarifai api postman
---

I'm going to go through as basic introduction of two of my favorite things. One is a Postman a graphical API client, and the other is Clarifai a image and video tagging service that allow us to quickly get information on our content. If you prefer videos I've made one down below.

<iframe width="420" height="315" src="https://www.youtube.com/embed/iJMxg-mcZXE" frameborder="0" allowfullscreen></iframe>

## Requirements

* Google Chrome
* Postman
* Clarifai Account

## What is Clarifai?

Clarifai is a company that offers image tagging as a service. You send them an image or a link to an image and they give you back image tags. 

## What is Postman?

Postman is a tool that allows us to send requests to API services like Clarifai. It's a very nice way to get up and running. The standard way of using CURL commands is hard and not very efficient. With Postman we get things like history, saved API calls, and a beautiful interface. 

## The Setup

### Clarifai

Navigate to [Clarifai's developer portal](https://developer.clarifai.com/) and sign up. Once you've signed up we need to create an application. Go and click "Application" on the right hand side.
You should see a page like this.

Click on "Create a new Application". Go ahead and create an application. It doesn't matter what you name it. Leave the other selections alone and click "Create Application."

![](http://i.imgur.com/SnW3lmf.png)

![](https://i.imgur.com/NTo8rXH.png)

Next go and click "Generate Access Token". You should see some randomized letters show up next to it. That is your access token save it some place, or just don't close your tab.

![](http://i.imgur.com/H2GVjUP.png)

### Postman

If you've ever used an API doc before you typically see something like this. In the black boxes those are what are known as CURL commands. CURL commands are commands to communicate with the web from your computers command line. CURL commands are great, but they are pretty daunting for somebody not used to the command line.

![](https://i.imgur.com/bKzI8l2.png)

That's why for this tutorial we're going to use Postman. Postman is a tool for users to interact with APIs using a graphical interface. You can download Postman in the chrome store. [ Link](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?utm_source=chrome-ntp-icon). Go ahead and add it.

Now if you go to your Chrome apps you can see Postman. Go ahead and open it.

![](https://i.imgur.com/qgEEQRW.png)

## The Request

Alright Clarifai gives us two options for tagging photos, but we will use the basic POST request API. If you don't know what the difference between a POST and GET request are, it is not a big deal. A POST request basically sends data outside of the URL and a GET sends data with the url.

So to the left of the url you will see something that says "GET". Click it and select POST instead.

To set it up in Postman put in the url  https://api.clarifai.com/v1/tag/


![](https://i.imgur.com/rNvrsxc.png)

In the headers tab place your authorization token like this:

![](https://i.imgur.com/bPoArNF.png)

Next click the body tag and put input url in the key and for the value put in a url to an image. We'll use http://www.clarifai.com/img/metro-north.jpg 

![](http://i.imgur.com/NY2rH0D.png)

All we have to do left is hit send. You should see a response in the box below with data.

![](http://i.imgur.com/VcKv6ki.png)

## Conclusion

Postman allows us to quickly test APIs in a very nice and quick manner. I personally use it for building and testing my own APIs. This tutorial is a quick one to get somebody up and running. I could see somebody using Postman along with Clarifai's feedback API. Their feedback API allows for the correction of tags. I would much rather use a nice interface like Postman than CURL calls for tasks like that.
