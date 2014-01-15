## Updating Feeds

You'll most likely want to update the feed objects you fetch at some interval
and Feedjira provides an easy way to do that:

```ruby
updated_feeds = Feedjira::Feed.update(feeds.values)
updated_feed = updated_feeds['http://feedjira.com/blog/feed.xml']
updated_feed.updated?    # => returns true if any of the feed attributes have changed
updated_feed.new_entries # => a collection of the entry objects that are newer than the latest in the feed before update
```
