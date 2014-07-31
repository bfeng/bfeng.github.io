---
layout: post
title: "Hello octopress"
date: 2014-07-11 10:12:47 -0500
comments: true
categories: blogging fun
---

This is first post from octopress. Octopress is an awesome blogging framework, which provides many handful facilities.

## Source commands

Many handful functionalites are wrapped in the `Rakefile`, which is a definetion file for `rake` commond. Basicly, the commands defined are:

  - install[]: the initial setup for Octopress to install a theme
  - generate: generate Jekyll site
  - watch: watch the site changes and regenerate if necessary
  - preview: launch a local website and preview in a web browser
  - new_post[]: make a new post in the `_post` folder
  - new_page[]: make a new page
  - update_style: move sass to sass.old, install sass theme updates
  - update_source: move source to source.old
  - gen_deploy: generate your blog, copy the generated files into `_deploy/`, add them to git, commit and push them up to the master branch (from [1]).

## Useful plugins

### Codeblock

Normally the Markdown paraser in Jekyll can convert the line starts with a double indent into a code block, like this:

    This is a line of code!

However, Codeblock does more than that--it provides language highlights with/without line numbers.
The following is line of python code.

In the source code, it is typed like this:


    {{ "{% codeblock lang:python" }} %}
    print "Hello, world"
    {{ "{% endcodeblock" }} %}

Then, the codeblock above will be rendered like this:

{% codeblock lang:python %}
print "Hello, world"
{% endcodeblock %}

### Video Tag

The video tag is very userful, when a video is displayed on the web page.
The usage and example can be found here: [2].

[1]: http://octopress.org/docs/deploying/github/ "Octopress Documentation"
[2]: http://octopress.org/docs/plugins/video-tag/ "Video Tag"
