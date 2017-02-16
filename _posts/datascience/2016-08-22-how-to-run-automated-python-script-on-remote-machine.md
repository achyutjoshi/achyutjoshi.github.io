---
layout: post
title:  "How to run automated python scripts on remote machines"
date:   2016-08-21 19:13:39
categories: datascience
comments : true

excerpt_separator: <!--more-->


---

I am currently working on the B.Tech Project that involves predicting flight prices. To build the models, I needed historical flight prices. Unfortunately, such data is not available and so I had to build a scraper to extract flight prices daily and save it in a csv file.

<!--more-->

Building a scraper is no rocket science. If you are using python, there are multiple frameworks like Scrapy, which are very powerful tools. My particular problem was not a complex one, and therefore I manually built a script which extracts the useful fields from Makemytrip website. You can look at the code [here](https://github.com/achyutjoshi/Flight-Prices-Scraper){:target="_blank"}.

Now, the most challenging part of this whole process was to schedule it. I wanted my script to run on a particular time, daily and everytime it runs, it should append the values to the original csv file. Scheduling it on my local machine was not a solution, because I cannot keep it running all the time.

I had two options - 

1. Run it on my institute’s server
2. Use virtual machines provided by [Microsoft Azure](http://azure.microsoft.com/){:target="_blank"} or [AWS](http://aws.amazon.com){:target="_blank"}

Due to some reason, the institute’s server was not responding. So the next best possible option was to use Microsoft Azure. AWS is better with respect to performance, but you need to be technically very sound to set up the server using AWS.So, I setup a virtual machine using the least possible configuration on Azure. It provides us with a INR 12k free credits on signing up. I used SSH to login into my remote system and installed python and all the libraries that were needed. 

Linux system provides a beautiful option called Cronjobs. It is an in-built scheduling option that is very easy to use. The major problem you can face when scheduling your scripts is the permissions of the file. Do make sure that you have given execution rights to all users(to be on the safer side). Also, if your script is writing/reading a file, make sure those files have the respective permissions. 

These are the few links that will help you to setup a cronjob and run a python script - 

1. [Quick Reference](http://www.adminschoice.com/crontab-quick-reference){:target="_blank"}
2. [Stack OverFlow - Python Script](http://stackoverflow.com/questions/8727935/execute-python-script-on-crontab){:target="_blank"}

To conclude, data science frequently requires the tedious job of collecting data. However, if you just learn the basics of scraping and scheduling scripts on a remote machine, your life will be a lot more easier.

