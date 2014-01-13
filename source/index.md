[Feedjira][github] is a Ruby library designed to fetch and parse feeds as
quickly as possible. Fetching is fast by using libcurl-multi through the
[curb][] gem. Similarly, parsing is made fast by using libxml through
[nokogiri][] and [sax-machine][]. Feedzirra requires Ruby version 1.9.2 or
greater.

[github]: https://github.com/feedjira/feedjira
[curb]: https://github.com/taf2/curb
[nokogiri]: https://github.com/sparklemotion/nokogiri
[sax-machine]: https://github.com/pauldix/sax-machine

Once you have fetched feeds using Feedjira, they can be updated using the feed
objects that are returned. Feedjira automatically inserts etag and last-modified
information from the http response headers to lower bandwidth usage, eliminate
unnecessary parsing, and make things speedier in general.

Callback are supported that get called on success and failure. This makes it
easy to do things like log errors or update data stores.

The fetching and parsing logic have been decoupled so that either of them can be
used in isolation if you'd prefer not to use everything that Feedjira offers.
However, the code examples below use helper methods in the `Feed` class that put
everything together to make things as simple as possible.

Lastly, Feedjira has the ability to define custom parsing classes. In truth,
Feedjira could be used to parse much more than feeds. Microformats, page
scraping, and almost anything else are fair game.

## Fetch and Parse

For many users, the `fetch_and_parse` method is what they use Feedjira for. This
method takes your urls and then returns Feed objects:

```ruby
urls = %w[http://feedjira.com/blog/feed.xml https://github.com/feedjira/feedjira/feed.xml]
feeds = Feedjira::Feed.fetch_and_parse urls # returns a Hash, with each url having a Feedjira::Feed object
# => {
#      'http://feedjira.com/blog/feed.xml' => <Feedjira::Feed ..>,
#      'https://github.com/feedjira/feedjira/feed.xml' => <Feedjira::Feed ..>
#    }
```

These feed objects have both the meta data for a feed and an `entries`
collection that contains all the entries that were found:

```ruby
feed = feeds['http://feedjira.com/blog/feed.xml']
feed.title   # => "The Feedjira Blog"
feed.url     # => "http://feedjira.com/blog/feed.xml"
feed.entries # returns an array of Entry objects
# => [<Feedjira::Feed::Entry ...>, <Feedjira::Feed::Entry ...>, ...]
```

These entry objects contain the data parsed from the feed XML:

```ruby
entry = feed.entries.first
entry.title # => "Announcing verison 1.0"
entry.url   # => "http://feedjira.com/blog/2014-02-12-announcing-version-10.html"
```

Check the documentation for a complete list of the methods available to you on
the [Feed][feed] and [Entry][entry] classes.

[feed]: http://link/to/docs?
[entry]: http://link/to/docs?

## Updating Feeds

You'll most likely want to update the feed objects you fetch at some interval
and Feedjira provides an easy way to do that:

```ruby
updated_feeds = Feedzirra::Feed.update(feeds.values)
updated_feed = updated_feeds['http://feedjira.com/blog/feed.xml']
updated_feed.updated?    # => returns true if any of the feed attributes have changed
updated_feed.new_entries # => a collection of the entry objects that are newer than the latest in the feed before update
```

## Callbacks

Feedjira supports both a success and failure callback, which are provided to
`fetch_and_parse`:

```ruby
success_callback = lambda { |url, feed| puts url, feed }
failure_callback = lambda { |curl, err| puts curl, err }
Feedjira::Feed.fetch_and_parse urls, on_success: success_callback, on_failure: failure_callback
```

## Just Fetching

The fetching functionality of Feedjira has been exposed so that it can be used
in isolation:

```ruby
Feedjira::Feed.fetch_raw urls
# => {
#      'http://feedjira.com/blog/feed.xml' => '<?xml ...?>',
#      'https://github.com/feedjira/feedjira/feed.xml' => '<?xml ...?>'
#    }
```

## Just Parsing

The parsing functionality of Feedjira has been exposed so that it can be used in
isolation:

```ruby
xml = '<?xml ...?>' # the XML from http://feedjira.com/blog/feed.xml
Feedjira::Feed.parse xml
# => {
#      'http://feedjira.com/blog/feed.xml' => <Feedjira::Feed ..>
#    }
```

## Extending

### Adding a feed parsing class

When determining which parser to use for a given XML document, the following
list of parser classes is used:

* `Feedzirra::Parser::RSSFeedBurner`
* `Feedzirra::Parser::GoogleDocsAtom`
* `Feedzirra::Parser::AtomFeedBurner`
* `Feedzirra::Parser::Atom`
* `Feedzirra::Parser::ITunesRSS`
* `Feedzirra::Parser::RSS`

You can insert your own parser at the front of this stack by calling
`add_feed_class`, like this:

```ruby
Feedzirra::Feed.add_feed_class MyAwesomeParser
```

Now when you `fetch_and_parse`, `MyAwesomeParser` will be the first one to get a
chance to parse the feed.

If you have the XML and just want to provide a parser class for one parse, you
can specify that using `parse_with`:

```ruby
Feedzirra::Feed.parse_with MyAwesomeParser, xml
```

### Adding attributes to all feeds types / all entries types

```ruby
# Add the generator attribute to all feed types
Feedzirra::Feed.add_common_feed_element('generator')
Feedzirra::Feed.fetch_and_parse("http://www.pauldix.net/atom.xml").generator # => 'TypePad'

# Add some GeoRss information
Feedzirra::Feed.add_common_feed_entry_element('geo:lat', :as => :lat)
Feedzirra::Feed.fetch_and_parse("http://www.earthpublisher.com/georss.php").entries.each do |e|
  p "lat: #[e.lat}, long: #{e.long]"
end
```

### Adding attributes to only one class

If you want to add attributes for only one class you simply have to declare them
in the class

```ruby
# Add some GeoRss information
require 'lib/feedzirra/parser/rss_entry'

class Feedzirra::Parser::RSSEntry
  element 'geo:lat', :as => :lat
  element 'geo:long', :as => :long
end

# Fetch a feed containing GeoRss info and print them
Feedzirra::Feed.fetch_and_parse("http://www.earthpublisher.com/georss.php").entries.each do |e|
  p "lat: #{e.lat}, long: #{e.long}"
end
```

## Testing

Feedzirra uses [curb][] to perform requests. `curb` provides bindings for
[libcurl][] and supports numerous protocols, including FILE. To test Feedzirra
with local file use `file://` protocol:

[libcurl]: http://curl.haxx.se/libcurl/

```ruby
feed = Feedzirra::Feed.fetch_and_parse('file:///home/feedzirra/examples/feed.rss')
```

## Benchmarks

Since a major goal of Feedzirra is speed, benchmarks are provided--see the
[Benchmark README][benchmark_readme] for more details.

[benchmark_readme]: https://github.com/pauldix/feedzirra/blob/master/benchmarks/README.md
