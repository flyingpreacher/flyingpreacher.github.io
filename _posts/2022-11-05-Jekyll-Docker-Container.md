---
title: How to Run Jekyll in a Docker Container
categories:
- jekyll, docker
tags:
- jekyll
- docker
- github
---


I was tired of installing Jekyll on my PC everytime I needed it. Trying to get all the dependencies right was a PITA! So, when I read about the possibility of installing it ONE time in a container and never having to set it up again, I was intrigued! 

Here is how I did it with some help from Bill Raymond:

I watched the video below on YouTube:<br>
<a href="https://www.youtube.com/watch?v=owHfKAbJ6_M&list=PLWzwUIYZpnJuT0sH4BN56P5oWTdHJiTNq&index=3" target="_blank">Develop Jekyll websites in a container</a>


After you watch it, try following the instructions step-by-step here: <br>
<a href="https://github.com/BillRaymond/my-jekyll-docker-website#benefits-of-using-docker-with-visual-studio-code-remote-container" target="_blank">https://github.com/BillRaymond/my-jekyll-docker-website#benefits-of-using-docker-with-visual-studio-code-remote-containers</a>


I must say that Bill helped me a lot when I did not know what to do. I had tried other things before this method because I was afraid to mess up my existing Github repo. But when it came down to it, this was the best option, and it worked!<br>

Here is something I did differently to make it work for me. <br>
In step 7, when it came time to build the Jekyll website, here are the commands I did in the terminal: <br>
```bash
bundle init
bundle add jekyll --version "~>4"
bundle install
bundle update
```
I did not need the last 4 commands that Bill posted on his GitHub guide because I already had an existing Jekyll site. Then, I followed the rest of the tutorial on the GitHub page, and finally I had a working Jekyll site in Docker!

Jekyll is still a bit hard(to me), but after some practice, I think I am gonna like it. See you next time!

P.S. I did this on Ubuntu 22.04, but you can do it on Windows 10 as well.
1. Go to this website to install Docker for Windows: <a href="https://andrewlock.net/installing-docker-desktop-for-windows/" target="_blank">https://andrewlock.net/installing-docker-desktop-for-windows/</a>

Ok. STOP. The --livereload directive is not functioning on Windows. When you save your post with corrections, nothing happens in the terminal which means that it is not working. I am going to Google this and see what is happening.

This is a known problem without a good solution: I checked <a href="https://talk.jekyllrb.com/t/livereload-option-not-working-on-windows-10/5769/10" target="_blank">Here.</a>

I guess I will have to do all my work in Ubuntu. Cheers!
