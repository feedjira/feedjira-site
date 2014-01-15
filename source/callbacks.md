## Callbacks

Feedjira supports both a success and failure callback, which are provided to
`fetch_and_parse`:

```ruby
success_callback = lambda { |url, feed| puts url, feed }
failure_callback = lambda { |curl, err| puts curl, err }
Feedjira::Feed.fetch_and_parse urls, on_success: success_callback, on_failure: failure_callback
```
