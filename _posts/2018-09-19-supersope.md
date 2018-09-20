---
layout: post
title:  "Süperşöpe - a Stylish Preact music player"
date:   2018-09-20
image: supersope.jpg
---

[Check out the music player](https://supersope.now.sh), and [the code](https://github.com/kimeiga/supersope)! 

# One night I was bored

I had been learning the differences between lots of JavaScript frameworks at the time. React, Angular, and Vue I knew, but I was learning about Hyperapp, Svelte, Surplus, AppRun, Dojo, Keechma, etc. There's a lot of them out there. I remembered my appreciation for [Preact, a 3kb version of React by Jason Miller](https://preactjs.com/), and decided that it was high time that I make another thing with it.

## I want to make *something* now

So I thought about how I have **amazing** music taste that I would like to share with my friends, and I was also itching to try an unusual layout for a website, so I pulled out my web design notebook and sketched something out. I came up with a two-panel design, in which one panel was a song list, and the other would be the song currently playing.

### An idea

I listen to a lot of (good) music on Soundcloud. Especially funk. And I was interested in using the Soundcloud API.

## Do it with Preact!

So first I used the amazing [Preact-cli](https://github.com/developit/preact-cli) (Command Line Interface), to create a new Preact project (that was completely PWA enabled, thanks Jason!). I created a song-list screen, and used the Preact Router to create numerous Song pages. I then hooked them all into a CSS Grid layout that switched from side-by-side to top-and-bottom layout for mobile for responsiveness.

### SoundCloud API?

Well SoundCloud does have a [publicly facing API](https://developers.soundcloud.com/docs/api/guide), but you need a API key in order to play songs with it. I clicked their link to get one, and it said that they weren't accepting people for a while (perhaps indefinitely).

#### In need of a hack

I'm not one to wait. I tried using the SoundCloud player that you get when you click "Embed". It looks like this:

```html
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/125725588&color=%23ff00c8&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
```

I saw the `width` and `height` parameters in the iframe and played around with them. Apparently when you have the height set to about 20 pixels, the player converts into a minimal look with a play button and a waveform indicating progress though the song.

##### Forgot about CORS

I thought maybe I could have the user press a button on the website and it would send a click to the play button of the iframe, and I would just hide the iframe, or just set the opacity to 0. However, when I tried this, it violated the Cross-Origin Policy (duh hakan), and I knew I couldn't do that.

#### A clever solution!

So what I came up with I still think is kinda clever. I basically *ZOOMED IN* on the play button of the iframe, so it was nice and big, and placed it on a black circle background. I did that with the following CSS styles:

```css
#frame {
	-ms-zoom: 4;
	-moz-transform: scale(4);
	-moz-transform-origin: 0 0;
	-o-transform: scale(4);
	-o-transform-origin: 0 0;
	-webkit-transform: scale(4);
	-webkit-transform-origin: 0 0;

	position: relative;
	left: -30px;
	top: -30px;
}
```

This solves two problems! The first problem is that it gets around the SoundCloud API and plays music. However, I could have (and initially tried) to use a Soundcloud player with `autoplay` turned on, and then just hide it. But mobile phone browsers don't allow autoplay (to decrease data consumption).

BUT, this is **also** solved by the play button because it renders correctly (and prominently) on mobile and the user can just tap it like a normal Soundcloud play button for the music to start.

## Perfect

It was perfect, it played my funky music, [it had a cool picture of NYC that I stylized from Unsplash](https://unsplash.com/photos/M0tL38xahu0), and it was a PWA without me having to do anything.

All in about 4-5 hours of work. Preact is fantastic.

### Süperşöpe?

Also if you're wondering about the name:

Süper means super in Turkish. Şöpe means... I don't know. It's a word I came up with to mean "dope" or "cool". It sounds fun to say. Şöööpeeeeeeee! So the title means "supercool" I suppose.

### Check it

[Check out the music player](https://supersope.now.sh), and [the code](https://github.com/kimeiga/supersope)! 

I will be adding more songs to it once I figure out how to avoid making new `index.js` files for each song I want to add, and just interpolate data in a database (maybe [unistore](https://github.com/developit/unistore)) to create the routes automatically.
