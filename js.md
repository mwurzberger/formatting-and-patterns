# Front End Coding and Formatting - JavaScript

 * [Namespacing](#namespacing)
 * [Whitespace](#whitespace)
 * [Beautiful Syntax](#spacing)
 * [Type Checking (Courtesy jQuery Core Style Guidelines)](#type)
 * [Conditional Evaluation](#cond)
 * [Naming](#naming)
 * [Native & Host Objects](#native)
 * [Comments](#comments)

------------------------------------------------

## Preface

The goal of this document is not to give rules that result in perfect code. It is so that with minimal effort the code will:
* Do what it is supposed to do
* Reduce the lead time required to understand an implementation
* Make it easier to establish what code can be reused
* Clarify how updates to an implementation should be styled or structured 

## Styles

1. <a name="namespacing">Namespacing</a>
  - All JavaScript should be wrapped in an object to prevent function name overlap and keep the code neat

  ```
  if (! com) { var com = {}; }
  if (! com.pageName) { com.pageName= {}; }

  com.pageName = {
    variableName: 'variableValue',
    functionName: function( param1 ) {
    }
  }
  ```    

  - Calls can be made directly by using the entire path

  ```
  com.pageName.functionName(param1);

  $(document).ready({  
    com.pageName.initialize();  
  });
  ```

2. <a name="whitespace">Whitespace</a>
  - Never mix spaces and tabs.
  - Use soft indents (spaces) instead of real tabs
  - For readability, set your editor's indent size to four characters

3. <a name="spacing">Beautiful Syntax</a>

    A. Parens, Braces, Linebreaks

    ```javascript
    // 3.A.1.1
    // Examples of really cramped syntax
    if(condition) doSomething();

    while(condition) iterating++;

    for(var i=0;i<100;i++) someIterativeFn();


    // 3.A.1.1
    // Use whitespace to promote readability
    if ( condition ) {
      // statements
    }

    while ( condition ) {
      // statements
    }

    for ( var i = 0; i < 100; i++ ) {
      // statements
    }

    var prop;
    for ( prop in object ) {
      // statements
    }

    if ( true ) {
      // statements
    } else {
      // statements
    }

    // 3.A.1.2
    // Ternery if/else statments allowed
    if ( value > 100 ) ? alert('Expensive') : alert('Cheap');
    ```

    B. Assignments, Declarations, Functions ( Named, Expression, Constructor )

    ```javascript

    // 3.B.1.1
    // Variables
    var foo = "bar",
        num = 1,
        undef;

    // Literal notations:
    var array = new Array(),
        object = new Object();

    // 3.B.1.2
    // Using only one `var` per scope (function) promotes readability
    // and keeps your declaration list free of clutter (also saves a few keystrokes)

    // Bad
    var foo = "";
    var bar = "";
    var qux;

    // Good
    var foo = "",
        bar = "",
        quux;

    // 3.B.1.3
    // var statements should always be in the beginning of their respective scope (function)
    function foo() {
      var bar = "",
          qux;

      // all statements after the variables declarations.
    }
    
    ```

    ```javascript
    
    // 3.B.2.1
    // Named Function Declaration
    function foo( arg1, argN ) {
      // statements
    }

    // Usage
    foo( arg1, argN );

    // 3.B.2.2
    // Named Function Declaration
    function square( number ) {
      return number * number;
    }

    // Usage
    square( 10 );

    // Really contrived continuation passing style
    function square( number, callback ) {
      callback( number * number );
    }

    square( 10, function( square ) {
      // callback statements
    });

    // 3.B.2.3
    // Function Expression
    var square = function( number ) {
      // Return something valuable and relevant
      return number * number;
    };

    // Function Expression with Identifier
    // This preferred form has the added value of being
    // able to call itself and have an identity in stack traces:
    var factorial = function factorial( number ) {
      if ( number < 2 ) {
        return 1;
      }

      return number * factorial( number - 1 );
    };

    // 3.B.2.4
    // Constructor Declaration
    function FooBar( options ) 
      this.options = options;
    }

    // Usage
    var fooBar = new FooBar({ a: "alpha" });
    fooBar.options;
    // { a: "alpha" }

    ```

    C. Exceptions, Slight Deviations

    ```javascript

    // 3.C.1.1
    // Functions with callbacks
    foo(function() {
      // Note there is no extra space between the first paren
      // of the executing function call and the word "function"
    });

    // Function accepting an array, no space
    foo([ "alpha", "beta" ]);

    // 3.C.1.2
    // Function accepting an object, no space
    foo({
      a: "alpha",
      b: "beta"
    });

    // Single argument string literal, no space
    foo("bar");

    // Inner grouping parens, no space
    if ( !("foo" in obj) ) {

    }

    ```

    D. Consistency Always Wins

    Whitespace rules for consistency. Lines can be separated by up to one line of white space but should never
    have more.

    ```javascript

    // 3.D.1.1

    if (condition) {
      // statements
    }

    while (condition) {
      // statements
    }

    for (var i = 0; i < 100; i++) {
      // statements
    }

    if (true) {
      // statements
    } else {
      // statements
    }

    ```

    E. Quotes

    Use single quotes for all strings. For complex jQuery selectors the single and double quotes can be reversed from the example.

    ```
    
    Bad: $(".testClass[href^='www.any.com']").show();

    Good: $('.testId[href^="www.any.com"]').show();
    
    ```

    F. End of Lines and Empty Lines

    Whitespace can ruin diffs and make changesets impossible to read. Consider incorporating a pre-commit hook that removes end-of-line whitespace and blanks spaces on empty lines automatically.  

4. <a name="type">Type Checking (Courtesy jQuery Core Style Guidelines)</a>

    A. Actual Types

    String:

        typeof variable === "string"

    Number:

        typeof variable === "number"

    Boolean:

        typeof variable === "boolean"

    Object:

        typeof variable === "object"

    Array:

        Array.isArray( arrayLikeObject )
        (wherever possible)

    Node:

        elem.nodeType === 1

    null:

        variable === null

    null or undefined:

        variable == null

    undefined:

    > Global Variables:
    ```
    >    typeof variable === "undefined"
    ```
    >  Local Variables:
    ```
    >    variable === undefined
    ```
    >  Properties:
    ```
    >    object.prop === undefined  
    >    object.hasOwnProperty( prop )  
    >    "prop" in object  
    ```
    
    B. Coerced Types

    Consider the implications of the following...

    Given this HTML:

    ```html
    <input type="text" id="foo-input" value="1">
    ```


    ```javascript

    // 4.B.1.1
    // `foo` has been declared with the value `0` and its type is `number`
    var foo = 0;

    // typeof foo;
    // "number"
    ...

    // Somewhere later in your code, you need to update `foo`
    // with a new value derived from an input element

    foo = document.getElementById("foo-input").value;

    // If you were to test `typeof foo` now, the result would be `string`
    // This means that if you had logic that tested `foo` like:

    if ( foo === 1 ) {
      importantTask();
    }

    // `importantTask()` would never be evaluated, even though `foo` has a value of "1"


    // 4.B.1.2
    // You can preempt issues by using smart coercion with unary + or - operators:

    foo = +document.getElementById("foo-input").value;
    //    ^ unary + operator will convert its right side operand to a number

    // typeof foo;
    // "number"

    if ( foo === 1 ) {
      importantTask();
    }

    // `importantTask()` will be called
    ```

    Here are some common cases along with coercions:


    ```javascript

    // 4.B.2.1

    var number = 1,
      string = "1",
      bool = false;

    number;
    // 1

    number + "";
    // "1"

    string;
    // "1"

    +string;
    // 1

    +string++;
    // 1

    string;
    // 2

    bool;
    // false

    +bool;
    // 0

    bool + "";
    // "false"
    ```


    ```javascript
    // 4.B.2.2

    var number = 1,
      string = "1",
      bool = true;

    string === number;
    // false

    string === number + "";
    // true

    +string === number;
    // true

    bool === number;
    // false

    +bool === number;
    // true

    bool === string;
    // false

    bool === !!string;
    // true
    ```

5. <a name="cond">Conditional Evaluation</a>

    ```javascript

    // 5.1.1
    // When only evaluating that an array has length,
    // instead of this:
    if ( array.length > 0 ) ...

    // ...evaluate truthiness, like this:
    if ( array.length ) ...


    // 5.1.2
    // When only evaluating that an array is empty,
    // instead of this:
    if ( array.length === 0 ) ...

    // ...evaluate truthiness, like this:
    if ( !array.length ) ...


    // 5.1.3
    // When only evaluating that a string is not empty,
    // instead of this:
    if ( string !== "" ) ...

    // ...evaluate truthiness, like this:
    if ( string ) ...


    // 5.1.4
    // When only evaluating that a string _is_ empty,
    // instead of this:
    if ( string === "" ) ...

    // ...evaluate falsy-ness, like this:
    if ( !string ) ...


    // 5.1.5
    // When only evaluating that a reference is true,
    // instead of this:
    if ( foo === true ) ...

    // ...evaluate like you mean it, take advantage of built in capabilities:
    if ( foo ) ...


    // 5.1.6
    // When evaluating that a reference is false,
    // instead of this:
    if ( foo === false ) ...

    // ...use negation to coerce a true evaluation
    if ( !foo ) ...

    // ...Be careful, this will also match: 0, "", null, undefined, NaN
    // If you _MUST_ test for a boolean false, then use
    if ( foo === false ) ...


    // 5.1.7
    // When only evaluating a ref that might be null or undefined, but NOT false, "" or 0,
    // instead of this:
    if ( foo === null || foo === undefined ) ...

    // ...take advantage of == type coercion, like this:
    if ( foo == null ) ...

    // Remember, using == will match a `null` to BOTH `null` and `undefined`
    // but not `false`, "" or 0
    null == undefined

    ```
    ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

    ```javascript

    // 5.2.1
    // Type coercion and evaluation notes

    // Prefer `===` over `==` (unless the case requires loose type evaluation)

    // === does not coerce type, which means that:

    "1" === 1;
    // false

    // == does coerce type, which means that:

    "1" == 1;
    // true


    // 5.2.2
    // Booleans, Truthies & Falsies

    // Booleans:
    true, false

    // Truthy:
    "foo", 1

    // Falsy:
    "", 0, null, undefined, NaN, void 0

    ```

6. <a name="naming">Naming</a>



    A. Use long descriptive names for varaibles. The compression will be handled during deployment.

    ```javascript

    // 6.A.3.1
    // Naming strings

    `dog` is a string


    // 6.A.3.2
    // Naming arrays

    `dogs` is an array of `dog` strings


    // 6.A.3.3
    // Naming functions, objects, instances, etc

    camelCase; function and var declarations


    // 6.A.3.4
    // Naming constructors, prototypes, etc.

    PascalCase; constructor function


    // 6.A.3.5
    // Naming regular expressions

    rDesc = //;


    // 6.A.3.6
    // From the Google Closure Library Style Guide

    functionNamesLikeThis;
    variableNamesLikeThis;
    ConstructorNamesLikeThis;
    EnumNamesLikeThis;
    methodNamesLikeThis;
    SYMBOLIC_CONSTANTS_LIKE_THIS;

    ```

7. <a name="comments">Comments</a>

    Comments are always preceded by a blank line. Comments start with a capital first letter, but don't require a period at the end, unless you're writing full sentences. There must be a single space between the comment token and the comment text; for multi-line comments a new line may be used in place of a space.

    ```
    // We need an explicit "bar", because later in the code foo is checked.
    var foo = "bar";
    ```

    ```
    /*
    Four score and seven-pause-minutes ago...
    */
    ```

    ```
    function foo( types, selector, data, fn, /* INTERNAL */ one ) {
        // Do stuff
    }
    ```

----------

Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/rwldrn/idiomatic.js" rel="dct:source">github.com/rwldrn/idiomatic.js</a>.
