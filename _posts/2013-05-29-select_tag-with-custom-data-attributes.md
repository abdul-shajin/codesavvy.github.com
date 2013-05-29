---
layout: post
title: "select_tag with custom data attributes"
category: posts
---
Select tag with data attributes can be done by the following method

{% highlight ruby %}
<%= f.select :country_id, options_for_select(@countries.map{ |c| [c.name, c.id, {'data-currency_code'=>c.currency_code}] }) %>
{% end highlight %}

Adding an initial selection:

{% highlight ruby %}
<%= f.select :country_id, options_for_select(@countries.map{ |c| [c.name, c.id, {'data-currency_code'=>c.currency_code}] }, selected_key = f.object.country_id) %>
{% end highlight %}

If you need grouped options, you can use the grouped_options_for_select helper, like this (if @continents is an array of continent objects, each having a countries method):

{% highlight ruby %}
<%= f.select :country_id, grouped_options_for_select(@continents.map{ |group| [group.name, group.countries.map{ |c| [c.name, c.id, {'data-currency_code'=>c.currency_code}] } ] }, selected_key = f.object.country_id) %>

{% end highlight %}
