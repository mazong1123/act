---
layout: post
title: How to implement inheritance in react.js.
date: 2015-10-13 14:19
author: mazong1123
comments: true
categories: [Uncategorized]
published: false
---

[React.js](https://facebook.github.io/react/) is a great library to build view in component way. However, one thing makes me frustrated is
there's no inheritance support by using React.createClass() to create a react component. A "Class" cannot be inheritied! Facebook
now recommend us using [High order components](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750) to
address code reusable issue, which makes me more frustrated. OK, I'm an old school object oriented guy. I just want something in classic: Class inheritance and overriding.

That's why I developed [ReactOO](https://github.com/mazong1123/reactoo). By leveraging ReactOO, we can build react component in a classic
OO way. Following is an example to build a simple Button component:
```javascript
    window.ButtonClass = window.ReactOO.ReactBase.extend({
        getReactDisplayName: function () {
            return 'Button';
        },

        onReactRender: function (reactInstance) {
            var self = this;

            var text = reactInstance.props.text;

            return React.createElement('button', self.getButtonProperty(reactInstance), text);
        },

        getButtonProperty: function (reactInstance) {
            return {};
        }
    });
    
    var button = new window.ButtonClass();
    button.render({ text: 'Button' }, '#normalButton');
```
    
