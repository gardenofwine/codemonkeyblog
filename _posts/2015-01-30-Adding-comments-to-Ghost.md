---
layout: post
---
Before publishing this blog I wanted to add the ability for users to post comments. I found this [great tutorial](http://ghostforbeginners.com/how-to-enable-comments-on-a-ghost-blog/) which I followed, but got stuck on step #8:

`The file you are going to edit is post.hbs and is located at:`

The problem is that the tutorial is meant for people self hosting ghost, that have access to the codebase of ghost. I have the code hosted on Bitnami, so in order to follow the tutorial I had to get access to the bitnami server.  Happily, bitnami wrote a [wiki page](https://wiki.bitnami.com/howto/How_to_connect_to_your_server) on how to do that. Although the wiki page is very detailed, I'll repeat the steps that worked for me (working on a macbook) for completness:

1. Download the PEM file and save it in your `~/.ssh` directory

![](/assets/Adding-comments-to-Ghost/download_pem.jpg)

1. Open Terminal.

1. Set the permissions for your private key file to 0600 using a command like the one below:

       $ chmod 600 ~/.ssh/bitnami-hosting.pem

1. Log in to the server using the following command:

       $ ssh -i ~/.ssh/bitnami-hosting.pem bitnami@<YOUR_SERVER_IP_ADDRESS>

## Editing without git

After connecting to the server and locating the ghost folder (`/home/bitnami/apps/ghost/htdocs`), I realized the source code is not source controlled; the files are just sitting there. It seems almost unholy, after working with git for many years, to edit source code files without a commit (and a commit message). However, I wanted to add comments so badly, that I went ahead and followed step #11 in [the tutorial](http://ghostforbeginners.com/how-to-enable-comments-on-a-ghost-blog/). But I certainly don't wish to continue working in this way. My options are

1. Set up a git repository on bitnami and manage it via a public github repository.
1. Find another blog hosting solution.

What do you think?
