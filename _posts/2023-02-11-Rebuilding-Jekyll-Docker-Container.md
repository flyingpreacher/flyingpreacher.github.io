---
title: Rebuilding My Jekyll Docker Container
categories:
- jekyll, docker
tags:
- jekyll
- docker
- github
---

Since Github Actions was not publishing my site to GitHub pages, I had to find out what was wrong. Here it is: The pages-deploy.yml had changed significantly, and it did not work with my existing repo. I also found several other files that had changed as well. So, after considering my predicament, I decided that I would need to destroy my repo and replace it with a new one. I know that seems like a drastic step, but what was I to do?  

I think there is a way to update the Chirpy Repo, but I did not know how to do it. The documentation in the README does not tell you how, and Google did not either.  

I started from this page: <a href="https://github.com/cotes2020/chirpy-starter/generate" target="_blank">Chirpy Starter Template</a>  
I followed the directions <a href="https://github.com/cotes2020/chirpy-starter/" target="_blank">here.</a>  

I did not use the "bundle" command because my repo was going to be served in a Docker container.  

Now, I went back to Bill Raymond(remember him from the last post?) and followed his instructions to get back to the Docker container in VS Code. I transferred all my old posts and my other files to my repo, and I was up and running in a couple minutes! I didn't have to change my Dockerfile, but I did anyway. I uncommented the ruby line and put in my own FROM statement. Here it is:  

FROM ruby:3.0.5-alpine3.16  

I went back to Alpine because the Chirpy repo added a new Gemfile. Here is a snippet of what the relevant change was:
```
# Lock jekyll-sass-converter to 2.x on Linux-musl
if RUBY_PLATFORM =~ /linux-musl/
  gem "jekyll-sass-converter", "~> 2.0"
end
```  
This locked the troublesome jekyll-sass-converter to 2.0 so that Github could publish my pages through Github actions.  

After I made these changes, I was back up and running. I admit this was a frustrating challenge at times, but I am glad God helped me find a way to fix this.  

Thats all for now folks, and I will see you next time!😄
