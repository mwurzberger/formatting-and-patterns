# Front End Coding and Formatting - JavaScript

 * [Namespacing](#namespacing)
 * [Naming Conventions](#namingconventions)
 * [Whitespace](#whitespace)
 * [Beautiful Syntax](#spacing)
 * [Type Checking (Courtesy jQuery Core Style Guidelines)](#type)
 * [Conditional Evaluation](#cond)
 * [Comments](#comments)

------------------------------------------------

## Preface

The goal of this document is not to give rules that result in perfect code. It is so that with minimal effort the code will:
* Do what it is supposed to do
* Reduce the lead time required to understand an implementation
* Make it easier to establish what code can be reused
* Clarify how updates to an implementation should be styled or structured 

## Styles

<a name="namespacing">Namespacing</a>
  - All JavaScript should be wrapped in an object to prevent function name overlap and keep the code neat  
  ```
  if (! com) { var com = {}; }
  if (! com.pageName) { com.pageName= {}; }

  com.pageName = {
    variableName: 'variableValue',
    functionName: function( param1 ) {
    }
  }

  com.pageName = function() {
      var functionName = function () {
      }

      var oPublic = {
          functionName: functionName
      };

      return oPublic;
  }
  ```    

  - Calls can be made directly by using the entire path  
  ```
  com.pageName.functionName(param1);
  ```

<a name="namingconventions">Naming Conventions</a>
    - Naming functions, objects, instances, etc  
    ```
    camelCase; // function and var declarations
    functionNamesLikeThis;
    variableNamesLikeThis;
    methodNamesLikeThis;

    ```

    - Naming constructors, prototypes, etc  
    ```
    PascalCase; // constructor function
    ConstructorNamesLikeThis;
    EnumNamesLikeThis;
    ```

    - Naming Symbolic Constants using ALL_CAP_UNDERSCORED  
    ```
    SYMBOLIC_CONSTANTS_LIKE_THIS
    ```

    - No Abbreviations, use longer descriptive names  
    ```javascript
    // Good
    var deliveryNote = 1; 

    // Bad
    var delNote = 1; 
    ```

    - Collection names should match their contents  
    ```
    'dog' is a string
    'dogs' is an array 
    ```

    - Prefixes for metadata. Certain prefixes let the reader know details about the variable or function 
    ```javascript
    // jQuery objects should be prefixed with $
    var $curTarget = $(event.currentTarget);

    // Regular Expressions prefixed with r
    var rEmailer = //;

    // Private methods are prefixed with _
    com.pageName = function() {
      var publicFunction = function () {
        _privateFunction();
      }

      var _privateFunction = function () {
      }

      var oPublic = {
          publicFunction: publicFunction
      };

      return oPublic;
    }
    ```    

<a name="whitespace">Whitespace</a>
  - Use 4 space indentation
  - Never mix spaces and tabs
  - No trailing whitespace on any line
  - No more than one blank line separating any other command
  - There should be no spaces between the function name and the first ```(```
  - There should be a space after open parens and before close parens ```function( param1, param2 )```
  - One space should be added following commas and colons ```{param1: "Hello", param2: "World"}```

<a name="spacing">Beautiful Syntax</a> 
  - Parens, Braces, Linebreaks  
  ```javascript
  // Open braces on same line as the previous statement
  // Close braces on the same indent as the original function call
  function func() {
    return {
      "name": "Batman"
    }; 
  }

  // Readability Examples
  while( condition ) {
    // statements
  }

  if( true ) {
    // statements
  } else {
    // statements
  }

  // Ternery if/else statments allowed
  if( value > 100 ) ? alert('Expensive') : alert('Cheap');
  ```

  - Assignments, Declarations, Functions ( Named, Expression, Constructor )
  ```javascript
  // Using only one `var` per scope (function) promotes readability
  // and keeps your declaration list free of clutter 
  var foo = "",
      bar = "",
      quux;

  // Literal notations:
  var array = new Array(),
      object = new Object();

  // var statements should always be in the beginning of their respective scope (function)
  function foo() {
    var bar = "",
        qux;
    // statements
  }

  - Callbacks can be passed in one of two ways
  // Inline
  $( "#target" ).click( function() {
    // statements
  });

  // By Reference
  $( "#target" ).click( functionName );

  // Constructor Declaration
  function FooBar( options ) 
    this.options = options;
  }

  // Usage
  var fooBar = new FooBar({ a: "alpha" });
  fooBar.options;
  ```

  - Use single quotes for all strings. For complex jQuery selectors the single and double quotes can be reversed from the examples on the jQuery website.  
  ```javascript
  $('.testId[href^="www.any.com"]').show(); // Good
  var word = "word"; // Bad
  ```

<a name="type">Type Checking (Courtesy jQuery Core Style Guidelines)</a>
  - Actual Types
    String: ```typeof variable === "string"```
    Number: ```typeof variable === "number"```
    Boolean: ```typeof variable === "boolean"```
    Object: ```typeof variable === "object"```
    Array: ```Array.isArray( arrayLikeObject )```
    Node: ```elem.nodeType === 1```
    null: ```variable === null```
    null or undefined: ```variable == null```

    undefined:
    > Global Variables: ```typeof variable === "undefined"```
    >  Local Variables: ```variable === undefined```
    >  Properties:
    ```javascript
    >    object.prop === undefined  
    >    object.hasOwnProperty( prop )  
    >    "prop" in object  
    ```
    
  - Coerced Types
    Consider the implications of the following...
    Given this HTML: ```html <input type="text" id="foo-input" value="1">```

    ```javascript
    // `foo` has been declared with the value `0` and its type is `number`
    var foo = 0;

    // typeof foo;
    // "number"
    

    // Somewhere later in your code, you need to update `foo`
    // with a new value derived from an input element

    foo = document.getElementById("foo-input").value;

    // If you were to test `typeof foo` now, the result would be `string`
    // This means that if you had logic that tested `foo` like:

    if ( foo === 1 ) {
      importantTask();
    }

    // `importantTask()` would never be evaluated, even though `foo` has a value of "1"

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

<a name="cond">Conditional Evaluation</a>
  - It is almost always better to use the === and !== operators. The == and != operators do type coercion. In particular, do not use == to compare against falsy values.
  ```javascript

  // When only evaluating that an array has length,
  // instead of this:
  if ( array.length > 0 ) ...

  // ...evaluate truthiness, like this:
  if ( array.length ) ...


  // When only evaluating that an array is empty,
  // instead of this:
  if ( array.length === 0 ) ...

  // ...evaluate truthiness, like this:
  if ( !array.length ) ...


  // When only evaluating that a string is not empty,
  // instead of this:
  if ( string !== "" ) ...

  // ...evaluate truthiness, like this:
  if ( string ) ...


  // When only evaluating that a string _is_ empty,
  // instead of this:
  if ( string === "" ) ...

  // ...evaluate falsy-ness, like this:
  if ( !string ) ...


  // When only evaluating that a reference is true,
  // instead of this:
  if ( foo === true ) ...

  // ...evaluate like you mean it, take advantage of built in capabilities:
  if ( foo ) ...


  // When evaluating that a reference is false,
  // instead of this:
  if ( foo === false ) ...

  // ...use negation to coerce a true evaluation
  if ( !foo ) ...

  // ...Be careful, this will also match: 0, "", null, undefined, NaN
  // If you _MUST_ test for a boolean false, then use
  if ( foo === false ) ...


  // When only evaluating a ref that might be null or undefined, but NOT false, "" or 0,
  // instead of this:
  if ( foo === null || foo === undefined ) ...

  // ...take advantage of == type coercion, like this:
  if ( foo == null ) ...

  // Remember, using == will match a `null` to BOTH `null` and `undefined`
  // but not `false`, "" or 0
  null == undefined

  ```
  - ALWAYS evaluate for the best, most accurate result - the above is a guideline, not a dogma.

  ```javascript

  // Type coercion and evaluation notes

  // Prefer `===` over `==` (unless the case requires loose type evaluation)

  // === does not coerce type, which means that:

  "1" === 1;
  // false

  // == does coerce type, which means that:

  "1" == 1;
  // true


  // Booleans, Truthies & Falsies

  // Booleans:
  true, false

  // Truthy:
  "foo", 1

  // Falsy:
  "", 0, null, undefined, NaN, void 0
  ```


<a name="comments">Comments</a>
  - Comments are always preceded by a blank line. Comments start with a capital first letter, but don't require a period at the end, unless you're writing full sentences. There must be a single space between the comment token and the comment text; for multi-line comments a new line may be used in place of a space.

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

  Commenting for documentation should be done using the YUIDoc style. Documentation of the style http://yui.github.io/yuidoc/
  ```javascript
  /**
   * Reverse a string
   *
   * @param  {String} input_string String to reverse
   * @return {String} The reversed string
   */
  function reverse(input_string) {
    // ...
    return output_string;
  };
  ```

----------

Based on a loosely on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/rwldrn/idiomatic.js" rel="dct:source">github.com/rwldrn/idiomatic.js</a>.
