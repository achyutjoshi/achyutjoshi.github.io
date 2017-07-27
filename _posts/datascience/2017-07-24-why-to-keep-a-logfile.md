---
layout: post
title:  "Why to keep a log file and how to keep it in R?"
date:   2017-07-24 20:13:39
category : datascience
comments : true
excerpt_separator: <!--more-->
description : Log file is a file that records events that occur during a process. It basically helps to track back the process and discover if anything has gone wrong. Log File plays a very pivotal role in data science while working with large datasets distributed in several files.
keywords : "datascience, data, coding, programming, logfile, log file, how to create log files, r language, achyutjoshi, achyut, iitjodhpur, data science, large datasets, big data, bigdata, r"
---

One of the first things we are taught in Programming 101 is to write a well structured & commented code. And as any newbie would, we ignore this lesson and focus on achieving the end result. Continuing the same learnings, I coded a R(the R language!) script to be run on files amounting to 30GBs! This was my first professional experience after my graduation and I did not want to fuck up. So, I structured the code, wrote all the comments and ran it on all the files. And what happened next?

<!--more-->

All files were not structured the same way and so my script broke for a few files, leaving my final dataset void of some very important data. Moreover, my script was deleting some rows from every file, and thus again I was tampering with the original dataset without any logical and concrete reason behind it. It might not sound something as significant as not achieving the final goal, but believe me, in *data science if your data is not representative of the true dataset, your analysis is considered void.*

>Log file is a file that records events that occur during a process. It basically helps to track back the process and discover if anything has gone wrong.

__Reasons to keep a Log File__

So how to account for such cases? *Maintain a Log File*! If you need more reasons for maintaining a log file, here are few I can think of -

1. Large datasets follow Murphy's Law. *Anything that can go wrong, will go wrong.* And log file is the best way to keep a check
2. While running a common script on several multiple files, log file will give you a gist of the whole process
3. Log file will help for future reference, for your own self and also for others who will use the script or the dataset again.


__What to write in a log file?__

So, okay! I know log file is important, but what do I write in the log file? *It depends on the use case.* As someone who works with data daily, I usually maintain the following parameters in my log file -
* Total number of Files the script was run for
* File names
* Number of rows in each file (before and after processing)
* Number of Columns in each file (before and after processing)
* Any specific parameter important to the particular dataset
* Processing time


__How to keep a log file in R?__

{% highlight ruby %}
createLog <- function(df){
  log_con <- file("process.log",open="w")
  cat(nrow(df), file = log_con, sep="\n")
  ...
}
{% endhighlight %}

This is a very basic way to keep a log file. I prefer using this function in every script because it gives me the freedom to choose the contents of my log file.

Happy Coding!


---
---
