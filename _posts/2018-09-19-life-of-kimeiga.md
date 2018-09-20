---
layout: post
title:  "Life of Kimeiga - a PWA Blog"
date:   2018-09-20
image: life-of-kimeiga.jpg
---

[View my blog!](https://kimeiga.github.io/blog/)

If you've been paying attention to the frontier of web development, you'll probably have heard of the Progressive Web Application. It's basically a set of guidelines that a web app has to follow in order to provide a near-native like experience, such as offline functionality, fast load times, and ability to add to one's home screen. Google has been pushing PWAs as the future of the web and you can [learn more about it here](https://developers.google.com/web/progressive-web-apps/).

Well I liked the ideas of a PWA, and I also needed a dedicated blog, so I decided that would be my first PWA experiment.

### Started with Jekyll

I first decided that I would use Jekyll to construct my blog. Jekyll is a *static site* generator, which means that it takes markdown/html files and inserts them into HTML layouts with CSS styling (that you provide), to create a set of linked webpages, i.e. a website. In addition, the content of these pages is **static**, meaning that it doesn't change, and so static sites are very easy to maintain on the web because there's no dynamic content or CMS (content management system) to take care of. Obama's election was run on a static site and had practically zero downtime. These things are useful! You can find out more about Jekyll [here](https://jekyllrb.com/).

Well one of the biggest problems of Jekyll is the lack of inspiring themes. A lot of themes are quite similar, and frankly, not well designed. It took a day or so of searching until I happened upon [Hikari](https://kimeiga.github.io/blog/), an interesting Jekyll blog theme. I liked how Hikari's home page was a list of full-width color blocks with the names of the blog posts on it.

As soon as I saw it, I knew it would be a perfect theme to extend with picture support! Instead of the color blocks, we could display the image associated with the blog post there. I'm a huge fan of full-width and full-height images in web design (as you can probably tell by this website! (which was also built in Jekyll from scratch!)).

So I forked the repo and began modifying the theme.

### CSS Problems

>One of the most difficult parts of adding picture support was that I could not access `post.image` from the CSS file that's styling the home page!

I could only access it from the HTML file that was displaying the posts. In hindsight, what I could have done (and what I'm doing on this site), is just write `style="background-image: url(/assets/img/{{ post.image }})"` on the HTML element displaying the blog post card. Inline styles would work. 

But unfortunately I didn't figure this out at the time so I actually made an `<img>` element with a `src={{ post.image }}`, and struggled for a few days to align it perfectly with the back of the post card. I also did this for the image that you see at the top of every post. So that was annoying ahaha.

## Making it a PWA!

So the Hikari theme was responsive from the start, so I didn't need to worry about responsiveness! That means that the functionality I would have to add to make this blog a PWA would be:

- A service worker to cache the blog posts on the phone (so they can be viewed offline)
- A app.manifest to provide information on the app-like qualities of the web app

Ideally I should also optimize it, but there is so little to optimize (and I'm already JPG compressing all the images) that I thought it would be too much hassle for no reason.

Luckily, I found [PWABuilder](https://www.pwabuilder.com/), which promised to build all you need for a PWA in a few clicks. Well, it really does work!

### App Manifest

The automated script parsed my website and gave me a sufficient `app.manifest`. I later added a few things to it that I saw in different websites. This is what it ended up looking like:

```json
{
    "dir": "ltr",
    "lang": "en",
    "name": "Life of Kimeiga",
    "display": "standalone",
    "short_name": "KimeigaLife",
    "theme_color": "#F1C33A",
    "description": "Thoughtful adventures of a bubbly game developer.",
    "orientation": "any",
    "background_color": "#1B1B1B",
    "related_applications": [],
    "prefer_related_applications": false,
    "icons": [
        {
            "src": "/android-chrome-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/android-chrome-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}
```

To be frank, it ended up being called `site.webmanifest`, but it doesn't matter as long as you use the same name in your `<meta>` tag:

```html
<link rel="manifest" href="{{ "/site.webmanifest" | relative_url }}">
```

### Service Worker

Then it was on to the service worker! This is basically two pieces of JavaScript that cache your website's styling and content on the device so that pages load faster and load offline!

I chose the "Offline copy of pages" option, which basically stores every page that the user visits in the cache. It's simple to set up, and worked well!

Then I went through the hassle of finding a the right favicon generator. I eventually ended up combining the outputs of [Favicomatic](http://www.favicomatic.com/) and [Real Favicon Generator](https://realfavicongenerator.net/). It looks really messy, especially in the `<head>` of my `index.html` where there are tons of `<link>`s to different favicon sizes, but I suppose this is what you have to do these days.

## Conclusion

At the end of it all, I got a high Lighthouse (Google's PWA and web standards audit) score, and deployed my site to Github Pages! When I visited the blog, I was prompted to "Add to Homescreen", and after adding to home screen, my blog acted like an app, loading pages offline too!

Finally! [You can view my blog for yourself here!](https://kimeiga.github.io/blog/)

