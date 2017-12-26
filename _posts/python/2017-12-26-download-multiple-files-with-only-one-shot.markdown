---
layout: post
title: "Download multiple files with only one shot"
date: "2017-12-26 11:44:37 -0800"
location: "San Diego, CA"
commentIssueId: 32
category: Python
tags: [python]
---

<h3>A few days ago,</h3>

I was trying to download TOEIC test listening files from [barronsbooks.com](http://barronsbooks.com/tp/toeic/audio/), Essential Words for the TOEIC, 6th Edition.
Because I already have mp3 CD but you know, recent laptops almost don't have CD-ROM.

Anyway, we got the link so ready to download my listening files. But...

![](/images/download_multiple_files_with_only_one_shot.PNG)

No zip files? and download 55 files 'MANUALLY'?? That doesn't make sense. It's like ancient way to download my files...

But we got python(we can do with other languages absolutely) and we know how to solve these life-hacking problems :)

Let's code

After some trials with download links, every files has same format, "http://barronsbooks.com/tp/toeic/audio/ks97xr/Track%20[number].mp3".

But number starts from 01 to 55. So use iteration and use zfill to padding with zero.

{% highlight python %}
file_number = str(i).zfill(2)
{% endhighlight %}

And use requests module to send http request to url and write the content from request object.

{% highlight python %}
import requests

for i in range(1, 56):
  file_number = str(i).zfill(2)
  url = "http://barronsbooks.com/tp/toeic/audio/ks97xr/Track%20{}.mp3"\
                .format(file_number)
  r = requests.get(url, allow_redirects=True)
  f = open("{}.mp3".format(file_number), "wb")
  f.write(r.content)
  f.close()
{% endhighlight %}

Just run it and get all 55 mp3 files at a time!

Now we only need more time to study. python saved our boring, time-wasting download time :)
