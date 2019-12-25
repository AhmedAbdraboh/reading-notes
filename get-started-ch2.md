In JS, we should consider "function" to take the broader meaning of another related term: "procedure". 
A procedure is a collection of statements that can be invoked one or more times, may be provided some inputs, 
and may give back one or more outputs.

It's extremely important to note that in JS, functions are values that can be assigned (as shown in this snippet) 
and passed around. In fact, JS functions are a special type of the object value type. Not all languages treat 
functions as values, but it's essential for a language to support the Functional Programming pattern, as JS does.

But the === operator does have some nuance to it, a fact many JS developers gloss over, to their detriment. 
The === operator is designed to lie in two cases of special values: NaN and -0. Consider:

```
NaN === NaN;            // false
0 === -0;               // true
```

When making such comparisons, since the lying is likely bothersome, don't use ===. For NaN comparisons, 
use the Number.isNaN(..) utility, which does not lie. For -0 comparison, use the Object.is(..) utility, 
which also does not lie. Object.is(..) can also be used for non-lying NaN checks, if you prefer. 
Humorously, you could think of Object.is(..) as the "quadruple-equals" ====, the really-really-strict comparison!

JS does not define === as structural equality for object values. Instead, === uses identity equality for object values.

JS does not provide a mechanism for structural equality comparison of object values, only reference identity comparison. 
To do structural equality comparison, you'll need to implement the checks yourself.

The == operator performs an equality comparison similarly to how the === performs it. In fact, both operators consider 
the type of the values being compared. And if the comparison is between the same value type, both == and === do exactly 
the same thing, no difference whatsoever.

If the value types being compared are different, the == differs from === in that it allows coercion before the 
comparison. In other words, they both want to compare values of like types, but == allows type conversions first, 
and once the types have been converted to be the same on both sides, then == does the same thing as ===. Instead 
of "loose equality", the == operator should be described as "coercive equality".

There's no way to get these relational operators to avoid coercion, other than to just never use mismatched types 
in the comparisons. That's perhaps admirable as a goal, but it's still pretty likely you're going to run into a case 
where the types may differ.

```
var x = "10";
var y = "9";

x < y;      // true, watch out!
```

The wiser approach is not to avoid coercive comparisons, but to embrace and learn their ins and outs.


Two major patterns for organizing code (data and behavior) are used broadly across the JS ecosystem: classes and modules. 
These patterns are not mutually exclusive; many programs can and do use both. Other programs will stick with just one 
pattern, or even neither!

A class in a program is a definition of a "type" of custom data structure that includes both data and behaviors that 
operate on that data. Classes define how such a data structure works, but classes are not themselves concrete values. 
To get a concrete value that you can use in the program, a class must be instantiated (with the new keyword) one or
more times.

The module pattern has essentially the same goal as the class pattern, which is to group data and behavior together into 
logical units. Also like classes, modules can "include" or "access" the data and behaviors of other modules, for cooperation 
sake.

The key hallmarks of a classic module are an outer function (that runs at least once), which returns an "instance" of the 
module with one or more functions exposed that can operate on the module instance's internal (hidden) data.

Because a module of this form is just a function, and calling it produces an "instance" of the module, another description 
for these functions is "module factories".

The class form stores methods and data on an object instance, which must be accessed with the this. prefix. With modules, 
the methods and data are accessed as identifier variables in scope, without any this. prefix.

With class, the "API" of an instance is implicit in the class definition -- also, all data and methods are public. With 
the module factory function, you explicitly create and return an object with any publicly exposed methods, and any data 
or other unreferenced methods remain private inside the factory function.

There are other variations to this factory function form that are quite common across JS, even in 2019; you may run across 
these forms in different JS programs: AMD ("Asynchronous Module Definition"), UMD ("Universal Module Definition"), 
and CommonJS (classic Node.js style modules). The variations, however, are minor (yet not quite compatible). Still, all 
of these forms rely on the same basic principles.

ES modules (ESM), introduced to the JS language in ES6, are meant to serve much the same spirit and purpose as the existing 
classic modules just described, especially taking into account important variations and use-cases from AMD, UMD, and CommonJS.

The implementation approach does however differ significantly.

First, there's no wrapping function to define a module. The wrapping context is a file. ESMs are always file-based; one file, 
one module.

Second, you don't interact with a module's "API" explicitly, but rather use the export keyword to add a variable or method 
to its public API definition. If something is defined in a module but not exported, then it stays hidden (just as with classic 
modules).

Third, and maybe most noticeably different from previously discussed patterns, you don't "instantiate" an ES module, you just 
import it to use its single instance. ESMs are, in effect, "singletons", in that there's only one instance ever created, 
at first import in your program, and all other imports just receive a reference to that same single instance. If your module 
needs to support multiple instantiations, you have to provide a classic module style factory function on your ESM definition 
for that purpose.


