---
### TRANSLATE ONLY "title" CONTENT IN THIS SECTION
layout: page
title: Serving static files in Express
menu: starter
lang: en
redirect_from: "/starter/static-files.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---

# Serving static files in Express

To serve static files such as images, CSS files, and JavaScript files, use the `express.static` built-in middleware function in Express.

Pass the name of the directory that contains the static assets to the `express.static` middleware function to start serving the files directly. For example, if you keep your images, CSS files, and JavaScript files in a directory named `public`, you can use the following code:

<pre><code class="language-javascript" translate="no">
app.use(express.static('public'));
</code></pre>

Now, you can load the files that are in the `public` directory:

<pre><code class="language-javascript" translate="no">
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
</code></pre>

<div class="doc-box doc-info">
The files are looked up relative to the static directory, so the name of the static directory is not part of the URL.
</div>

If you want to use multiple directories as static assets directories, you can call the `express.static` middleware function multiple times:

<pre><code class="language-javascript" translate="no">
app.use(express.static('public'));
app.use(express.static('files'));
</code></pre>

The files are looked up in the order in which you set the static directories by using the `express.static` middleware function.

If you want to create a virtual path prefix (where the path does not actually exist in the file system) for the files that are served by the `express.static` function, you can [specify a mount path](/{{ page.lang }}/4x/api.html#app.use) for the static directory, as shown below:

<pre><code class="language-javascript" translate="no">
app.use('/static', express.static('public'));
</code></pre>

Now, you can load the files that are in the `public` directory from the `/static` path prefix.

<pre><code class="language-javascript" translate="no">
http://localhost:3000/static/images/kitten.jpg
http://localhost:3000/static/css/style.css
http://localhost:3000/static/js/app.js
http://localhost:3000/static/images/bg.png
http://localhost:3000/static/hello.html
</code></pre>

However, the path that you provide to the `express.static` function is relative to the directory from where you launch your `node` process. If you run the express app from another directory, it's safer to use the absolute path of the directory that you want to serve:

<pre><code class="language-javascript" translate="no">
app.use('/static', express.static(__dirname + '/public'));
</code></pre>