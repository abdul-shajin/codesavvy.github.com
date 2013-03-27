---
layout: post
title: "Fonts in asset pipeline"
category: posts
---
 - Place your new font in the folder `app/assets/fonts`.

 - Tell the server where the fonts are located and that it has to precompile assets with those specific file extensions. You probably only have to add the following lines to your config/environments/production.rb file since you are not precompiling your assets locally. If you are, then also add these lines to your `config/environments/development.rb` file:
{% highlight ruby %}
# Add the fonts path
config.assets.paths << Rails.root.join('app', 'assets', 'fonts')
{% endhighlight %}

{% highlight ruby %}
# Precompile additional assets
config.assets.precompile += %w( .svg .eot .woff .ttf )
{% endhighlight %}

 - Declare your font in your css like so:

{% highlight css %}
@font-face {
  font-family: 'Icomoon';
  src:url('icomoon.eot');
  src:url('icomoon.eot?#iefix') format('embedded-opentype'),
    url('icomoon.svg#icomoon') format('svg'),
    url('icomoon.woff') format('woff'),
    url('icomoon.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
}
{% endhighlight %}

 Make sure that the font is named exactly like in the url portion of the declaration. Capital letters make a difference. So in this case the font should have the name icomoon.

 - If you are using Sass or Less with Rails 3.1 (so your css file has the `.scss` or `.less` extension), then change the `url(...)` in the font declaration to `font-url(...)`.

 If you are not, then your css file should have the extension .css.erb and the font declaration should be like this `url('<%= asset_path(...) %>')`.

 - Finally, use your font in your css like you declared it in the font-family part. Since it was declared capitalized, you can use it like this:

{% highlight css %}
font-family: 'Icomoon';
{% endhighlight %}
