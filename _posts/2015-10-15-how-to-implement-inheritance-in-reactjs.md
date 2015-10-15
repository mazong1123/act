---
layout: post
title: How to implement inheritance in react.js.
date: 2015-10-13 14:19
author: mazong1123
comments: true
categories: [Uncategorized]
published: true
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
Now everything looks more classic. At first, we defined a ButtonClass, which inherits from the base window.ReactOO.ReactBase class. Then we created an instance of ButtonClass and call its render() method to render itself to an element with 'normalButton' id.

You probably noticed the **getButtonPropery** method. It can be overrided in the subclass, and the Button property could be changed. Nothing new, just overriding in the OO way. Let's build a StyledButtonClass in this manner:

```javascript
    window.StyledButtonClass = window.ButtonClass.extend({
        getReactDisplayName: function () {
            return 'StyledButton';
        },

        getButtonProperty: function (reactInstance) {
            var self = this;
            var property = self._super();

            property.className = 'nice-button';

            return property;
        }
    });
    
    var styledButton = new window.StyledButtonClass();
    styledButton.render({ text: 'Styled Button' }, '#styledButton');
```
StyledButtonClass inherits from ButtonClass, overrides the **getButtonProperty** to add a **className** property. Done. Pretty simple huh?

How about add some interactions? Let's build a button with click handler and styled:
```javascript
    window.StyledButtonWithClickHandlerClass = window.StyledButtonClass.extend({
        getReactDisplayName: function () {
            return 'StyledButtonWithClickHandler';
        },

        getButtonProperty: function (reactInstance) {
            var self = this;
            var property = self._super();

            property.onClick = reactInstance.handleClick;

            return property;
        },

        onReactHandleClick: function (reactInstance, e) {
            e.preventDefault();

            alert('Clicked!');
        }
    });
    
    var styledButtonWithClickHandler = new window.StyledButtonWithClickHandlerClass();
    styledButtonWithClickHandler.render({ text: 'Styled Button With Click Handler' }, '#styledButtonWithClickHandler');
```
This time, we defined a class StyledButtonWithClickHandlerClass which inherits from StyledButtonClass, overrided **getButtonProperty** method to add an onClick property. And then overrided **onReactHandleClick** method to provide the click handler code. That's it. 

Please note for any [react life cycle methods](https://facebook.github.io/react/docs/component-specs.html) or javascript event handler (e.g: onClick, onSubmit), ReactOO provides built-in handler method in onReactxxx manner. A reactInstance can be used as a input parameter when you override these methods. [Please read the code sample and documentation for more details](https://github.com/mazong1123/reactoo).

Any bug or thoughts, please create an issue on [github](https://github.com/mazong1123/reactoo). Thanks :)
