---
layout: documentation
title: "BrowserSync + Gulp.js"
page-label: "gulp"
---

There's no official BrowserSync plugin for Gulp, because it's not needed! You simply `require` the module, utilise 
the [API]({{site.links.api}}) and configure it with [options]({{site.links.options}}). The following are some common 
use-cases as seen in popular projects such as [Google's web starter kit](https://developers.google.com/web/starter-kit/)
and many others.

{% include headerlink.html title="Install" slug="gulp-install" %}

First, you'll need to install BrowserSync & Gulp as development dependencies.

{% highlight bash %}
{% include snippets/gulp/install.txt %}
{% endhighlight %}

Then, use them within your `gulpfile.js`:

{% highlight javascript %}
{% include snippets/gulp/require.js %}
{% endhighlight %}

{% include headerlink.html title="SASS + CSS Injecting" slug="gulp-sass-css" %}

Streams are supported in BrowserSync, so you can call reload at specific points during your tasks and
all browsers will be informed of the changes. Because BrowserSync only cares about your CSS when it's 
*finished* compiling - make sure you call reload *after* `gulp.dest`

{% highlight javascript %}
{% include snippets/gulp/sass.js %}
{% endhighlight %}

{% include headerlink.html title="SASS & Source Maps" slug="gulp-sass-maps" %}

If you use [gulp-ruby-sass](https://www.npmjs.org/package/gulp-ruby-sass) with the `sourcemap: true` option, additional `.map` 
files will be generated. These files end up being sent down stream and when `browserSync.reload()` receives them, it will attempt
a full page reload (as it will not find any `.map` files in the DOM).

To fix this problem, you can use the [gulp-filter](https://www.npmjs.org/package/gulp-filter) package to ensure that only `*.css`
 files ever reach `.reload` - this way you'll still get CSS injecting.


{% highlight javascript %}
{% include snippets/gulp/sass.maps.js %}
{% endhighlight %}

{% include headerlink.html title="Browser Reloading" slug="gulp-reload" %}

Sometimes you might just want to reload the page completely (for example, after processing a bunch of JS files) - 
you can do that by passing once as an option. This will stop `.reload()` being call multiple times.

{% highlight javascript %}
{% include snippets/gulp/reload.js %}
{% endhighlight %}

{% include headerlink.html title="Manual Reloading" slug="gulp-manual-reload" %}

If the streams support doesn't suit your needs, you can fire the reload method manually 
by wrapping it in a task. This example will compile & auto-inject CSS just as before, but when HTML files are 
changed, the browsers will be reloaded instead.

{% highlight javascript %}
{% include snippets/gulp/reload.manual.js %}
{% endhighlight %}



