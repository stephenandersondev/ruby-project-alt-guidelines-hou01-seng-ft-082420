Best By Me App 
========================

![Best-By-Me_Interface](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)

## About

HTTP (The Gem! a.k.a. http.rb) is an easy-to-use client library for making requests
from Ruby. It uses a simple method chaining system for building requests, similar to
Python's [Requests].

Under the hood, via [Ruby FFI bindings][http-parser-ffi], http.rb uses the Node.js
[http-parser], a fast HTTP parsing native extension. This library
isn't just yet another wrapper around Net::HTTP. It implements the HTTP protocol
natively and outsources the parsing to native extensions.

[requests]: http://docs.python-requests.org/en/latest/
[http-parser]: https://github.com/nodejs/http-parser
[http-parser-ffi]: https://github.com/cotag/http-parser


## Another Business Search Engine? Why should I care?

Best By Me is designed for users who do not have the time or 
interest to spend hours reading reviews and researching businesses. 
When a user enters a business type and a zipcode, our app responds
 with the top ten most highly rated business of that type in their area. 


## Installation

Add this line to your application's Gemfile:
```ruby
gem "http"
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install http
```

Inside of your Ruby program do:
```ruby
export YELP_KEY="place-your-yelp-API-key-here"
```

...to pull it in as a dependency.

```ruby
API_KEY = ENV["YELP_KEY"]
```
Use this link to guide you through the process of acquiring your own API key:

https://www.yelp.com/developers/documentation/v3/authentication

  


## Documentation

[Please see the http.rb wiki][documentation]
for more detailed documentation and usage notes.

The following API documentation is also available:

* [YARD API documentation](http://www.rubydoc.info/gems/http/frames)
* [Chainable module (all chainable methods)](http://www.rubydoc.info/gems/http/HTTP/Chainable)

[documentation]: https://github.com/httprb/http/wiki

### Basic Usage

Here's some simple examples to get you started:

```ruby
>> HTTP.get("https://github.com").to_s
=> "\n\n\n<!DOCTYPE html>\n<html lang=\"en\" class=\"\">\n  <head prefix=\"o..."
```

That's all it takes! To obtain an `HTTP::Response` object instead of the response
body, all we have to do is omit the `#to_s` on the end:

```ruby
>> HTTP.get("https://github.com")
=> #<HTTP::Response/1.1 200 OK {"Server"=>"GitHub.com", "Date"=>"Tue, 10 May...>
```

We can also obtain an `HTTP::Response::Body` object for this response:

```ruby
>> HTTP.get("https://github.com").body
=> #<HTTP::Response::Body:3ff756862b48 @streaming=false>
```

The response body can be streamed with `HTTP::Response::Body#readpartial`.
In practice, you'll want to bind the HTTP::Response::Body to a local variable
and call `#readpartial` on it repeatedly until it returns `nil`:

```ruby
>> body = HTTP.get("https://github.com").body
=> #<HTTP::Response::Body:3ff756862b48 @streaming=false>
>> body.readpartial
=> "\n\n\n<!DOCTYPE html>\n<html lang=\"en\" class=\"\">\n  <head prefix=\"o..."
>> body.readpartial
=> "\" href=\"/apple-touch-icon-72x72.png\">\n    <link rel=\"apple-touch-ic..."
# ...
>> body.readpartial
=> nil
```




