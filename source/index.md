[Feedjira][github] (formerly Feedzilla) is a Ruby library designed to fetch and
parse feeds as quickly as possible. Version 1.0 [was recently released][one].

[github]: https://github.com/feedjira/feedjira
[one]: /blog/feedjira-goes-one-point-oh.html

<a class="button" href="/upgrading.html">Learn more about upgrading to 1.0</a>

The fetching and parsing logic have been decoupled and can be used separately if
don't need everything that Feedjira offers.

<a class="button" href="/fetching-and-parsing.html">Learn more about fetching and parsing</a>

Once feeds have been fetched, they can be updated using the feed objects that
are returned. Feedjira automatically inserts etag and last-modified information
from the http response headers to lower bandwidth usage, eliminate unnecessary
parsing, and make things speedier in general.

<a class="button" href="/updating-feeds.html">Learn more about updating feeds</a>

Users can provide callbacks that get invoked on success and failure. This makes
it easy to do things like log errors or update data stores.

<a class="button" href="/callbacks.html">Learn more about callbacks</a>

Feedjira is very extensible with great support for adding your own custom parser
classes or just on the fly customizations like adding an attribute to all or
just one feed.

<a class="button" href="/extending.html">Learn more about extending</a>

## Getting Started

Feedjira requires Ruby version 1.9.2 or greater and like any Ruby gem, the first
step is to install the gem:

```
$ gem install feedjira
```

Or add it to your Gemfile:

```ruby
gem 'feedjira'
```

## Testing

Feedjira uses [curb][] to perform requests. `curb` provides bindings for
[libcurl][] and supports numerous protocols, including FILE. To test Feedjira
with a local file, use the `file://` protocol:

[libcurl]: http://curl.haxx.se/libcurl/

```ruby
feed = Feedjira::Feed.fetch_and_parse('file:///home/feedzirra/examples/feed.rss')
```

## Speed and Benchmarks

An important goal of Feedjira is speed - fetching is fast by using libcurl-multi
through the [curb][] gem. Similarly, parsing is made fast by using libxml
through [nokogiri][] and [sax-machine][].

[curb]: https://github.com/taf2/curb
[nokogiri]: https://github.com/sparklemotion/nokogiri
[sax-machine]: https://github.com/pauldix/sax-machine

To ensure its fast and stays that way, benchmarks are provided that compare it
to other feed libraries and itself.

<a class="button" href="/benchmarks.html">View the benchmarks</a>
