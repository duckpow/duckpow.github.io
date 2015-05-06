#About this site

So this site might be one of my craziest ideas I have had yet. And that is not in the good sense.

It is not having a blog that is the crazy, nor is it putting my terrible writing skill out in public view.

It is the architecture of the site it self that is crazy!

This is a dynamically created blog without any server-site scripting.

##Hosting on Github

Like most people (I hope) does when creating a new site I looked for tools and inspiration around the web. How had others made a site on Github, what tools had they used, and what does Githubs hosting offer?

First off all Githubs 'hosting' offers only the bare minimum. You can load a static site. And that is fine. I don't need fancy logins, comment threads with voting or leaky databases with sensitive user information.

##So what do I want?

I like Markdown. So I would like to write my posts in Markdown. So I checked what the internet says: "Github hosted + Markdown? Use Jekyll!"

I don't want to much hassle with CSS. Because... ! What does the internet say: "Oh... that is easy. There is loads of themes for Jekyll!"

##WTH is Jekyll?

In the creators own words "Jekyll is a simple, blog-aware, static site generator".

Generator? I'd ask... "Yeah. Just run it every time you want to update your site." Me: "..."

Actually I kind of like the idea of Jekyll and they obviously created a great tool. It just seemed to me at the time that I would relinquished a lot of control and structure of the site. Looking at it now, that may have been a good idea.

#Too late

I have written small blogs before in php and with markdown. Doing the same client-side can't be that difficult... Actually it isn't.

I am not a webdev, nor am I a programmer. But getting JavaScript to fetch markdown files wasn't that difficult. Parsing them to html was 'outsourced'. Christopher Jeffrey has written a great markdown parser called [marked](https://github.com/chjj/marked). And then there was only left to make a working menu... which took some trickery and use of a 'marked' feature.

#It works

It was always the idea to have this blog as small as possible and not cluttered with all kinds of distracting 'features'. And I think it accomplishes that and on the same time is it incredibly simple.

It may not be pretty to look at or working across all platforms but it works.