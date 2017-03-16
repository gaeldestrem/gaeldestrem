---
title: Vue.js - The simplicity ! 
date: "2017-01-17"
layout: post
path: "/vuejs"
category: "javascript"
description: "This is like React but easier and faster to build stuff with. I’m using Vue.js since september and I’m still impressed by how everything feels natural and simple."
---

Vue.js is like React but easier and faster to build stuff with. I have been using Vue.js since september and I'm still impressed by how natural and simple everything feels.

I'm using it on my project (www.occaz.io) with server side rendering, routing, vue-x (redux-like) and everything looks simple and clean.
 
<img src="https://i.giphy.com/zcCGBRQshGdt6.gif" width="500" height="500"/>

What does the minimal implementation look like?

```
<!DOCTYPE html>
<html>
<head>
  <title>Vue hello world</title>
  <script src="https://vuejs.org/js/vue.min.js"></script>
</head>
<body>
  <div id="app">
    {{ message }}
  </div>

  <script>
    new Vue({
      el: '#app',
      data: {
        message: `Hello from Vue`
      }
    })
  </script>
</body>
</html>
```

And with webpack and vue-loader, it's even easier. Let's create an app !

```
#todoList.vue
<template>
  <div class="todo" v-for="todo in todos">
    {{ todo }}
  </div>
</template>

<script>
  export default {
    name: 'hello-world'
    props: ['todos'],
  }
</script>

<style>
  .hello {
    color: red
  }
</style>

# app.vue
...
<app>
  <todo-list :todos="['take a cofee', 'take a nap', 'code']"></todo-list>
</app>
```

Yes, basically you can just write html, css, js in a file and webpack will take care of everything else :D IMO React has a considerably steep learning curve



### Features :
- Virtual DOM
- Component oriented
- Component scoped css
- Light (30kb)
- Faster than react (<a href="https://vuejs.org/v2/guide/comparison.html#Performance-Profiles">source</a>)
 
### Scaling up:
- Server Side Rendering
- VueX (A Redux like store with mutations/actions)
- Vue-router
 
You can check out a great example here to see how easy the code is to understand : https://github.com/vuejs/vue-hackernews-2.0

 
