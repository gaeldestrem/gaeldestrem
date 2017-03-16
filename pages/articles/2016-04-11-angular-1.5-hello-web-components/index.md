---
title: Angular 1.5 - Hello web components!
date: "2016-04-11"
layout: post
path: "/angular-1.5-hello-web-components"
category: "angular"
description: "Angular 1.5 is now out, what are components ? Why you should use them ?"
---

Angular 1.5 is now out, so what are components ? Why you should use them ?

<img src="https://i.giphy.com/3o6ZsSEFiJDoSdZSHm.gif" width="500" height="500"/>

## What are angular components ?

First things first: This method is just syntax sugar for the `.directive()` method you know (and hate if you're like me :D) 

Here's an example of a hello-world component:

`<hello-world name="World"></hello-world>`

Directive syntax :
```
angular.directive('helloWorld', function helloWorld () {
  return {
    restrict: 'E',
    scope: {},
    bindToController : {
      name : '@'
    },
    controller : function helloWorldCtrl () {
      this.hello = function () {
        console.log(this.name);
      }
    },
    controllerAs: 'helloCtrl',
    template: '<div><span ng-click="hw.logName()">Hello {{helloCtrl.name}}!</span></div>'
  }
});
```

Here's how you can write it now with components:

```
angular.component('helloWorld', {
  bindings: {
    name: '@'
  },
  controller : function helloWorldCtrl () {
    this.logName = function () {
      console.log(this.name);
    }
  },
  template : '<div><span ng-click="$ctrl.logName()">Hello {{$ctrl.name}}!</span></div>'
});
```


Things are simpler and more straightforward. 

## Why you should use them?

- Components have isolated scopes by default
- The bindToController option is on by default
- They use controllers instead of link functions
- They automatically use ControllerAs syntax
