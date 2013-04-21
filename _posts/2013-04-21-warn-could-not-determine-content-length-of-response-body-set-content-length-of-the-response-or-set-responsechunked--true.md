---
layout: post
title: "WARN Could not determine content length of response body. Set content length of the response or set Response#chunked = true"
category: posts
---

If u feel disturbed seeing this on your development log which u can safely ignore,

Simply add webrick gem to your Gemfile.

{% highlight ruby %}
group :development do
  gem 'webrick', '~> 1.3.1'
end
{% endhighlight %}

Or use `thin` server instead of webrick

{% highlight ruby %}
group :development do
  gem 'thin'
end
{% endhighlight %}

Do `bundle` have fun ;)
