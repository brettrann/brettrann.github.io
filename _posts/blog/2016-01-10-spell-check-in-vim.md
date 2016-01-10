---
layout: post
title: Spell Check in Vim
modified:
categories: blog
excerpt: How to configure Vim for smarter spell checking.
tags: [vim,development]
image:
  feature:
date: 2016-01-10T17:20:37+11:00
---
### Using Vim Spell Checking

A quick post on Vim's built in spell-checking, including a small recommended <a href="#vimrc">.vimrc</a>.

Vim has built-in spell checking which is simple enough to turn on:

{% highlight vim %}
:set spell
{% endhighlight %}

But probably you want it only on for your local buffer:

{% highlight vim %}
:setlocal  spell
{% endhighlight %}

You can specify the region which chooses the spell check file for you:

{% highlight vim %}
:setlocal  spell spelllang=en_us
{% endhighlight %}

And to turn it off:
{% highlight vim %}
:set nospell
{% endhighlight %}

You can turn it on automatically for specific extension:
{% highlight vim %}
:autocmd BufRead,BufNewFile *md,*txt :setlocal spell spelllang=en_us
{% endhighlight %}

Or through Vim's FileType:

{% highlight vim %}
:autocmd FileType gitcommit,markdown,text :SpellOn
{% endhighlight %}

You can bind it to an F key:

{% highlight vim %}
:map <F5> :setlocal spell spelllang=en_us
{% endhighlight %}

You can add a word to a local dictionary using 'zg when over a highlighted word:

{% highlight vim %}
Word 'Jekyll' added to ~/.vim/spell/en.utf-8.add
{% endhighlight %}

And undo that using 'zug'

And you can get suggestions using 'z=' when over a highlighted word.

Finally, you can get suggestions as completions inline when using CTRL-N or CTRL-P:

{% highlight vim %}
:set complete+=kspell
{% endhighlight %}

<a name="vimrc"></a>
And if you want to do all of those things, you can create a command alias and then reference that command in AllTheThings, and put it into your .vimrc (since this is for the .vimrc, this time with no prefixing ':' for each line):

{% highlight vim %}
" spell checking automation
command SpellOn setlocal spell spelllang=en_us
map <F5> :SpellOn<CR>
autocmd BufRead,BufNewFile *.md,*.txt :SpellOn
autocmd FileType gitcommit,markdown,text :SpellOn
set complete+=kspell
{% endhighlight %}

For more info ':help spell' inside vim!
