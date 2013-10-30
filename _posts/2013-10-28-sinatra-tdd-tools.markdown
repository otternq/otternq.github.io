---
layout: post
title:  "Sinatra Test Driven Development, Tools"
date:   2013-10-28 18:00:05
tags: ["ruby", "sinatra", "TDD"]
---

I'm just starting to work with Sinatra / Ruby, and I've been looking at automated testing to help follow Test Driven Development (TDD). 

#Test Coverage

Test Coverage is very importanat in TDD, and for that I'm using _Simplecov_. With just a couple of additional lines of code, I am able to:
- Monitor the entire code base
- Exclude test suite from coverage
- Categorize the files being tested.

To start, add `gem 'simplecov'` to your _Gemfile_ and add `SimpleCov.start` to your *spec_helper.rb*. This is all you have to add for full test coverage reports, it will generate a _coverage_ folder with a very nice looking report. It covers the following data points for each file:
- % covered
- Lines
- Relevant Lines
- Lines covered
- Lines missed
- Avg. Hits / Line

Also each file can be loaded and it will tell you how many times a specific line executed during the tests. 

As I said above, _Simplecov_ allows you to define groups/categories for patters, this way you can see that all of your views are covered but your controllers are only at 60%. Here is my _Simplecov_ configuration in *spec_helper.rb*:

{% highlight ruby %}
SimpleCov.start do

    add_filter '/spec/'

    add_group 'Utils', 'src/utils'
    add_group 'Models', 'src/models'
    add_group 'Helpers', 'src/helpers'
    add_group 'Apps', 'src/hook.rb'

end if ENV["COVERAGE"]
{% endhighlight %}

the `if ENV["COVERAGE"] part stops _autotest_ from generating coverage reports every single time I save a file. Instead I run _Simplecov_ manually with a _Rake_ command.

Here is the _Simplecov_ portion of my *Rakefile*

{% highlight ruby%}
task :coverage do
    ENV['COVERAGE'] = 'true'
    Rake::Task["spec"].execute
end
{% endhighlight %}

and then just run `rake coverage`.

#Notifications

While reading I found a tutorial about having autotest report test results with Grunt notifications (I'm running on OSX Maverick). I purchased and installed Grunt and notifications worked about 30-40% of the time...not so awesome; I assumed that someone, somewhere on GitHub, has created a similar tool to allow notifications to work with the now standard _Notifications_ system. Luckly for me, GitHub user [twe4ked](https://github.com/twe4ked) wrote such a gem: [rspec-nc](https://github.com/twe4ked/rspec-nc).

I just added `gem 'rspec-nc'` to my _Gemfile_ and the line `--format=doc --format=Nc` to my _.rspec_ file. (also add the `--color` flag on another line, its great).

Now when I run `autotest` it watches for file changes, and runs my tests as it was before, and I get a notification telling me if the test successed or how many errors I just caused.

#Notes
- Installing Grunt wasn't a waste of time, now iTerm2 keeps me up to date on other proccesses, specificaly I like that it lets me know when commands hang.

- Also, here is my _.rspec_ file. These few changes really help its readability
{% highlight bash %}
--format nested
--color
--format=doc --format=Nc
{% endhighlight %}
