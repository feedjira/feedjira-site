# Upgrading to 1.0

The biggest hurdle to upgrading to Feedjira 1.0 is the name change. After you've
done a find and replace in your codebase to change the name, you're likely done.
The goal of Feedjira 1.0 is mostly to correct that this software was already
1.0-calibur and the name change.

The other thing to check is if you're using any deprecated functionality and
this is easy with the Feedjira 0.9 release. Its suggested that you first upgrade
to this version, do your find and replace and then run your tests. If you don't
get any deprecation warnings (and you might not!), then you should be clear to
upgrade to 1.0.
