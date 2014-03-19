# Updating Feeds

Once you've [fetched and parsed][f] a feed, you'll want to update it:

[f]: /fetching-and-parsing.html

```ruby
updated_feeds = Feedjira::Feed.update(feeds.values)
updated_feed = updated_feeds['http://feedjira.com/blog/feed.xml']
updated_feed.updated?    # => returns true if any of the feed attributes have changed
updated_feed.new_entries # => a collection of the entry objects that are newer than the latest in the feed before update
```

The above example assumes you have an array of feeds returned from the
`Feedjira::Feed.fetch_and_parse` method, but what's much more likely is that
you'll persist that stuff and then want to update without those object in
memory. This is not currently supported, but something that's coming soon.
