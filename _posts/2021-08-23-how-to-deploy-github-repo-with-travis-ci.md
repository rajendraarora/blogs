---
layout: post
title:  "How to deploy github repositories with Travis CI?"
comments: true
date:   2021-08-23
categories: travis 
tags: github repositories travis-ci
---

Github is a nice solution which can be integrated with Travis CI to host website, building solutions/container etc. I am using the same solution to host my blogs using jekyll to host static file via github pages.

I assume, you have github public repo. I will be taking my github blog example to deploy my blog repository with Travis CI.

So, let's begin with the following steps:

# 1. Add `.travis.yml` file in your github repo

We need to add travis build configuration configuration to generate the build, so add `.travis.yml` in your root directory. Below I am adding with my configuration:

{% highlight yml %}
language: ruby
cache: bundler
branches:
  only:
  - main
before_install:
- gem install bundler -v 2.0.1
script:
  - chmod +x ./script/cibuild
  - JEKYLL_ENV=production bundle exec jekyll build --destination site
deploy:
  repo: rajendraarora/blogs.github.io
  provider: pages
  local-dir: ./site
  target-branch: master
  email: deploy@travis-ci.org
  name: Deployment Bot
  skip-cleanup: false 
  github-token: $GITHUB_TOKEN
  keep-history: true
  on:
    branch: master
{% endhighlight %}

# 2. Get your Github Token

. Go to this [page](https://github.com/settings/tokens/new) and generate your token and keep it safe.

. Add your `GITHUB_TOKEN` environment below via go to setting options:

<p algin="center">
    <img src="/assets/img/token-setting-1.png" data-canonical-src="/assets/img/token-setting-1.png" />
</p>

. Add your token below:
<p algin="center">
    <img src="/assets/img/token-setting-2.png" data-canonical-src="/assets/img/token-setting-2.png" />
</p>


# 3. Trigger your Build

. Go to trigger setting options
<p algin="center">
    <img src="/assets/img/trigger-setting-1.png" data-canonical-src="/assets/img/trigger-setting-1.png" s/>
</p>

. Select trigger button
<p algin="center">
    <img src="/assets/img/trigger-setting-2.png" data-canonical-src="/assets/img/trigger-setting-2.png" height="500" />
</p>


That's it.. yay!

# 4. Publish your github pages

. Go to github pages tab and publish it!
<p algin="center">
    <img src="/assets/img/github-page.png" data-canonical-src="/assets/img/github-page.png" />
</p>

<br/><br/>
Feel free to write your comments for any issues or reach out to me directly at `contact[dot]rajendraarora[at]gmail.com`.
<br/>

<div id="disqus_thread"></div>
<script>
var disqus_config = function () {
this.page.url = 'https://blogs.rajendraarora.com/travis/2021/08/23/how-to-deploy-github-repo-with-travis-ci.html';  
// Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = 'travis/2021/08/23/how-to-deploy-github-repo-with-travis-ci.html';
};
(function() {
var d = document, s = d.createElement('script');
s.src = 'https://https-blogs-rajendraarora-com.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
<script id="dsq-count-scr" src="//https-blogs-rajendraarora-com-1.disqus.com/count.js" async></script>
