---
title: How to Run Jekyll in a Docker Container Updated
categories:
- jekyll, docker
tags:
- jekyll
- docker
- github
---

So, I tried to go back to my old Jekyll site and login to make some new posts. I opened my site in VS Code, and it would not work. The problem was that my Jekyll theme had been updated, and one of the dependencies would not install. (sass-embedded)
<br><br>
Now I could either give up or find a way to fix it. (I got blazing angry several times in the process! 😤) Here is what I had to do: <br>

I found out the reason sass-embedded would not install is because it needed glibc. Alpine Linux, the OS that I was using for my docker container, does not support glibc. It only supports musl libc. So I had to find another OS to support the new container. <br>

I swear to you, it took me hours and hours searching the internet on how to add glibc to an Alpine docker container. At first I thought it was not even possible! In most of the information I found, it was not advisable to add glibc to Alpine or you are asking for trouble. <br>

Now I have to find a new OS for my docker container. Also, my existing Dockerfile only had the parameters for Alpine, and I didn't know what dependencies another OS would need to make the container. Here comes Debian Buster! When you go on Docker Hub, you have a listing for Ruby that has all the supported tags and respective Dockerfile links. Ruby is compatible with Debian or Alpine, and you can choose the link you need and add it to your Dockerfile.<br>

In my case, I used 3.1.3-slim-buster. here is how it looks on the dockerfile: FROM ruby:3.1.3-slim-buster. <br>

Next, I tried using the dockerfile with no dependencies just to see what would happen. As I expected, there was a major error because it was expecting build tools to be installed. So, I put on my thinking cap and tried to find out what package(s) I needed on Debian Buster to build software. I did some searching and discovered it was build-essential. <br>

I was almost ready, but I needed a way to make Buster install this when it was creating the docker container. So, here is what I put in the Dockerfile. Make sure you add the '-y' parameter to the RUN lines or installation of the packages will abort:<br>

RUN apt-get update && apt-get upgrade -y <br>
RUN apt-get install build-essential git -y
<br><br>
Thank Goodness for <a href="https://github.com/BillRaymond/my-jekyll-docker-website#benefits-of-using-docker-with-visual-studio-code-remote-container" target="_blank">Bill Raymond</a> again! When I looked at the entries he put in the Dockerfile for Alpine, I was able to figure out what I needed to use for Buster to work. Here is the complete Dockerfile I used to get my docker container up and running:
<br>
```
# Create a Jekyll container from a Debian Buster image

# At a minimum, use Ruby 2.5 or later
# Uncomment the following line if you want to use GitHub Pages (Jekyll 3.9.x):
# FROM ruby:2.7-alpine3.15
# Uncomment the following line if you want to use the latest version of Jekyll:
FROM ruby:3.1.3-slim-buster

# Add Jekyll dependencies to Alpine
#RUN apk update
#RUN apk add --no-cache build-base gcc cmake git

# Add Jekyll dependencies to Buster
RUN apt-get update && apt-get upgrade -y
RUN apt-get install build-essential git -y

# Update the Ruby bundler and install Jekyll
RUN gem update bundler && gem install bundler jekyll
```

As you can see, I left some of Bill's original entries in the Dockerfile for future reference. I commented out almost all of his entries and added my own. And guess what??<br>
IT WORKED!! 😂<br>

I am creating this page now from my new Docker container. 
<br><br>
It took a few minutes, but I enjoyed creating this post. Hopefully, I have written something that will help you as well. Thanks, and I will see you next time!

EDIT: Hold up. Everything is NOT fixed. Github Actions is not publishing my site to GitHub pages. 
<br>
You know what I had to do? Rebuild my old site from the chirpy-starter repo. I am going to make a blog entry for that soon. Thanks again for reading!!
