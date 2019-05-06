# MemCachier Rails Elastic Beanstalk Tutorial App

This is an example Rails application that demonstrates the use of
caching using [MemCachier](https://www.memcachier.com) on AWS Elastic
Beanstalk. This example is written with Rails 5.2.

You can read the full tutorial
[here](https://blog.memcachier.com/2019/05/06/rails-on-elastic-beanstalk/).

## Setup MemCachier

Setting up MemCachier to work in Rails is very easy. You need to make
changes to Gemfile, production.rb, and any app code that you want
cached. These changes are covered in detail below.

### Gemfile

MemCachier has been tested with the [dalli memcache
client](https://github.com/mperham/dalli). Add the following gem to
your Gemfile:

```ruby
gem 'dalli'
```

### production.rb

Ensure that the following configuration option is set in production.rb:

```ruby
config.cache_store = :mem_cache_store,
                    (ENV["MEMCACHIER_SERVERS"] || "").split(","),
                    {:username => ENV["MEMCACHIER_USERNAME"],
                     :password => ENV["MEMCACHIER_PASSWORD"],
                     :failover => true,
                     :socket_timeout => 1.5,
                     :socket_failure_delay => 0.2,
                     :down_retry_delay => 60
                    }
```

## Using MemCachier

In your application, use `Rails.cache` methods to access MemCachier.
A list of methods is available
[here](http://api.rubyonrails.org/classes/ActiveSupport/Cache/Store.html).
All the built-in Rails caching tools will work, too.

## Get involved!

We are happy to receive bug reports, fixes, documentation enhancements,
and other improvements.

Please report bugs via the
[github issue tracker](http://github.com/memcachier/examples-rails-contacts/issues).

Master [git repository](http://github.com/memcachier/examples-rails-contacts):

* `git clone git://github.com/memcachier/examples-rails-contacts.git`

## Licensing

This library is BSD-licensed.
