---
layout: documentation
title: "BrowserSync API"
page-label: "api"
---

Our API is incredibly simple & powerful. You can use it to create your own
tiny node program for local development or integrate with other tools. To use it, 
simply `require` the BrowserSync module like you would any other. This will give 
you access to the public methods detailed below.

{% highlight javascript %}
{% include scripts/api/require.js %}
{% endhighlight %}


<h3 id="api-browserSync">browserSync( config, cb ) <a href="#api-browserSync" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
Handle External API usage.


<ul class="param-list" id="api-browserSync-config">
    <li class="name">config <a href="#api-browserSync-config" class="page-anchor"><i class="icon icon-external-link"></i></a></li>
    <li class="type">Type: <span class="color-teal">Object</span>
        <span class="recede">[optional]</span>
    </li>
    <li class="desc">This is the main configuration for your BrowserSync instance and can contain any of the [available options](/docs/options)
 If you do not pass a config an argument for configuration, BrowserSync will still run; but it will be in the `snippet` mode</li>
</ul>

<ul class="param-list" id="api-browserSync-cb">
    <li class="name">cb <a href="#api-browserSync-cb" class="page-anchor"><i class="icon icon-external-link"></i></a></li>
    <li class="type">Type: <span class="color-teal">Function</span>
        <span class="recede">[optional]</span>
    </li>
    <li class="desc">If you pass a callback function, it will be called when BrowserSync has completed all setup tasks and is ready to use. This
is useful when you need to wait for information (for example: urls, port etc) or perform other tasks synchronously.</li>
</ul>




{% highlight javascript %}
var config = {
    server: {
        baseDir: "./"
    }
};

// config only
browserSync(config);

// config + callback
browserSync(config, function (err, bs) {
    if (!err) {
        console.log("BrowserSync is ready!");
    }
});
{% endhighlight %}


<h3 id="api-reload">.reload( arg ) <a href="#api-reload" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
The `reload` method will inform all browsers about changed files and will either cause the browser to refresh, or inject the files where possible.


<ul class="param-list" id="api-reload-arg">
    <li class="name">arg <a href="#api-reload-arg" class="page-anchor"><i class="icon icon-external-link"></i></a></li>
    <li class="type">Type: <span class="color-teal">String|Array|Object</span>
        <span class="recede">[optional]</span>
    </li>
    <li class="desc">- The file or files to be reloaded. Provide {stream: true} for streams support.</li>
</ul>




{% highlight javascript %}
// browser reload
browserSync.reload();

// single file
browserSync.reload( "styles.css" );

// multiple files
browserSync.reload( ["styles.css", "ie.css"] );

// streams support
browserSync.reload( { stream: true } );
{% endhighlight %}


<h3 id="api-notify">.notify( msg ) <a href="#api-notify" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
Helper method for browser notifications


<ul class="param-list" id="api-notify-msg">
    <li class="name">msg <a href="#api-notify-msg" class="page-anchor"><i class="icon icon-external-link"></i></a></li>
    <li class="type">Type: <span class="color-teal">String|HTML</span>
        
    </li>
    <li class="desc">Can be a simple message such as 'Connected' or HTML</li>
</ul>




{% highlight javascript %}
browserSync.notify("Compiling, please wait!");

browserSync.notify("HTML <span color='green'>is supported</span> too!");
{% endhighlight %}


<h3 id="api-exit">.exit() <a href="#api-exit" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
This method will close any running server, stop file watching & exit the current process.


{% highlight javascript %}
browserSync(config, function (err, bs) {
    browserSync.exit();
});
{% endhighlight %}


<h3 id="api-emitter">.emitter <a href="#api-emitter" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
The internal Event Emitter used by the running BrowserSync instance (if there is one).
You can use this to emit your own events, such as changed files, logging etc.


{% highlight javascript %}
var evt = browserSync.emitter;

evt.on("init", function () {
    console.log("BrowserSync is running!");
});

browserSync(config);
{% endhighlight %}


<h3 id="api-active">.active <a href="#api-active" class="page-anchor"><i class="icon icon-external-link"></i></a></h3>
A simple true/false flag that you can use to determine if there's a currently-running BrowserSync instance.


{% highlight javascript %}
console.log(browserSync.active); // false

browserSync(config, function (err, bs) {
    console.log(browserSync.active); // true
});
{% endhighlight %}

