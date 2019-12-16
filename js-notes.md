## Reading Notes from You Don't Know Javascript Yet. 

Transpilation and polyfilling are two highly effective techniques for addressing that gap between code 
that uses the latest stable features in the language and the old environments a site or application needs 
to still support. Since JS isn't going to stop improving, the gap will never go away. Both techniques 
should be embraced as a standard part of every JS project's production chain going forward.

Step back and consider the entire flow of a JS source program:

1. After a program leaves a developer's editor, it gets transpiled by Babel, then packed by Webpack (and perhaps half a dozen other build processes), then it gets delivered in that very different form to a JS engine.

2. The JS engine parses the code to an AST(Abstract Syntax Tree).

3. Then the engine converts that AST to a kind-of byte code, a binary intermediate representation (IR), which is then refined/converted even further by the optimizing JIT compiler.

4. Finally, the JS VM executes the program.

I think it's clear that in spirit, if not in practice, **JS is a compiled language.**

Why strict mode? Strict mode shouldn't be thought of as a restriction on what you can't do, but rather as a guide to the best way to do things so that the JS engine has the best chance of optimizing and efficiently running the code. Most JS code is worked on by teams of developers, so the strict-ness of strict mode (along with tooling like linters!) often helps collaboration on code by avoiding some of the more problematic mistakes that slip by in non-strict mode.

