---
layout: post
title:      "Javascript Oddities: Variables and Hoisting"
date:       2019-04-26 13:21:40 +0000
permalink:  javascript_oddities_variables_and_hoisting
---


Javascript is pretty weird.

You may have heard before that despite the name Javascript is very unlike Java. One of the biggest reasons for that is variables. In Java variables are much more strict; where they can be accessed, where they can be edited, what type of information they contain are all more strictly monitored. In Java and traditional Object Oriented Progamming in general, scope and privacy of information is one of the foundational principles. While you always could build Javascript like old Object Oriented languages, ES6 has gotten some upgrades to give the tools and readability to accomplish that more naturally.

With const and let you can now use variables like you were probably first trained; they are block scoped. any let or const variable declared within a block now cannot be accessed outside of the block, and cannot be redeclared within a block. The only difference is that a let variable can be reassigned, while a const cannot. This is in stark contrast to var and global scoped variables. They were the only previous option and they can be declared as  many times as you want. Their only difference (var, global variables) is that var is *function* scoped. this means that var variables are not accessible outside of the function in which it is declared. Global variables are true to their name and are accessible... globally. If the javascript is running the variable is accessible. No bueno.

If you can, avoid using global and var variables. Let and const are more reliable and behave more closely to what you will see in other programming languages. If it hasn't yet been declared within your scope, it is not yet a variable. This leads us into the other unique Javascript topic -- hoisting. Like declared functions, var and global variables are "hoisted" to the top of the highest scope available to them. That means global variables are initialized at the same time as the environment. And var variables are initialized at the same time as the function they are scoped to. Their assignment may come later on, but you can try to access their value before they have any. This can lead to all sorts of strange bugs and the dreaded "undefined" debugging value.

console.log("a")
var a = 2
console.log("a")

console: undefined
console: 2

Again, let and const are more reliable to work with. They are not hoisted and therefore declared on initialization. Were you to try to access them before they were declared you would find yourself an Uncaught ReferenceError, which is good! the more debugging information the better. Stick to declaring variables once, assigning them as necessary (unless const... because it's meant to be a constant...), and sticking them at the top of your scope on your own and you will have a minimum of problems. using let and const is always advised over var and global variables.

One last thing; most people as they are learning scope feel as though it's very restrictive, everything is so *private* all the time. That's not the purpose, it's about being as *specific* as possible about the information you are trying to define.

for let/const:
let a = 3
{let a = 4}

these a's are not the same variable, the first a is inherited by the block and then over-written by the blocks' *own* a. Rather than saying "oh we have the same 'a' variable", the block figured "you and I both have an 'a', but everytime I see 'a' I am referencing my version". If you put this into your console and then request a, it will return 3. One 'a' was declared outside the block and assigned to 3. Another was declared inside the block and assigned to 4 but is no longer accessible because the block is *gone*. But for var/globals:

var b = 2
{var b = 3}
b is the **same** variable. If you again put this into your console and request b you will be returned 3. How unspecific! Were you sticking to better naming conventions this wouldn't be any problem, but why deal with these issues if you don't have to? Go forth and be specific with ES6 conventions.
