---
layout: post
---
I decided to hook up my blog site to github, for backup. So I hooked up via ssh into my instance machine.

       $ ssh -i ~/.ssh/bitnami-hosting.pem bitnami@<YOUR_SERVER_IP_ADDRESS>

Now I went to my app directory:

       $ cd apps/ghost/htdocs/

And started a git repository (Bitnami comes with git pre installed)

       $ git init
       $ git add -A
       
After running `git add -A` I noticed I was adding all the node_module directory, because I forgot to edit `.gitignore`. No problem, I just need to revert:

       $ git reset --hard
       

![](http://media.giphy.com/media/rod1LnilW2rDO/giphy.gif)

I removed all the files from the directory. There is no way to recover (I tried). The reason being that I haven't even made a single commit; there is no HEAD. All my files turned to nameless blobs in in .git object tree, and no wat to recover. My blog site now looks like this:

![](/assets/horrible-git-mistake/Website after break.png)

## Next steps
I have decided not to take this too bad. Afterall I have all the content on my machine, and I can easily prop up a new blog site (Using my own tutorials). This time, I'll set it up right with backups. 
               