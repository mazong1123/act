---
layout: post
title: How to enable 'meta_key' option for wordpress REST api filter
date: 2014-08-10 13:48
author: mazong1123
comments: true
categories: [Uncategorized]
---
I'm working at a project which is using wordpress as the backend management system. WP has a great <a href="http://wordpress.org/plugins/json-rest-api/" target="_blank">rest api plugin</a> . However, the filter options are limited. Unfortunately, 'meta_key' is not supported in current version.

I've spent several hours to investigate this plugin, and finally found a one-line-code solution:

1. Find a line in get_posts function:
<pre><code>// Allow the same as normal WP
$valid_vars = apply_filters('query_vars', $wp-&gt;public_query_vars);</code></pre>
2. Add following code below it:
<pre><code>// Add additional key to support.
array_push($valid_vars, 'meta_key');</code></pre>
Done :)

Additionally, add more custom field support you need:
<pre><code>// Add additional custom field keys to support.
array_push($valid_vars, 'meta_key');
array_push($valid_vars, 'meta_value');
array_push($valid_vars, 'meta_value_num');
array_push($valid_vars, 'meta_compare');
array_push($valid_vars, 'meta_query');
</code></pre>
