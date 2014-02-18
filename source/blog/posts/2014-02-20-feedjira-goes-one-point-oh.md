---
title: Feedjira Goes One-Point-Oh
---

Last fall, totally out of the blue, I asked [Paul Dix][p] if I could take over
maintenance of his Gem Feedzirra. It appeared to need some work and there were
things I was interested in doing with it, so I was pretty pumped when he got
right back to me and said yes. He said that he didn't have time to work on it
anymore and so I should feel free to do whatever I thought was best.

[p]: http://www.pauldix.net

Score!

My first order of business was to go through the many open issues and pull
requests on GitHub. When I started there were over 60, a number that I've gotten
down to single-digits. I thought it was important to ensure that users saw me
treat their issue as important and even if it was very old (which many were), I
asked if there was anything I could do to help.

I was pleasantly surprised by the nice way many people responded and we got to
work addressing their questions and issues.

[SemVer][s] talks about how if a project is used in production and its not 1.0,
then its probably past time that you were at that version number. This sounded
like Feedzirra to me! The project was about 5 years old and I knew it was being
used in production, so I treated it as a project at 1.0 and I did my best to
release versions that were backward compatible and added deprecations for what I
wanted to do in 1.0. I saw things that I wanted to completely rewrite, but I
resisted the urge to burn it all down and start again.

[s]: http://semver.org

Next, I wanted to create a website for the project and worked with [Daniel
Ariza][d] to make it look good. I ripped apart the README and rewrote just about
all the instructions, separating them into a few natural topics.

[d]: http://danielariza.com

There was an open issue on the project about renaming the Gem and I knew I
wanted to rename it, but I also knew that Feedzilla (the suggestion from that
issue) was already a thing, so I went with Feedjira instead - you can [read more
about that][more], but its not actually all that interesting.

[more]: link/to/another/post.html

With those things in place, I did a commit to end the Feedzirra Gem and another
that renamed everything and bumped the version to 1.0. Those have both been
pushed to RubyGems and thus Feedjira has gone 1.0!

For most users, upgrading to 1.0 should be a breeze, but I have an [upgrade
page][u] to help with a couple details. If you have any trouble
upgrading, please let me know by [opening an issue][i].

[u]: path/to/upgrade/page.html
[i]: path/to/github/issues.html

There are still lots of things I'd like to do with this Gem. I mentioned seeing
things that I wanted to completely rewrite, so that'll be something that I work
on with a 2.0 release, but that wont be ready anytime soon. I'd like to support
JRuby, which probably means looking at how the fetching happens since Curb is
built on a C extension. Many people use Feedjira with Rails, so a separate
project that helps those users get up and running quickly seems to have value.

The list goes on.

I do have a request before I finish this thing: I'd like to hear from users that
have apps in production using Feedjira. If you're using Feedjira for a
commercial app, please [email me][e]!

[e]: feedjira@gmail.com

Thanks to everyone who has helped me accomplish this, but especially [Paul
Dix][p] for creating such a fun project to work on, [Daniel Ariza][d] for a
badass website design and the many people who opened issues or sent pull
requests. Open source is fun to work on because of people like you!! <3 <3 <3
