---
layout: post
title: Everything about Facebook Messenger ChatBot
published: true
---

This Documentation is still not complete. Thank you for visiting my blog. Please check back after a few days.  
Facebook announced Bots for Messenger in April, 2016 making it possible for developers to connect with the more than 900 million people around the world who use Messenger every month.    
  
  
#### What are Bots for Messenger?  
Bots for Messenger are for anyone who's trying to reach people on mobile - no matter how big or small your company or idea is, or what problem you're trying to solve.   
Whether you're building apps or experiences to share weather updates, confirm reservations at a hotel, or send receipts from a recent purchase, bots make it possible for you to be more personal, more proactive, and more streamlined in the way that you interact with people.
  

#### So Let's get started!  
Let's look at the various chabot backend services to build our chatbot.  
Some of the available API services that can be used are as follows:  
- [wit.ai](https://wit.ai/home)  
- [Nuance Mix](https://developer.nuance.com)  
- [SiriKit](https://developer.apple.com/sirikit/)  
- [api.ai](https://api.ai/)  

### BASIC STEPS  

- Create  account in wit.ai using github credentials(https://wit.ai/home)
- Create chat conversions that you would like to create a bot for.
- Create a new project in wit.ai (https://wit.ai/apps/new)
- Now create stories in in this project in wit.ai along with it's correponding entities list
- Check out this(https://github.com/wit-ai/pywit) example in github using python
- Check docs for wit.ai here(https://wit.ai/docs)
- Get the Server Access Token for this wit.ai project from settings
- Access developers.facebook.com
- create a page for which you want to deploy your bot
- Create a facebook app for the page you created
- generate the page token id and page id for the page
- Now create a backend for facebook messenger using python
- For Facebook to be able to connect to our backend, we need to verify our callback endpoint using webhooks in developers.facebook.com
- So, go to https://developers.facebook.com/docs/messenger-platform/quickstart and follow the guide
- Now create a POST function in backend which can handle the calls from facebook which receives any message a user sends in through your page chat.
- This post function should pass the message and user id to another function which can process the data and send it to wit.ai to decide the actions it needs to perform
- Follow this link (https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps) to create a Flask application
- Follow this (https://gethttpsforfree.com/) to install HTPPS certificates in your server
