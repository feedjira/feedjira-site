---
title: Feedjira Goes One-Point-Oh
---

Last fall, I asked [Paul Dix][p] if I could take over maintenance of his gem
Feedzirra. My request was totally out of the blue, so I was pretty pumped when
he got right back to me and said yes. He said that he didn't have time to work
on it anymore and so I should feel free to do whatever I thought was best.

[p]: http://www.pauldix.net

Score!

My first order of business was to go through the many open issues and pull
requests on GitHub. When I started there were over 60, a number that I've gotten
down to just a few. I thought it was important to ensure that users saw me treat
their issue as important and even if it was very old (which many were), I asked
if there was anything I could do to help.

I was pleasantly surprised by the nice way many people responded and we got to
work addressing their questions and issues.

As I was working through issues and pull requests, I kept [SemVer][s] in mind -
bug fixes in patch releases and backward-compatible changes in minor releases.
But I also realized that it was past time for this project to be at version 1.0.
In the SemVer FAQ, they talk about when to release version 1.0 and Feedzirra fit
the bill: it was being used in production, there was a stable API and I was
taking backwards compatibilty seriously.

[s]: http://semver.org

So I treated it as a project at 1.0 and I did my best to release versions that
were backward compatible and added deprecations for what I wanted to do in 1.0.
I saw things that I wanted to completely rewrite, but I resisted the urge to
burn it all down and start again.

When I was close to being caught up on the backlog of issues and pull requests,
I started thinking about releasing version 1.0, and I knew I wanted to create a
website for the project. I worked with [Daniel Ariza][d] to make it happen. I
ripped apart the README and rewrote just about all the sections.

[d]: http://danielariza.com

There was an open issue on the project about renaming the Gem and I knew that
launching the website and releasing 1.0 would be the perfect opportunity, so I
went for it. There was a suggestion to change the name to Feedzilla, but since
that is already a thing, I went with Feedjira. I bought the domain and setup an
organization by that name on GitHub.

With those things in place, I needed to actually update the code for these
changes. I wanted to make this transition as easy as possible and devised a
simple way to use [three versions][v] to make the jump to 1.0.

[v]: /versions.html

For most users, upgrading to 1.0 should be a breeze, but I have an [upgrade
page][u] to help with a couple details. If you have any trouble upgrading,
please let me know by [opening an issue][i].

[u]: /upgrading.html
[i]: https://github.com/feedjira/feedjira/issues

There are still lots of things I'd like to do with this Gem. I mentioned seeing
things that I wanted to completely rewrite, so that'll be something that I work
on for a 2.0 release, but that's a ways off. I'd like to officially support
JRuby. Many people use Feedjira with Rails, so a separate project that helps
those users get up and running quickly seems to have value.

The list goes on.

I do have a request before I finish this thing: I'd like to hear from users that
have apps in production using Feedjira. If you're using Feedjira for a
commercial app, please [email me][e]!

[e]: feedjira@gmail.com

Thanks to everyone who has helped me accomplish this, but especially [Paul
Dix][p] for creating such a fun project to work on, [Daniel Ariza][d] for a
badass website design and the many people who opened issues or sent pull
requests. Open source is fun to work on because of people like you!! <3 <3 <3
