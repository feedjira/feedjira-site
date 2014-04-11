---
title: A Separate Project For Benchmarks
---

With the release of version 1.2.0, the benchmarks for Feedjira have been moved
to a separate project: [https://github.com/feedjira/feedjira-benchmarks][p].

[p]: https://github.com/feedjira/feedjira-benchmarks

What's nice about this is that it keeps things much more organized and allowed
me to add a pretty neat new benchmark - more on that in a moment. I also rewrote
the [Benchmarks page][b] on this site so please check that out.

[b]: /benchmarks.html

One benchmark that I didn't pull over to the new project is the fetching one. I
left it out because it relied on the consistency of your network connection and
that didn't feel like it was scientific enough.

In its place I've added a benchmark for parsing speed that's run against each
version of the gem. Its pretty cool - when you clone down the
feedjira-benchmarks project, you also clone down feedjira itself and then the
script moves to each version tag in the git repo, runs the benchmark and records
the results. It was pretty fun to write and works like a charm.

For the charts, I ended up learning some [R][r] so that I could have a little
more control.

[r]: http://www.r-project.org/

Benchmarks are really only valuable if they can be reproduced by others, so I've
written up instructions in the README for setting things up and running them. If
you're interested, take a look and try running them yourself!

I'll continue to use the benchmarks to ensure Feedjira stays fast, so you wont
have to worry about your favorite Ruby feed library slowing down. If you have
any feedback for me on the benchmarks, feel free to hit me up on Twitter
([@feedjira][t]) or [open an issue][i] on the project's repo.

[t]: https://twitter.com/feedjira
[i]: https://github.com/feedjira/feedjira-benchmarks/issues
