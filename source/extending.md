# Extending

## Adding a feed parsing class

When determining which parser to use for a given XML document, the following
list of parser classes is used:

* `Feedjira::Parser::RSSFeedBurner`
* `Feedjira::Parser::GoogleDocsAtom`
* `Feedjira::Parser::AtomFeedBurner`
* `Feedjira::Parser::Atom`
* `Feedjira::Parser::ITunesRSS`
* `Feedjira::Parser::RSS`

You can insert your own parser at the front of this stack by calling
`add_feed_class`, like this:

```ruby
Feedjira::Feed.add_feed_class MyAwesomeParser
```

Now when you `fetch_and_parse`, `MyAwesomeParser` will be the first one to get a
chance to parse the feed.

If you have the XML and just want to provide a parser class for one parse, you
can specify that using `parse_with`:

```ruby
Feedjira::Feed.parse_with MyAwesomeParser, xml
```

## Adding attributes to all feeds types / all entries types

```ruby
# Add the generator attribute to all feed types
Feedjira::Feed.add_common_feed_element('generator')
Feedjira::Feed.fetch_and_parse("http://www.pauldix.net/atom.xml").generator # => 'TypePad'

# Add some GeoRss information
Feedjira::Feed.add_common_feed_entry_element('geo:lat', :as => :lat)
Feedjira::Feed.fetch_and_parse("http://www.earthpublisher.com/georss.php").entries.each do |e|
  p "lat: #[e.lat}, long: #{e.long]"
end
```

## Adding attributes to only one class

If you want to add attributes for only one class you simply have to declare them
in the class

```ruby
# Add some GeoRss information
require 'lib/feedzirra/parser/rss_entry'

class Feedjira::Parser::RSSEntry
  element 'geo:lat', :as => :lat
  element 'geo:long', :as => :long
end

# Fetch a feed containing GeoRss info and print them
Feedjira::Feed.fetch_and_parse("http://www.earthpublisher.com/georss.php").entries.each do |e|
  p "lat: #{e.lat}, long: #{e.long}"
end
```
