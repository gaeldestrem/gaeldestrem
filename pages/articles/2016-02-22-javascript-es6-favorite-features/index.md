---
title: My 5 favorite features in Javascript ES6
date: "2016-02-22"
layout: post
path: "/javascript-es6-favorite-features"
category: "javascript"
description: "I'm now using ES6 since a few months at my work, and I have to say, I'm not going back ! So, what's so awesome ? Here are my five favorite features !"
---

I have now been using ES6 for a few months and I have to say I'm not going back ! What's so awesome ? Here are my five favorite features.

<img src="https://i.giphy.com/5GoVLqeAOo6PK.gif" width="500" height="500"/>

## Arrow function

The fat arrows are amazing because they make your *this* behave properly, i.e., this will have the same value as in the context of the function—it won’t mutate

Using arrows functions in ES6 allows us to stop using that = this or self = this or _this = this or .bind(this). For example, this code in ES5 is ugly:

<pre>
<code>
var self = this;

$('.btn').click(function(event) {
  self.onClick()
})
</code>
</pre>
This is the ES6 code without _this = this:

<pre>
<code>
$('.btn').click(event => {
  this.onClick()
})
</code>
</pre>

and you can also do cool inline things like this

<pre>
<code>
let objects = [1, 3, 5, 8, 11, 15, 17]
let filteredObjects = objects.filter(o => o < 10)
console.log(filteredObjects) // 1 3 5 8 
</code>
</pre>

## Template Literals (variable + multi-line)

Remember when we had to do ugly things like this ?

<pre>
<code>
var url = 'http://'+serverDomain+':'+port+'/api'
  
var text = 'Cumque pertinacius ut \n\t'  
 +  'doctus id Caesar libertatemque superbiam \n\t'
 +  'Illum veterem Stoicum qui ut mentiretur '   
</code>
</pre>

Now we can just use

<pre>
<code class="js hljs">
var url = `http://${serverDomain}:${port}/api`

var text = `Cumque pertinacius ut
doctus id Caesar libertatemque superbiam 
Illum veterem Stoicum qui ut mentiretur`

</code>
</pre>

## Promises

There were different promise libraries (Q, Bluebird, Deferred to name just a few). Now there's a standard Promise implementation in ES6

Promises are really useful when we have to chain async actions. 

<pre>
<code class="js hljs">
var itsGonnaBeLegendary = function () {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, 1000)
  })
 }

itsGonnaBeLegendary()
    .then(function() {
        console.log('Ater 1000 ms')
        return itsGonnaBeLegendary()
    })
    .then(function() {
        console.log('After 2000 ms!')
    });


console.log('hey')

// hey
// Ater 1000 ms
// After 2000 ms!
</pre>
</code>




## Default Parameters

We had to do things like this to declare default parameters

<pre>
<code class="js hljs">
var computeSomething = function (a, b) {
    var a = a || 50
    var b = b || 'red'
    ...
}
</code>
</pre>

And now we can just use default parameters :D
<pre>
<code class="js hljs">
var computeSomething = function (a = 50, b = 'red') {
    ...
}
</code>
</pre>

 
 ## Destructuring

We had to use this to retrieve data from a request

<pre>
<code>
var body = req.body // body has username and password
var username = body.username
var password = body.password  
</code>
</pre>

Now we can just use 

<pre>
<code>
var {username, password} = req.body
</code>
</pre>

## Conclusion

You can now use those ES6 features by using babel with gulp/webpack/grunt

<img src="https://i.giphy.com/12NUbkX6p4xOO4.gif" with="500" height="500"/>

And you know what ? There is still more ! :)

- ES6 Module
- Let/Const
- Enhanced Object Literals


