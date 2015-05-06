#About this site

So this site might be one of my craziest ideas I have had yet. And that is not in the good sense.

It is not having a blog that is the crazy, nor is it putting my terrible writing skill out in public view.

It is the architecture of the site it self that is crazy!

This is a dynamically created blog without any server-site scripting.

##Hosting on Github

Like most people (I hope) does when creating a new site I looked for tools and inspiration around the web. How had others made a site on Github, what tools had they used, and what does Githubs hosting offer?

First off all Githubs 'hosting' offers only the bare minimum. You can load a static site. No php, no .net, no RubyOnRails, no server-site scripting at all. And that is fine by me. I don't need fancy logins, comment threads with voting or leaky databases with sensitive user information.

##So what do I need and what do I want?

I like Markdown. So I would like to write my posts in Markdown. It is easy to use and I don't need to type in a thousand tags. So I checked what the internet says: "Github hosted + Markdown? Use Jekyll!"

I don't want too much hassle with CSS. Because... ! So what does the internet say about how to avoid that: "Oh... that is easy. There is loads of themes for Jekyll!"

##WTH is Jekyll?

In the creators own words "Jekyll is a simple, blog-aware, static site generator". Generator? I'd ask... "Yeah. Just run it every time you want to update your site." Me: "So I need to install it? I already have my computer full of all kind of programs I don't use"

Actually I kind of like the idea of Jekyll and they obviously created a great tool able to help a lot of busy people setting up a quick site. It just seemed to me at the time that I would relinquished a lot of control and structure of the site. Looking at it now it may have been a good idea to lose that control. But would I have learned anything from that?

##Too late

I have written small blogs before in php and with markdown. Doing the same client-side can't be that difficult. Can it? ...Actually it isn't that difficult.

I am not a webdev, nor am I a programmer. But getting JavaScript to fetch markdown files wasn't that difficult. Parsing them to html was 'outsourced'. Christopher Jeffrey has written a great markdown parser called [marked](https://github.com/chjj/marked). And then there was only left to make a working menu... which took some trickery and use of a 'marked' feature.

The only 'downsides' for me is the warnings that XMLHttpRequest is harmful for the user experience (wth?), but I have found no alternatives, and that I couldn't load every file in a folder and thus need to type in the names of the files to load. The last part has something to do with security I believe.

Github may also find a slight downside in the fact that every user that tries access my site, results in '1 + numberOfPosts' http requests for them...

##It works

It was always the idea to have this blog as small as possible and not cluttered with all kinds of distracting 'features'. And I think it accomplishes that and on the same time is it incredibly simple.

It may not be pretty to look at or working across all platforms but it works. For me. And I learned a thing or two.