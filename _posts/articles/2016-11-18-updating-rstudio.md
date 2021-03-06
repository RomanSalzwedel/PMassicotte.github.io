---
title: "Installing latest version of RStudio from R"
layout: post
---

If you are like me, chances are that you update  [RStudio](https://www.rstudio.org/download/daily/desktop/ubuntu64/) on a daily basis. Here is a small R script that automatically download and install the latest version of RStudio on your computer. Note this is for ubuntu64 based systems, but this can be easily modified for Windows or Mac platforms.


{% highlight r %}
rstudio_ubuntu_daily_url <- "https://www.rstudio.org/download/daily/desktop/ubuntu64/"

r <- readLines(curl::curl(rstudio_ubuntu_daily_url))

file <- regmatches(r, regexpr("https\\S+?deb", r))[1]
file

destfile <- paste("/tmp/", basename(file))

download.file(file, destfile = destfile)

cmd <- sprintf("dpkg -i %s", destfile)
system(cmd)
{% endhighlight %}
