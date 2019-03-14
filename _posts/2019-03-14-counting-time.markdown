---
layout: post
title:  "Counting time oneliner"
date:   2019-03-14 16:30:36 +0100
categories: oneliner ruby gist
---
I find it difficult to count time easily. I mean, to count periods of time.
If I have several tasks and their duration, I want to know the total amount of time.

This time, I wanted to know the total remaining time of a [udemy](https://www.udemy.com) course.

I have created this simple oneliner that will take standard input, extract times and sum them.

{% highlight ruby %}
grep -o "[0-9]\+:[0-9]\+" | xargs | tr ' ' , | \
ruby -ne 's = $_.split(",").map{|e| t = e.split(":").map(&:to_i); t[0]*60+t[1]}.sum; puts "#{s/60}min. #{s%60}s."'
{% endhighlight %}

In th case of udemy, you can select from the content videos, run this oneliner and paste the contents.

Probably there's a utility to do something like this but I haven't find it.
