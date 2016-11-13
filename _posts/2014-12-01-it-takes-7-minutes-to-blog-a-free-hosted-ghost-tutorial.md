---
layout: post
title: It takes 7 minutes to blog (a free hosted ghost tutorial)
---
I decided to setup my own blog website. I've had a couple of articles in my [company's website blog](http://notninjas.com/), and I've written a couple more, so I feel ready to set out on my own. In spirit of blog-as-you-work, I've started this very article as I set out to do this.

I love markdown, and I use [Mou](http://25.io/mou/) to write research documents and [gists](https://gist.github.com/) other than writing blog posts. I want to be able to just take an `.md` file and upload it. 
With that in mind, I set out to Google to find my blogging platform.

### Ghost
Someone blogged about how he liked [Ghost](http://karloespiritu.com/choosing-a-new-markdown-blog-platform/) as a blogging platform, and I liked what he wrote. Ghost is built with [node.js](http://nodejs.org/), and supports online editing with preview

![](/assets/it-takes-7-minutes-to-blog-a-free-hosted-ghost-tutorial/ghost.png)

This sounds great! However, the free version is just the source code. That's bad news because I love free stuff so I knew I was about to invest time trying to install Ghost on a [Heroku](https://www.heroku.com/) dyno, and that was going to take some time. Luckily, they made some [guides](https://github.com/tryghost/Ghost). Their [deploying Ghost](http://support.ghost.org/deploying-ghost/) guide had 3 hosting options, none of which was heroku, and none of which I had experience with.

### Bitnami

I decided to go and try the first one listed, [bitnami](https://app.bitnamihosting.com/). At a glance, Bitnami looked a lot like Heroku. They have a free service, too, which made me continue trying to create a Ghost server hosted on their cloud. It was pretty simple, too:

1. Create a bitnami account (or login using github, google or facebook)
2. [Enter your AWS access keys](https://wiki.bitnami.com/cloud/prepare_aws_account)
3. [Create a new Ghost app](https://app.bitnamihosting.com/servers/new) within bitnami (its basically a button to click)
![](/assets/it-takes-7-minutes-to-blog-a-free-hosted-ghost-tutorial/New app selection.png)
4. Wait for the server to launch (mine took 5 minutes)

#### Admin password
I had the server up and running pretty quickly, but I couldn't log in as admin and edit the content... Until I figured out my initial username and passowrd:

__username__ is your email used with your bitnami account.

__password__ was set up automatically by bitnami in the application's [Manage Server](https://app.bitnamihosting.com/servers/{server_id}/manage) panel.

##### tip
After you log into your server with the admin credentials mentioned above, you can change the password to whatever you want. I forgot the password and was then stuck, not being able to login and add content to the blog :( I tried to `ssh` into the server and edit the admin apssword manually, but decided it was easier to delete the ghost server and build anew.

the result is the page you are reading right now.
