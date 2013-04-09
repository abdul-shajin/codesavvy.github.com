---
layout: post
title: "Setting up rails app for TDD"
category: posts
---

NB: Created for my own reference

##How to set up rails app for Test Driven and Behavioud Driven Development
Include Rspec gem

{% highlight ruby %}
group :development, :test do
  gem 'sqlite3', '1.3.5'
  gem 'rspec-rails', '2.11.0'
end
{% endhighlight %}

Bundle the gem
{% highlight ruby %}
bundle install
{% endhighlight %}

Next we need to configure rails app to use Rspec instead of `Test::Unit` 
{% highlight ruby %}
` rails generate rspec:install`
{% endhighlight %}

##Automate Tests with Guard

Add appropriate `gems`
{% highlight ruby %}
group :development, :test do
  gem 'rspec-rails', '2.11.0'
  gem 'guard-rspec', '1.2.1'
  gem 'capybara', '1.1.2'
end
{% endhighlight %}

And
{% highlight ruby %}
group :development, :test do
  gem 'sqlite3', '1.3.5'
  gem 'rspec-rails', '2.11.0'
  gem 'guard-rspec', '1.2.1'
end
{% endhighlight %}

`bundle` again

Initialize guard with rspec

`bundle exec guard init rspec`

Additions to Guardfile

{% highlight ruby %}
require 'active_support/core_ext'

guard 'rspec', :version => 2, :all_after_pass => false do
  .
  .
  .
  watch(%r{^app/controllers/(.+)_(controller)\.rb$})  do |m|
    ["spec/routing/#{m[1]}_routing_spec.rb",
     "spec/#{m[2]}s/#{m[1]}_#{m[2]}_spec.rb",
     "spec/acceptance/#{m[1]}_spec.rb",
     (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" : 
                       "spec/requests/#{m[1].singularize}_pages_spec.rb")]
  end
  watch(%r{^app/views/(.+)/}) do |m|
    (m[1][/_pages/] ? "spec/requests/#{m[1]}_spec.rb" : 
                       "spec/requests/#{m[1].singularize}_pages_spec.rb")
  end
  .
  .
  .
end

{% endhighlight %}

We can start Guars as below
`bundle exec guard`

Create routing file to avoid warning for not having the folder
`mkdir spec/routing`

##Speeding up Tests with `SPORK`

{% highlight ruby%}
group :development, :test do
  .
  .
  .
  gem 'guard-spork', '1.2.0'
  gem 'spork', '0.9.2'
end
{% endhighlight %}

bundle and bootstrap Spork
`bundle`
`bundle exec spork --bootstrap`

edit `spec_helper` file as given below
{% highlight ruby %}

require 'rubygems'
require 'spork'

Spork.prefork do
  # Loading more in this block will cause your tests to run faster. However, 
  # if you change any configuration or code from libraries loaded here, you'll
  # need to restart spork for it take effect.
  # This file is copied to spec/ when you run 'rails generate rspec:install'
  ENV["RAILS_ENV"] ||= 'test'
  require File.expand_path("../../config/environment", __FILE__)
  require 'rspec/rails'
  require 'rspec/autorun'

  # Requires supporting ruby files with custom matchers and macros, etc,
  # in spec/support/ and its subdirectories.
  Dir[Rails.root.join("spec/support/**/*.rb")].each {|f| require f}

  RSpec.configure do |config|
    # == Mock Framework
    #
    # If you prefer to use mocha, flexmock or RR, uncomment the appropriate line:
    #
    # config.mock_with :mocha
    # config.mock_with :flexmock
    # config.mock_with :rr
    config.mock_with :rspec

    # Remove this line if you're not using ActiveRecord or ActiveRecord fixtures
    config.fixture_path = "#{::Rails.root}/spec/fixtures"

    # If you're not using ActiveRecord, or you'd prefer not to run each of your
    # examples within a transaction, remove the following line or assign false
    # instead of true.
    config.use_transactional_fixtures = true

    # If true, the base class of anonymous controllers will be inferred
    # automatically. This will be the default behavior in future versions of
    # rspec-rails.
    config.infer_base_class_for_anonymous_controllers = false
  end
end

Spork.each_run do
  # This code will be run each time you run your specs.

end

{% endhighlight %}

Do 
`bundle exec spork`

Configuring Rspec automatically using Spork
(Edit .rspec file)

{% highlight ruby%}
--colour
--drb
{% endhighlight %}

#Guard With Spork
In command line,
`bundle exec guard init spork`





