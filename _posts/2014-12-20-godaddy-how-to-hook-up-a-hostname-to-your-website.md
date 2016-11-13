---
layout: post
title: GoDaddy - How to hook up a hostname to your website
---
	
I bought the domain codemonkeyblog.com at [godaddy.com](godaddy.com), and now I want to hook up [my blog site](http:://codemonkeyblog.bitnamiapp.com) to this url.

As usual, I started out by googling. Pretty quickly I found out I lack a lot of knowledge in how the internat works. Take [this tutorial](https://wiki.bitnami.com/BitNami_Cloud_Hosting/howto/Assign_a_Custom_Domain_to_Your_Server) by bitnami itself (Where I am hosting my blog app). According to this tutorial, there are two ways to "assign a custom domain to your server". It seems I didn't even know the correct way to name "hook up a hostname to your website". Just from skimming the tutorial, I encountered terminology that is new to me:

1. A-record
1. CNAME
1. Elastic IP
1. Zone File

At any rate, There are two ways to "assign a custom doamin to your server", and I chose the first one to follow.

 1. Configure the Domain in your DNS Provider with A-record
 1. Configure the Domain in your DNS Provider with CNAME


## Configure with an A-record

I tried this method first, since it was written first in the bitnami tutorial. What I was required to do is 2 things
 1. Assign a static IP to my bitnami app. This is done through the bitnami app manage console.
 1. [Configure the A-recod in godaddy](https://support.godaddy.com/help/article/680/managing-dns-for-your-domain-names)

It seemed to work. I got bitnami to assign a static ip address to my ghost blog instance application, and get godaddy to point to this address. However, what actually happened, is that instead of  _codemonkeyblog.com_ pointing to _http://codemonkeyblog.bitnamiapp.com/_, it was pointing to  _http://ghost.codemonkeyblog.bitnamiapp.com/_, which is bitnami's admin console:

![](/assets/godaddy-how-to-hook-up-a-hostname-to-your-website/admin console.png)

It turns out I missed a step in configuring my bitnami app. I had to [configure the url for my bitnami application] (https://wiki.bitnami.com/BitNami_Cloud_Hosting/Applications/Domain_Name#Configuring_the_URL_for_the_application).

#Summary

In order to make my domain codemonkeyblog.com to point to my blog application instance on bitnami, I had to go through 3 steps:

 1. [Assign a static IP to my bitnami app. This is done through the bitnami app manage console](https://wiki.bitnami.com/BitNami_Cloud_Hosting/howto/Assign_a_Custom_Domain_to_Your_Server#Assign_Static_IP_Address_to_the_Server).
 1. [Configure the A-recod in godaddy](https://support.godaddy.com/help/article/680/managing-dns-for-your-domain-names)
 1. [configure the url for my bitnami application] (https://wiki.bitnami.com/BitNami_Cloud_Hosting/Applications/Domain_Name#Configuring_the_URL_for_the_application).

#What the hell did I just do?
I got through the steps of setting up the domain, but I have no idea what I have done. I'm going to read more about a-records and CNAMEs so I'd be able to look myself in the mirror
