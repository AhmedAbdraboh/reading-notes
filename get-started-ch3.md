
## Iterator 

The iterator pattern defines a data structure called an "iterator" that has a reference to an underlying data source 
(like the query result rows), which exposes a method like next(). Calling next() returns the next piece of data (ie, 
a "record" or "row" from a database query).

You don't always know how many pieces of data that you will need to iterate through, so the pattern typically indicates 
completion by some special value or exception once you iterate through the entire set and go past the end.

The importance of the iterator pattern is in adhering to a standard way of processing data iteratively, which creates 
cleaner and easier to understand code, as opposed to having every data structure/source define its own custom way of 
handling its data.

ES6 standardized a specific protocol for the iterator pattern directly in the language. The protocol defines a next() 
method whose return is an object called an iterator result; the object has value and done properties, where done is a 
boolean that is false until the iteration over the underlying data source is complete.

### Consuming Iterators

With the ES6 iteration protocol in place, it's workable to consume a data source one value at a time, checking after 
each next() call for done to be true to stop the iteration. But this approach is rather manual, so ES6 also included 
several mechanisms (syntax and APIs) for standardized consumption of these iterators.

One such mechanism is the for..of loop.
Another mechanism that's often used for consuming iterators is the ... operator. This operator actually has two symmetrical 
forms: spread and rest (or gather, as I prefer). The spread form is an iterator-consumer.

To spread an iterator, you have to have something to spread it into. There are two possibilities in JS: an array or an 
argument list for a function call.

An array spread:
```
// spread an iterator into an array,
// with each iterated value occupying
// an array element position.
var vals = [ ...it ];
```
A function call spread:
```
// spread an iterator into a function,
// call with each iterated value
// occupying an argument position.
doSomethingUseful( ...it );
```

## Iterables

The iterator-consumption protocol is technically defined for consuming iterables; an iterable is a value that can be iterated 
over.

The protocol automatically creates an iterator instance from an iterable, and consumes just that iterator instance to its 
completion. This means a single iterable could be consumed more than once; each time, a new iterator instance would be 
created and used.

ES6 defined the basic data structure/collection types in JS as iterables. This includes strings, arrays, maps, sets, and others.

A Map data structure uses objects as keys, associating a value (of any type) with that object. Maps have a different default
iteration than seen above, in that the iteration is not just over the map's values but instead its entries -- an entry is a
tuple (2-element array) including both a key and a value.

For the most part, all built-in iterables in JS have three iterator forms available: keys-only (keys()), values-only 
(values()), and entries (entries()).

## Closure

Closure is the ability of a function to remember and continue to access variables defined outside its scope, even when that 
function is executed in a different scope.







