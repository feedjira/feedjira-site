---
title: Feedjira Two-Point-Oh
---

About a year ago, I took Feedjira to [version 1.0][one] and today I'm releasing
version 2.0. Not much has changed actually - the biggest difference is that
`curb` has been replaced with `faraday`. For many users, upgrading to version
2.0 won't require anything more than a `bundle update feedjira`.

[one]: http://feedjira.com/blog/2014/03/17/feedjira-goes-one-point-oh.html

The other big change is that the `Feedjira#update` method was removed. It was
unreliable and mostly just caused issues. To read more about why this was
removed, check out [this comment][comment] on a GitHub issue that was opened
about it not working as expected.

[comment]: https://github.com/feedjira/feedjira/issues/218#issuecomment-40282091

I've also updated the site to reflect the changes in this version. I took the
opportunity to greatly simply things and got just about all the documentation to
fit on one page.

I hope you like version 2.0 - feel free to hit me up [on Twitter][twitter] or if
you have any trouble, open a [GitHub issue][issue] and I'll give you a hand.

[twitter]: https://twitter.com/feedjira
[issue]: https://github.com/feedjira/feedjira/issues

Finally, thanks to those that gave me feedback on either my thoughts on version
2.0 or the release candidate - I really appreciate it!
