---
layout: post
title: Alternative way to resolve "stream_select(): You MUST recompile PHP with a larger value of FD_SETSIZE" issue without recompiling PHP
date: 2014-02-08 12:05
author: mazong1123
comments: true
categories: [Uncategorized]
---
I met a boring issue when adding websocket to a PHP site by using Ratchet (A PHP websocket framework):

"It is set to 1024, but you have descriptors numbered at least as high as 1266.

--enable-fd-setsize=2048 is recommended, but you may want to set it
to equal the maximum number of open files supported by your system"

I struggled and googled it, finally found a bad news: <strong>FD_SIZE is set to 1024 in the PHP source code. The error occurs if the web socket connections are over 1024.</strong> I don't want to modify the PHP source code and recompile it, which may cause unexpected issue. So I try to find another way to solve this issue. Fortunately, I found it.

Basically, I'm opening multiple websocket service processes in the server, and each process has different port. In the front end, I wrote a js function to choose different port to connect. That means we have 1024 * n availiable connections now. Let's go to the details.

<strong>Back-end implementation</strong>

Write a websocket service called push-server.php. Please refer to <a href="http://socketo.me/docs/push" target="_blank">Ratchet's example</a>. However, we need make the php file to accept a port parameter:

<code>$port</code> <code>= </code><code>$argv</code><code>[1];</code>
<div><code>if</code> <code>(</code><code>$port</code> <code>== </code><code>""</code><code>){</code></div>
<div><code>    </code><code>$port</code> <code>= 40003; </code><code>// Default port</code></div>
<div><code>}</code></div>
<div><code>// .....Ignoring other code .....</code></div>
<div></div>
<div><code>// Passing port paramter.</code></div>
<div><code>$webSock</code><code>-&gt;listen(</code><code>$port</code><code>, </code><code>'0.0.0.0'</code><code>);</code></div>
<div></div>
<div></div>
<div>

<span style="line-height:1.5;">Now we can start multiple websocket processes with different ports, for instance:</span>

<span style="line-height:1.5;"> </span>php push-server 40003

php push-server 40004

php push-server 40005

The server can have 1024 * 3 = 3072 websocket connections now.

<strong>Front-end implementation</strong>

The js code to connect websocket service randomly:
<pre>function getWSServer() {
    var serverPorts = ['40003', '40004', '40005'];
    var server = 'ws://youhost';
    var randomPortIndex = Math.floor(Math.random() * serverPorts.length);

    server += ':' + serverPorts[randomPortIndex];

    return server;
};</pre>
</div>
