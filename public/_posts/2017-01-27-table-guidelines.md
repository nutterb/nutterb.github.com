---
layout: post
title: "Initial Thoughts on Table Guidelines"
date: 2017-01-27
comments: true
---

During my (mis)adventures of writing `pixiedust`, I've sometimes found
myself considering ideas that I eventually decided were bad ideas. The
first such idea occurred very early on as I was trying to map out all of
the features I thought were necessary for a complete package. As I
considered the possibility of complex coloring schemes, I thought it
could be useful to generate legends to accompany tables.
<!--excerpt-->
Table legends weren't an idea I pursused for long because I knew it was
probably a little beyond my coding capabilities. As I've learned more,
however, I've decided that it's a terrible idea to begin with. Tables,
by their nature, ought to reduce their message to as simplistic a
presentation as possible. I eventually decided that if a table becomes
so complex that it requires a legend, then it probably ought to be a
graph.

As I've continued with additional development, I've tried to think
carefully about whether or not the idea I'm approaching ought to ever be
used. The use of color is another feature in tables that I think can be
dangerously overused. And so, my initial thoughts on some guiding
principles for producing effective tables.

1.  Avoid trying to use tables the way you would a graph.
2.  If your table requires a legend, it’s too complicated. Use a
    graph instead.
3.  Background colors should only be used for row or group
    discrimination (with very rare exceptions).
4.  Subtlety is a virtue.
5.  When using color (backgrounds, fonts, or borders), try to limit
    yourself to two colors.

I've also published these in [*Get Your Sparkle
On*](http://nutterb.github.io/pixiedust/using-tables-effectively.html#guiding-principles),
my extended guide to the `pixiedust` package. (still under development,
and these principles may change as I my ideas mature).
