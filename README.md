# Pragmatic.js code style guidelines

## TL;DR

### General coding:
* Use long, descriptive variable and method names
* Use blank lines to separate "paragraphs" of code for readability
* Use comments to describe non-obvious code behavior
* Don't write comments that do not add to code understanding
* Optimize for performance only if there's a measurable problem
* If a source file is longer than 200 LoC, it's time to split it up

### Functions:
* Use one var statement per function, at the top
* `function name() { }` for named functions
* `function(){ }` for anonymous functions
* Don't use more than 10 LoC per method (except for closures)

### Statements & expressions:
* Use short and concise expressions
* Use duck-typing and rely on unit tests rather than testing for types of arguments
* Prefer functional programming over `for` and `while` loops, unless performance is a concern (see above)
* No curly braces for single-line control flow statements such as `if` & friends, but always include braces if you split it into two lines, even if there's only one statement in the block
* Always use semicolons where the spec says a semicolon *could* be put. Optional 
semi-colon coding increases the chance you will make a mistake, and places a higher burden on your fellow maintainers.
* Which means you don't need to put a single semicolon _before_ statements that start with `(` or `[` as the previous line ended with one
* Use ternary when it is simple enough as to not make code difficult to understand
* Do not use `try` and `catch` unless absolutely required (like an API forcing you to do so)

## Pragmatic JavaScript

The word pragmatic means _"Practical, concerned with making decisions 
and actions that are useful in practice, not just theory."[1]_ Writing pragmatic
JavaScript is all about optimizing the process of writing JavaScript for you 
as a programmer, using all the facilities the language provides. 

Writing less code is good; ~~emphasized by the no optional semicolons rule, by 
no curly braces where not necessary and~~ by using functional programming constructs
whereever possible.

At the same time, when you come back to your code later, you want to understand it—
thus long, descriptive variable and method names, and comments where necessary.

JavaScript is a modern, flexible and malleable scripting language, and it deserves
to be treated as such. Pragmatic.js is also about discovering and learning the language
strengths as well as its quirks so you can make full use of it.

### Examples

Here are some examples from [Zepto.js][zepto].

```javascript
// typical helper function
function eachEvent(events, fn, iterator){
  if ($.isObject(events)) $.each(events, iterator)
  else events.split(/\s/).forEach(function(type){ iterator(type, fn) })
}

// shortcut methods for `.bind(event, fn)` for each event type
;('focusin focusout load resize scroll unload click dblclick '+
'mousedown mouseup mousemove mouseover mouseout '+
'change select keydown keypress keyup error').split(' ').forEach(function(event) {
  $.fn[event] = function(callback){ return this.bind(event, callback) }
})

// from Zepto core, $.fn.siblings implementation
function filtered(nodes, selector) {
  return selector === undefined ? $(nodes) : $(nodes).filter(selector)
}

$.fn.siblings = function(selector){
  return filtered(this.map(function(i, el){
    return slice.call(el.parentNode.children).filter(function(child){ return child!==el })
  }), selector)
}
```

### Contribute

I welcome contributions—this guide is very basic at the moment and should probably have some more
guidelines for specific situations and how to get started. You know where the fork & pull request
buttons are.

### License

Pragmatic.js is licensed under the terms of the MIT License.

  [1]: http://en.wiktionary.org/wiki/pragmatic
  [optional]: http://mislav.uniqpath.com/2010/05/semicolons/
  [zepto]: http://zeptojs.com/


From Slifty:
------------

### Conventions
Chain whenever possible

In situations where order is functionally irrelevant, lists of things should be sorted alphabetically. This means classes, constants, lists of lists (e.g. this sentence), switch statements, variable declarations, etc.

Variable names are camelCase. This includes acronyms -- "ID" is "Id" and "URL" is "Url"

An attribute can only be called "id" if it is the id of that object. If it refers to the id of another object it should be "[objectType]Id" e.g. "gameId" or "playerId"

For the sake of simplicity, function and class names concerning communication are always from the perspective of the server, even in client code. "In" means the message is going from client->server ("into" the server). "Out" means the message is going server->client ("out" of the server).