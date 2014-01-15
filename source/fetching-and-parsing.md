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
