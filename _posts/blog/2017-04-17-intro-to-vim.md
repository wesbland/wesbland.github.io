---
layout: post
title: "Introduction to Vim"
modified:
categories: blog
excerpt: "You don't have to use Vim, but you're in the wrong place if you do."
tags: [tools,vim]
---

Everyone has their favorite editor. For some, it's Emacs. For others, it's Vim.
Still others don't know how to use a computer. I'm kidding. I'm actually writing
this post in [Atom](https://atom.io) (though with Vim keybindings). What editor
you use depends on a bunch of things, but if you want to pick one of the biggest
two, it comes down to Emacs and Vim. Someday I'll try to get someone to write a
post or two about Emacs, but in my world, it's all about Vim. Well...actually
[Neovim](http://neovim.io), but I'll come back to that later.

In this post, I'll try to cover some of the basics of Vim to get you started and
circle back to some of the more advanced features in a later post. Let's start
with the thing that is probably the most searched for feature of Vim.

## [Jane! Stop this crazy thing!](https://www.youtube.com/watch?v=gTZ91YtKLN4)

```
Esc
:q<enter>
```

The first thing you notice about Vim is that you can't just hit the escape key
(or Ctrl+C) to quit. You very quickly become familiar with the fact that Vim
lives in modes. When you start it up, you're probably in "normal mode". This
means that you're in the mode where you can give commands to Vim (as opposed to
the one where you input text to the buffer). Most people think that they need to
get into "insert mode" as quickly as possible so they can start typing text. In
reality, I'm probably 50/50 on time spent in the two modes. As soon as I finish
typing the thing I'm thinking, I drop back down out of insert mode into normal
mode. You can generally assume that every command and key that I'm telling you
for the rest of this post applies only to normal mode and won't do anything in
insert mode.

So lets start with some basic navigation. There's the very basic keys to move
from character to character:

```
h - Left
j - Up
k - Down
l - Right
```

Chances are that you probably knew that part though. Those are the basics that
everyone learns. One thing to keep in mind is that you shouldn't fall back to
the old trap of using those obnoxious keys on the bottom right of your keyboard.
The arrow keys were made for gaming, not typing. Using them just slows you down
massively as you have to move your right hand all the way from the home row to
the arrow keys and back. Stick with `hjkl` and you'll be on your way to
lightning Vim speed.

One thing to keep in mind when flying around your buffers is that all of the
movement keys only work when you're in normal mode. If you're in insert mode,
there's nothing you can do to move around without moving to those pesky arrow
keys. That's why it's so important that you train yourself to move down from
insert mode to normal mode. `Esc` to go to normal mode. `i` to go back to insert
mode (though you'll find later why I so rarely use the `i` key).

## Time to move faster

Now that you can crawl from character to character, it's time to move a little
faster. What if you want to move forward a whole word at a time instead of just
a character? This is a pretty important one. The `w` key is your friend here.
This is one of those rare times where the shortcut key might actually help you
remember what it does. `w` for word. You can also you `e` to go to the end of
the word. See what I did there? `e` for end? Yeah, you saw it. You're smart. The
word `b`efore the current word? You'll figure it out. Something else to remember
is that "word" has a tricky definition, especially when you're talking about
code. Vim's word delimiters change depending on the type of file you're editing
so you'll have to experiment a bit, but in general it's any whitespace or
punctuation mark. Underscores generally don't count since they usually fall in
the middle of variable names.

So now we can move one word at a time. What if we want to move a bunch of words?
This is where Vim starts to make sense. Just about every command there is in Vim
can be repeated by typing in a number first. For instance, want to move 5
characters down? That's a `5k`. Move back 3 words? `3b`.

Now lets try moving up and down by paragraph. That'd be the `{` and `}` symbols.
They'll move you to the previous and next empty line, respectively. These are
great. I use them a lot to fly around the code.

You can also page up and down. `Ctrl+u` (up) goes up a half page. `Ctrl+d`
(down) goes down. `Ctrl+b` (back) is up a whole page, and `Ctrl+f` (forward)
goes down a whole page.

What do you do if you've been moving around so much that your cursor is stuck
way at the bottom of the screen and you want to re-center? `zz` (zoom zoom?)
will do the trick there. It centers the screen based on your current cursor
location. You can also put the current cursor at the top `zt` (zoom top) or
bottom `zb` (zoom bottom).

Sometimes you just want to go to the top of the buffer and `gg` will take you
there. `G` will also drop you to the end of the file.

## Ok, now I want to actually type something

You've spent all this time figuring out where you want your cursor to be. It's
probably time to actually write some code. Push `i` (insert) and you're now in
insert mode just before the highlighted character. Did you actually want to
append? `a`. What if you want to put something at the beginning of the line, `I`
(super insert), or at the end, `A` (super append). How about you're wanting to
create a new line before the current line? `o` (I got nothing). `O` (nope) will
insert a new line after the current line.

It may seem silly to have so many ways of going from normal mode to insert mode,
but if you can get to the point where you know all of these shortcut keys by
heart, you can really speed things up when you're both navigating and typing.

## Oops, I made a mistake. I guess I'll hit the old backspace

You could do that, but I think you've learned by now that if it works in
Microsoft Word, it's probably not the best way to do things in Vim. Of course,
the backspace key will work if you're in insert mode, but if you're following my
lead, you're probably in normal mode by this point. The `x` key is the starting
point for character destruction. It will delete the character currently
highlighted. But of course, you probably want to delete more than that. You
might was to delete a word. This is where learning all those navigation keys
above will start to pay off. Let's see if you can guess what these things do.

```
dw
d}
dG
dj
```

If you guess delete the next word, delete everything until the next whitespace,
delete everything until the end of the file, and delete this line and the next
line, then you're probably cheating and didn't need to be reading this tutorial
anyway. Move along.

There's a few more that you should know. `dd` will delete the entire current
line. `D` will delete the rest of the line. `4x` will delete 4 characters.

## That's cool. I can dele...wait...what just happened when I bumped the `p` button?!?

Ah, so you're learning to paste. That's good. But when did you cut? Well, in
Vim, every time you delete text, you're actually cutting it. So if you delete a
character with `x`, you can push `p` later and past it after the currently
highlighted character. `P` will put it before. This works with anything that you
delete. A word, line, paragraph, entire file? No problem. Just `p` it in place.

## All that's good, but I don't even know where to find my code

If you're trying to find some code somewhere in that big file and just can't
scroll around to where you need to be, it's time to learn to search for things.

I'm not going to spend a bunch of time teaching regular expressions here. In
general, I hate them and I'm not particularly good at learning them. That being
said, it's definitely worth learning them at some point. For now though, let's
just do the basics. You know that you want to find `foo` in your program
somewhere. For that, you need to go into search mode. I know that I said there
were only two modes, but I lied. Anyway, it's not like you spend much time in
search mode so it doesn't really count, right?

So push `/` and start typing what you're looking for. Most likely, it'll start
jumping around to find the next occurence of the text you were searching for.
When you hit `Enter`, you'll be moved back into normal mode. What if you want to
find the next occurence? `n` will take care of that and `N` will find the
previous one.

There's some pretty powerful shortcut keys here too. If you just want to find
the next occurence of the current word, `*` is your friend. `#` will find the
previous occurence of the current word. I use these a lot, particularly with
variables that I want to see where they're used.

## Whew...that's a lot. Let's take a break.

Yeah, you're probably right. There's definitely lots more, but let's `:q` for
now. Just go ahead and save your work. What? I didn't show you how to save
yet...fine. Last thing...

The word to keep in mind here is "write". You write the current buffer to disk
with `:w`. By pushing `:`, you're actually putting Vim into another special mode
that allows you to type out commands that are longer than a chacter. This
doesn't get used a lot, but for opening and closing buffers, it's pretty common.
`wq` will save and quit. If you want to quit without saving, you can tell Vim
that you mean it in the most traditional way, with a big old `!`. `q!` means NO!
I didn't want to save that buffer. I just want it gone.

## Ok, so we're done now...right?

Sure, we're done now. Next time we'll start looking at some more advanced
features. Not sure what they'll be yet, but I'm guessing configuratino and
plugins. That's where your text editor really becomes your own.

See you then...
