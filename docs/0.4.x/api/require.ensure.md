---
layout: api
version: 0.4.x
title: require.ensure
spec: CommonJS Experimental
---

{% highlight js %}
require.ensure([dependencies], callbackFunction);
{% endhighlight %}

The CommonJS specification allows for an asynchronous download method named `require.ensure`. It requires an array of dependencies, followed by a callback function. The callback function has the signature

{% highlight js %}
function (require) {}
{% endhighlight %}

The only parameter passed to the callback, `require`, is a local function that can retrieve any of the dependent modules by the name specified in `[dependencies]`.

### Ensure Async Dependencies

The primary use of `require.ensure` is to demand an unknown number of dependencies, and upon completion, map them back into a local scope.

{% highlight js %}
var deps = ['one', 'two', 'three'];
var modules = {};
require.ensure(deps, function (require) {
  for (var i = 0; len = deps.length; i < len; i++) {
    modules[deps[i]] = require(deps[i]);
  }

  // modules now contains the exports of all the dependencies, mapped to their name
});
{% endhighlight %}