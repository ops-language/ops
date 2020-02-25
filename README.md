# OPS LANGUAGE

## Types
Type        | Description
---         | ---
`N`         | 64 bit unsigned integer
`Z`         | 64 bit signed integer
`Integer`   | extensible signed integer (32-bit minimum)
`Q`         | floating point number storead as a fraction (Z / Z)
`R`         | 64 bit floating point number
`Bool`      | boolean value, stored in the boolean stack (1bit)
`Byte`      | 8-bit unsigned integer
`(A, B, C)` | tuple of type A, B and C
`{A}`       | set of type A
`A -> B`    | function from A to B

## Keywords
Identifier   | Description
---          | ---
`infer`      | imports a module (by copying the tokens)
`exfer`      | for functions and variables, doesn't mangle and builds a simple c function that requires all the parameters them (in front of declarations)
`externum`   | declares existance of a function/varibale extern to the program (in front of declarations)
`datum`      | declares a new data

## Operators
Operator | Description
---      | ---
`::`     | module/type access
`()`     | function call
`[]`     | set access (usage: id[expr])
`^`      | power
`*`      | multiply
`/`      | divide
`%`      | modulo
`+`      | add
`-`      | subtract
`.`      | function concatenation
`:`      | cast
`=`      | equals
`~=`     | almost equals (tries to convert rhs to the same type of lhs before comparing)
`/=`     |  not equals
`<`      | less
`>`      | greater
`<=`     | less or equals
`>=`     | greater or equals
`non`    | not
`aut`    | xor
`vel`    | or
`et`     | and
`\|\|`   | haskell's where (usage: `expr \|\| assignlike, assignlike`)
`\|>`    | pass to (takes the result of the expression and feeds it to the rhs)

## Expressions
* closure
    * `(x, y, z) -> x + y + z`
    * `(x, y) -> { match1, match2, match3, ... }`
    * **a generic case expression is always needed**

* match:
    * `pattern match | expression => expression;`
    * `(a, b)                  => a + b`
    * `(a, b) | a > 0 et b < 0 => b - a`
    * `(2, 3)                  => 8`
    * `(_, _)                  => 10`

* function call:
    * `f(1, 2+3)`
    * **if not all the arguments are given a closure is returned**
    
* set comprehension:
    * `{expr, expr, expr, ...}`
    * `{expr .. expr}`
    * `{expr | id <- expr, expr}`


## Statements
* import: `infer folder::folder::file;`
* expression (only in main)
* declaration: `id : typeid;`
* assignement: `id := expr;`
* main: `potissima { externfunc(expr1); externfunc2(expr2); };`

## Design
* strong type system:
    * types inferred from expressions, function bodies, or function calls
* lazy evaluation

## Building
* config file (build.toml)
    * name
    * version
    * target
    * libraries
        * github link/path
