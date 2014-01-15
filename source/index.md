[Feedjira][github] is a Ruby library designed to fetch and parse feeds as
quickly as possible. The fetching and parsing logic have been decoupled and can
be used separately if don't need everything that Feedjira offers.

[github]: https://github.com/feedjira/feedjira

[Learn more about fetching and parsing](/fetching-and-parsing.html)

Once feeds have been fetched, they can be updated using the feed objects that
are returned. Feedjira automatically inserts etag and last-modified information
from the http response headers to lower bandwidth usage, eliminate unnecessary
parsing, and make things speedier in general.

[Learn more about updating feeds](/updating-feeds.html)

Callback are supported that get invoked on success and failure. This makes it
easy to do things like log errors or update data stores.

[Learn more about callbacks](/callbacks.html)

Feedjira is very extensible with great support for adding your own custom parser
classes or just on the fly customizations like adding an attribute to all or
just one feed.

[Learn more about extending](/extending.html)

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
with local file use `file://` protocol:

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

[View the benchmarks](/benchmarks.html)
