---
layout: post
title: "Introduction to Git"
modified:
categories: blog
excerpt: "You have to put your code somewhere. This is the best place to do it."
tags: [tools,git]
---

Let's get one thing straight before I start this thing. Git is not the same
thing as GitHub. Git is a program that runs on your computer that creates a
repository where files can be safely stored and versioned. GitHub is a company
that runs a service online where you can place copies of your Git repositories
so if your computer falls in a lake, your files will still be safe. Don't get me
wrong. I love GitHub. Here's a picture of my laptop.

![My Octocat Laptop](/images/laptop_back.jpg)

I plan to write a post about GitHub at some point in the future, but this isn't
it. This is about Git itself.

I'm going to start by saying that if you're looking for a really good tutorial
about how to get started with Git, I'd recommend
[this](https://try.github.io/levels/1/challenges/1) one from GitHub. It doesn't
get into any details or the philosophy of Git, which is what I hope to touch
more on here, but it does a great job of being a hands-on tutorial to get you
started with some basic Git usage.

## Why is this so hard?!?

You've probably heard of Git before. You may have even tried it out. Shortly
after doing so, you probably said...

> "Arg! Why would anyone use this?!? It's so complicated and stupid!"

This is normal. Especially if you've come from one of the more traditional
version control systems where things were pretty straightforward. There was
none of this *distributed* nonsense and when you wanted to commit stuff, you
just said `commit`.

Git is different. If you're coming from previous version control systems, you
are probably familiar with the idea that there is a golden master repository
somewhere that has the magical canonical version of your code. This made things
nice and simple. When you wanted to get the most recent version of the code, you
went to that repository. If you wanted to see the side development that was
going on, it was probably also in that repository.

The downside was that if you ever wanted to try something out without sharing it
with the world...too bad.  Either you put it in a branch on that repository for
all to see, or you didn't put it version control at all and hoped that nothing
happened to your laptop for as long as it took you to finish that feature. You
also couldn't go back and fix any if your previous work if you discovered a bug
in a commit in your side branch and wanted to clean it up before you merged the
branch in with the main branch. Also, if you were somewhere without an Internet
connection...too bad. No checkins for you.

Also, if you've talked to someone who knew Git well to ask for help, they
probably said something like this:

> It's really easy once you think of it as a directed acyclic graph!

I'm going to leave that one for next time, but the short version is, yes, that's true...for a small number of people.

![XKCD 1597](/images/git_2x.png){: .center-image height="50%" width="50%"}
*Source: [https://xkcd.com/1597](https://xkcd.com/1597)*{: .center}

I could go on all day about all of the things that you couldn't do, but you came
here to find out about what you *can* do with Git. So let's move on to that.

## Set up your `.gitconfig`

Before we start, let's make sure we're all on the same page configuration-wise.
The very first thing you should do after you install Git on your machine is set
up the basics of your `.gitconfig` file in your home directory. Your's doesn't
have to be as
[long](https://github.com/wesbland/environment/blob/master/gitconfig) as mine,
but there are some critical things that you should have.

```
[user]
    name = <Your name here>
    email = <Your email here>
```

The first thing you need is to set up your name and email. It seems silly, but a
lot of people leave this part out. Git doesn't have usernames the way other
version controls systems do. For instance, in Subversion, you would set up your
username for a particular repository and the server would figure out your name
and email on the other end. With Git, you take care of all of that on your end.
Keep in mind that this `.gitconfig` file in your home directory is just the
default for all of your local repositories. You can always customize this if you
have some repositories where you want to go by one name (Wesley Bland), and
others where you want to use another (Stormcloak Dragonslayer). The important
thing is that you don't leave this blank, because then you're just whatever your
username is and your email is (`username@hostname`), which is gross and
unhelpful.

There's lots of other configuration you can put in there. There's one thing that
I recommend strongly and will assume that you're using here:

```
[alias]
    graph = log --graph --decorate --abbrev-commit --pretty=oneline
```

I always see people using `git log` as their main way of looking at history in
their repository. This is gross. It's the difference between this:

```
commit eb68396c3d5054f2f5b4a2f920dd7500b370df22
Merge: f1848ff00780 9c4170c8ffdf
Author: xxxxxx
Date:   Thu Jun 1 13:09:33 2017 -0700

    Merge pull request #3016 from jdinan/pr/man2pdf

    Add script to convert libfabric manpages into a PDF

commit f1848ff007807bfc723bf7b694b7df8f3b95dd1c
Merge: 58b96d73eb65 5b00c0407503
Author: xxxxxx
Date:   Wed May 31 14:01:17 2017 -0700

    Merge pull request #3021 from qwert182/win-fix-dgram

    win/build: fix recvmsg

commit 5b00c040750354148828b2a314e15216b2ae1bf8
Author: xxxxxx
Date:   Wed May 31 19:44:41 2017 +0300

    win/build: fix recvmsg

    - actual length of message is the result of recvfrom(), not len
    - copy result from buffer[offset] instead of buffer[len]

    Note: recvmsg was not used till commit c0548ae8014907d4a5be13678bc5e6ebf3115410

    Signed-off-by: xxxxxx
```

And this:

```
*   eb68396c3d50 (HEAD -> master, origin/master, origin/HEAD) Merge pull request #3016 from jdinan/pr/man2pdf
|\
| * 9c4170c8ffdf Automatically generate man2pdf manpages list
| * e9f4f26ece50 Add script to convert libfabric manpages into a PDF
* |   f1848ff00780 Merge pull request #3021 from qwert182/win-fix-dgram
|\ \
| * | 5b00c0407503 win/build: fix recvmsg
|/ /
* | 58b96d73eb65 Updated nroff-generated man pages
* |   de82f986952d Merge pull request #3020 from shefty/fixes
|\ \
| * | 7d6c53c38dda fabric: Update triggered op definitions in response to FI_CONTEXT2
* | |   6b2a3c204174 Merge pull request #3002 from thananon/pr/usnic_auth_key
|\ \ \
| * | | 9860cbdaddb1 prov/usnic: handle authorization key
* | | |   45465f4f2116 Merge pull request #2992 from thananon/pr/usnic_mode_v2
|\ \ \ \
| |_|_|/
|/| | |
| * | | fd83751f92af prov/usnic: correctly accommodate new mr_mode flag.
* | | |   ff14da944c66 Merge pull request #3014 from pkcoff/BGQ-Provider-copy-immediate-data-for-FI_PEEK
|\ \ \ \
| * | | | 4cc4b6411504 prov/bgq: Copy immediate_data into context on match for FI_PEEK
* | | | |   a63760b3d4e6 Merge pull request #3013 from j-xiong/master
|\ \ \ \ \
| * | | | | c7879a2044bb prov/psm2: Handle FI_DISCARD in tagged receive functions
* | | | | |   74493175723a Merge pull request #3011 from hppritcha/upstream_merge_pr1349
```

I know that second one can look a little intimidating, but I hope you'll see as
we go along how much more useful it actually is (also how much more information
you can see at once).

## What does distributed mean?

One of the taglines of Git is that it's "distributed". It's usually described as
a *distributed* version control system. This is something that confuses people,
especially if they came from the world of Subversion or something like it, that
has a single version of the repository that is the "main" version where everyone
else checks out their code. People hear about the distributed model and think
that it's the wild west and that it's impossible to find the "real" version of
the code anywhere.

I want to make some things pretty clear here. Yes, that model is possible. You
*can* have a million different versions of your repository that are all the
*right* version. In practice, that would be anarchy and stupid. The way that
every project usually works is that they decide on where the "main" version of
the repository will be (often at a cloud-based service like
[github.com](github.com), but not necessarily) and treat that as the blessed
version.

That's not to say that the idea of being distributed has no merit though. In
fact, it's incredibly useful. For instance, I started this post on an airplane.
With a single-server model, that would mean that I couldn't check the status of
my repository, make any commits, or really anything else but the most basic
repository operations. However, because I'm using Git, I actually have a
completely re-creatable copy of the repository on my laptop and can do anything
with the repository that I'd normally do. Later, when I get back to an Internet
connection, I can push my changes back to the main repository and everything is
in sync again.

## Wrap it up

I started out writing my Git tutorial as one huge post, but it ~~quickly~~
slowly became clear that it was going to be much bigger than anyone had interest
in waiting around for. So I've now broken this post up into more digestible
chunks. This time I covered some of the overall philosophy of Git and helped you
set up your environment. Next time I want to show you how to do some of the
basics of using a repository (cloning, pushing, fetching other's changes, etc.).
Later, we'll get into some of the more complex workflows that come from having a
repository on GitHub or contributing to others' repositories.