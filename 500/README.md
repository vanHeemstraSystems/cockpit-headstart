# 500 - Cockpit Starter Kit

## 100 - The bare minimum

[Cockpit’s API](https://cockpit-project.org/guide/latest/development.html) makes it easy to create your own pages (or “extensions” if you will) that appear in Cockpit’s menu and interact with your system in any way you like. Our pet example is the [Pinger](https://github.com/cockpit-project/cockpit/tree/master/examples/pinger) which is just the bare minimum: a [HTML file](https://github.com/cockpit-project/cockpit/blob/master/examples/pinger/ping.html) with a form to enter an IP, a small piece of [JavaScript](https://github.com/cockpit-project/cockpit/blob/master/examples/pinger/pinger.js) to call the ```ping``` Linux command through Cockpit [spawn()](https://cockpit-project.org/guide/latest/cockpit-spawn.html) and capture its output; and a [manifest file](https://github.com/cockpit-project/cockpit/blob/master/examples/pinger/manifest.json) which tells cockpit how to add it to the menu and where the entry point is.

There is a rather old [blog post](https://cockpit-project.org/blog/creating-plugins-for-the-cockpit-user-interface.html) which explains the Pinger example in detail. Cockpit changed its visual design quite dramatically since then, Pinger’s JavaScript got split into a separate file and does not use jQuery any more, but aside from these details that post is still generally applicable.

## 200 - Requirements for real projects

Pinger is great for explaining and understanding the gist of how Cockpit works. But an actual production-ready project requires a lot more:

- Separation of HTML, CSS, and JavaScript code: This ensures that your code can use a safe [Content-Security-Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) and does not have to use e.g. ```unsafe-inline```. We strongly recommend this for third-party pages, and absolutely require this for Cockpit’s own pages.

- Modern frameworks for creating page contents. For any non-trivial page you really don’t want to dabble with piecing together ```myelement.innerHTML = …``` strings, but use something like [React](https://reactjs.org/) to build page contents and [PatternFly](http://www.patternfly.org/) so that your page fits into Cockpit’s design.

- Use Babel to write your code in modern ES6 JavaScript.

- Use ESLint to spot functional and legibility errors in your code.

- A build system like webpack to drive all of the above and build blobs (“minified Javascript in a single file”) that are efficiently consumable by browsers.

- Building of release tarballs, source and binary RPMs for testing and distribution.

- Tests to make sure your code keeps working, new features work on all supported operating systems, and changes (pull requests) get validated.

- As a bonus, easy and safe testing of your page in a Vagrant virtual machine.

Sounds complex? It indeed is for someone who is not familiar with the ever-changing “modern” JavaScript world, and doesn’t want to learn the details of all of these before you can even begin working on your code. This is where the Starter Kit comes in!
