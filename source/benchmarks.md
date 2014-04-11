# Benchmarks

Speed is an important feature of Feedjira so benchmarks are used to ensure its
fast and stays that way. There is a separate project for this work:
[feedjira-benchmarks][b].

[b]: https://github.com/feedjira/feedjira-benchmarks

## Approaches to Fetching

One way Feedjira achieves its speed is by fetching feeds in parallel. When more
than one feed url is passed in, then a `Curl::Multi` is performed. This
benchmark compares ways to fetch feed urls:

```
                  user     system      total        real
Net::HTTP     0.190000   0.070000   0.260000 ( 12.351617)
Curl::Easy    0.070000   0.100000   0.170000 ( 13.245304)
Curl::Multi   0.030000   0.040000   0.070000 (  0.850036)
```

[![Approaches to Fetching](fetch-benchmark.png)](images/fetch-benchmark.png)

Its a little unfair to run this type of benchmark because we're actually hitting
the network and downloading XML over our internet connection. Speeds vary, so
the exact numbers aren't as important here - just the trend. Its no surprise
that the `Curl::Multi` approach is much faster.

See the [fetching systems code][fetching_systems] for more details.

[fetching_systems]: https://github.com/feedjira/feedjira-benchmarks/blob/master/fetch/benchmark.rb

## Parsing Benchmarks

Once the XML has been fetched, Feedjira parses it and then returns a Feed
object. This parsing is the real work of the library and its important that it
stays fast, so its benchmarked across each version of the gem:

```
            user     system      total        real
v0.1.0  1.330000   0.000000   1.330000 (  1.339773)
v0.1.1  1.300000   0.000000   1.300000 (  1.301276)
v0.1.2  1.230000   0.000000   1.230000 (  1.235078)
v0.1.3  1.270000   0.010000   1.280000 (  1.278005)
v0.2.1  1.450000   0.000000   1.450000 (  1.454689)
v0.2.2  1.440000   0.000000   1.440000 (  1.443726)
v0.3.0  1.480000   0.000000   1.480000 (  1.489133)
v0.4.0  1.530000   0.010000   1.540000 (  1.542944)
v0.5.0  1.480000   0.000000   1.480000 (  1.477226)
v0.6.0  1.490000   0.000000   1.490000 (  1.488935)
v0.7.0  1.460000   0.010000   1.470000 (  1.465545)
v0.7.1  1.500000   0.010000   1.510000 (  1.500025)
v0.9.0  1.530000   0.000000   1.530000 (  1.524827)
v1.0.0  1.540000   0.000000   1.540000 (  1.543938)
v1.1.0  1.540000   0.010000   1.550000 (  1.549528)
```

[![chart.png](parse-benchmark.png)](images/parse-benchmark.png)

Again, the exact numbers aren't that important - what's should stand out here is
how consistent from version to version these numbers are. Feedjira is fast at
parsing and hasn't changed much over the course of its life.

See the [basic benchmark code][basic] for more details.

[basic]: https://github.com/feedjira/feedjira-benchmarks/blob/master/parse/benchmark.rb

## Other Libraries

This benchmark compares various alternatives to Feedjira. As of 11/29/2013,
these are the top 10 gems in the [Atom & RSS Feed Parsing
category][alternatives] on Ruby Toolbox:

[alternatives]: https://www.ruby-toolbox.com/categories/feed_parsing

* Feedjira
* Simple-rss
* Feed-normalizer
* Ratom
* Rfeedparser
* FeedParser
* Feed me
* Feedtosis
* Ruby-feedparser
* Opds

Only some of these are still under active deveopment and still others aren't a
good fit for this type of benchmark comparison. Notes on those that were left
out:

* Ratom - only supports Atom
* Rfeedparser - can't install, depends on hpricot v0.6
* Feedtosis - can't install, unresolved dependencies
* Ruby-feedparser - uses the same constant as FeedParser and is slower, so I
  left it out
* Opds - aimed at OPDS specifically

The remaining alternatives are benchmarked to see how fast they can parse feed
XML.


```
                      user     system      total        real
feedjira          1.660000   0.000000   1.660000 (  1.666681)
simple-rss       48.190000   0.160000  48.350000 ( 48.409607)
feed-normalizer  45.330000   0.160000  45.490000 ( 45.604158)
feed_me           0.230000   0.000000   0.230000 (  0.234152)
feed_parser       0.210000   0.000000   0.210000 (  0.217082)
```

[![Others](others-benchmark.png)](images/others-benchmark.png)

Feedjira is beat slightly by a couple of these parsing libraries, but we think
the additional features more than make up for any differences.

See the [other benchmark code][other_benchmark] for more details.

[other_benchmark]: https://github.com/feedjira/feedjira-benchmarks/blob/master/others/benchmark.rb
