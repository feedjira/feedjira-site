---
title: Thoughts on Version Two-Point-Oh
---

TLDR: development of version 2.0 is being done on the [two-point-oh branch][two]
and a [GitHub issue][i] is open for you to give feedback on its direction.

I've starting work on a rewrite for Feedjira and I wanted to try using a [GitHub
issue][i] to discuss what I'd like to see in the new version. I'm very
interested in what users think, so please chime in!!

In no particular order, here are some design goals for the new version:

## Change HTTP Library

This gem depends on [curb][], but I'd like to switch that to something that will
allow me to support JRuby. I did some experimenting and really liked working
with [Faraday][f], so that's what I'm using at the moment.

## Forget Concurrency

Throwing an array of feed urls at Feedjira and watching it concurrently fetch
and parse them extremely quickly is cool in READMEs and demos, but I don't think
it's reality. I think what's much more likely is a single url being passed and
concurrency being dealt with in the application, workers being the likely
approach.

## More Objects

Feedjira has a dirty little secret and it's the `Feedjira::Feed` class. If you
open that sucker up, you'll see 19 class methods and 0 instance methods. These
class methods do everything from fetching and parsing to setting up curb and
unzipping raw xml. Not only is [SRP][s] off in the corner crying, its a mess to
test. I'd like to break this down into smaller objects that get instantiated and
passed around in normal OO fashion.

## Fewer Parsers

One of the things I like best about Feedjira is the ability for a user to define
their own custom parsers and I think its under-used. What I'd like to see is
Feedjira ship with a parser for Atom and a parser for RSS - the others are
really just custom parsers.

## Custom Parser Project

With version 1.2, I was able to spin off the benchmarks into [their own
project][b] and I was very happy with how it turned out - I'd like to see a
similar thing happen with the custom parsers mentioned above. You should be able
to easily grab these parsers and throw them in your application. If you write a
particularly cool custom parser, then you could contribute it back and others
could benefit from it.

## Raise Exceptions Instead of Callbacks

Feedjira almost never raises an exception and instead provides the ability to
register callbacks for success and failure situations, but this has proven
brittle and painful. With the new version, I want to see sensible exceptions
raised when something goes wrong and that pretty much removes the need for
callbacks, so those will be cut.

## Configuration

I want configuration for Feedjira done in a proper config block like most gems.
If you want to change the default parsers, that should be a config option. If
you want to set the user agent, that should be a configuration option.

## Feedback Appreciated

Do you have any other ideas to make Feedjira better? Please check out the
[GitHub issue][i] and share what you're thinking. I'm open to any feedback, so
if I just threw your favorite feature on the chopping block, please tell me!

[two]: https://github.com/feedjira/feedjira/tree/two-point-oh
[i]: https://github.com/feedjira/feedjira/issues/221
[curb]: https://github.com/taf2/curb
[f]: https://github.com/lostisland/faraday
[s]: http://en.wikipedia.org/wiki/Single_responsibility_principle
[b]: https://github.com/feedjira/feedjira-benchmarks
