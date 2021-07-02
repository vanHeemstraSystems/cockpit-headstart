# 500 - Cockpit Starter Kit

## 100 - The bare minimum

[Cockpit’s API](https://cockpit-project.org/guide/latest/development.html) makes it easy to create your own pages (or “extensions” if you will) that appear in Cockpit’s menu and interact with your system in any way you like. Our pet example is the [Pinger](https://github.com/cockpit-project/cockpit/tree/master/examples/pinger) which is just the bare minimum: a [HTML file](https://github.com/cockpit-project/cockpit/blob/master/examples/pinger/ping.html) with a form to enter an IP, a small piece of [JavaScript](https://github.com/cockpit-project/cockpit/blob/master/examples/pinger/pinger.js) to call the ```ping``` Linux command through Cockpit [spawn()](https://cockpit-project.org/guide/latest/cockpit-spawn.html) and capture its output; and a manifest file which tells cockpit how to add it to the menu and where the entry point is.

There is a rather old blog post which explains the Pinger example in detail. Cockpit changed its visual design quite dramatically since then, Pinger’s JavaScript got split into a separate file and does not use jQuery any more, but aside from these details that post is still generally applicable.

