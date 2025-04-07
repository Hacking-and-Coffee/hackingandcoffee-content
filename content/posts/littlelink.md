---
title: "RIP LinkTree worker; Long Live LittleLink Worker!"
date: 2025-04-07
draft: false
author_image: 'images/about.jpg'
author: 'hon1nbo'
---

### LinkTree
was handy, and I made some graphics that actually fit. But I *really* wanted to use my domains. I did a workaround in which I setup a reverse proxy with Cloudflare workers. This worked, but broke a *lot.* You see, LinkTree sets up Cross-Origin Resource Sharing (CORS) policies. For sensitive services this would have been a good thing. For account management, a good thing. For an always-public link sharing site? Just silly.

Well, I did something even sillier. So to reverse proxy this service we had to handle the static content as well as dynamically loaded assets. Of course, them putting it all on a single domain would have been too easy. So I did some fancy rewriting scripts. But these broke a lot as they updates their services under the hood. So recently, with more breakages causing the images to fail to load, I decided to toss the tree out to the curb.

### LittleLink
F/OSS replacement for LinkTree, and runs on Cloudflare pages without even having to run a build? Entirely static assets? Updated CSS with modern services? Yeah, I should have done this waaaayyyyy back.

So thanks LittleLink for making my life easier.

You can see how I run [https://hon1nbo.com](https://hon1nbo.com) using [littlelink](https://github.com/sethcottle/LittleLink) in [My Repo](https://github.com/hon1nbo/littlelink)).

Cheers,

~H
