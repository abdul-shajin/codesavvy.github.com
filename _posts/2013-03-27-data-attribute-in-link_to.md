---
layout: post
title: "Data attribute in link_to"
category: posts
---
Data attributes can be added in a link_to by,
{% highlight ruby %}
<%= link_to "foo", foo_path, data: { foo: "bar" } %>
{% endhighlight %}
