---
layout: post
title:  Why I Switched to TiddlyWiki for Note-taking
---

# Why I Switched to TiddlyWiki for Note-taking
I need to take lots of notes during my day, mostly related to my day job, research, and hobbies, and to a lesser degree for managing my daily life. Because most of  notes are work-related, I cannot use any system that is hosted by a third party. I also don't want to use multiple systems to do this. 

For a while now, I've been using TiddlyWiki, and it is FANTASTIC. I came across it while researching self-hosted alternatives to RoamResearch, which my Twitter feed tells me is gaining lots of momentum. Many of the things that seem to attract people to RoamResearch seem to have already been in TiddlyWiki for a while, see "[Philosophy of Tiddlers](https://tiddlywiki.com/#Philosophy%20of%20Tiddlers)", and [TiddlyWiki was started back in 2004](https://en.wikipedia.org/wiki/TiddlyWiki). A note in TiddlyWiki terminology is called a *[tiddler](https://tiddlywiki.com/#Tiddlers)*.

## What got me to move to TiddlyWiki?

Here is a non-exhaustive list with the highlights for *me*:

* **Ease of getting started**: TiddlyWiki can be used as a single-page application driven by an HTML file that you can have locally on your machine. With some JavaScript magic, TiddlyWiki is an example of a [quine](https://tiddlywiki.com/#Quine): a program that produces a copy of its own source code as its only output. The nice thing here is that if you add or edit a tiddler when running TiddlyWiki as a single-page HTML and save the resulting file, you'll get a copy of your wiki with the changes. If you happen to use Firefox, then you can the [TiddlyFox](https://tiddlywiki.com/static/Saving%2520with%2520TiddlyFox.html) plugin so that you're always modifying the same file. There are other ways to use TiddlyWiki (I use it as  Node.js package), but the ease of trying it out means you can see if it fits your needs before you worry about the details of setting it up.

* **Web-based**: I spend so much time in the browser, so I prefer to take notes there. 

* **Math typesetting support with KaTeX**: I need to take notes with a fair bit of math. There is an official [KaTeX plugin](https://tiddlywiki.com/static/KaTeX%2520Plugin.html) that can be easily installed and just works. 

* **Search**: I need to take lots of small quick notes, and retrieve them quickly. I don't want to spend any energy to organise these notes, and I don't think any amount of energy will suffice. Because of this, I need search-based retrieval on notes, and TiddlyWiki has that!

* **Interface allows having multiple notes open at once**: I often need to write a note while referring to other notes. TiddlyWiki allows you to have multiple notes ("tiddlers") open at once. You choose which ones to open, so it's not just a feed of the last few notes you've written.  This means I can jump quickly between multiple notes, including the one I'm writing, usually using `CTRL+F`. 

* **Interface allows live-preview while editing notes**: Tiddlers are written in a special markup language. As you're editing a note, you can have a preview pane that shows you the output. For me, the value of the preview pane is in the ability to edit one part of a note while referring to another part. If you read the [Philosophy of Tiddlers](https://tiddlywiki.com/#Philosophy%20of%20Tiddlers), you'll see that Tiddlers are not meant to be long, but I tend to not stick very closely to this part of the philosophy.

* **Easy linking and backlinks**: It's easy to create [links between tiddlers](https://tiddlywiki.com/#TiddlerLinks), and a tiddler is aware of other tiddlers that link to it. Similar to search, this also saves you the need to organize tiddlers, you can just establish ad-hoc links between tidddlers as needed and [inspect](https://tiddlywiki.com/#InfoPanel) connections between tiddlers as necessary.


I would recommend listing to an [interview](https://changelog.com/podcast/196) with [Jeremy Ruston](https://jermolene.com/), the author of TiddlyWiki, [on the Changlog podcast](https://changelog.com/podcast/196). Jeremy touches on things like the ability to open multiple Tiddlers at once. There is so much more to TiddlyWiki, enjoy exploring and hopefully I'll get to write about some of these at some point.
