# Bocoup Roost

## Day 1 - 2012.12.03

### Dan Heberden

[@danheberden](http://twitter.com/danheberden)

#### HTML5

* Basic markup
* void elements (`area`, `base`, etc.)
* Raw text
* Comments
* Normal elements
* Simpler DOCTYPE
* What else is new?
  * You know this already
	* new semantic elements
	* relaxed markup (not strict XML)
* Don't forget about these for checking for support:
	* html5readiness.com
	* caniuse.com
* For older browsers & support checking:
	* shims/shivs
	* Modernizr
	* polyfills
* Forms 
	* validation w/ new input types
		* `required`
		* `pattern`
		* `min` & `max`
* Data attributes
	* used to append info to an element in the DOM
	* `data-*`, e.g., `data-nickname="Bob"`
	* Accessed like so:
		* Raw JS:
	
			element.getAttribute('data-nickname');
			
		* jQuery:
	
			$("#person").data("nickname");
* `video` is awesome
    * Easy fallback support
    * Full scriptable
        * Check out [PopcornJS](http://popcornjs.org/)
* Both `video` and `audio` support multiple sources for compatibility (e.g., browser support for various codecs)
* `canvas` element
    * JS lets you draw various things within the element
* GeoLocation API
* Web Storage API
    * Better than cookies, persistant across pageloads
    * Very easy, uses the `localStorage.getItem()` & `localStorage.setItem()` for basic usage
* Web Sockets
    * instant client/server communication
        * "Push" data
    * **Socket.IO** is a good library for this
* Feature detection 
    * see Modernizr
    * better than browser detection by far
* Polyfills
    * yepnope.js is good for conditionally applying polyfills
* File API
    * allows for much better handling of files being input into the browser
    * Drag & drop of files
    * Output markup about what the file object consists of
        * File type
        * Last modified
        * Size
* SVG
    * vector graphics format
    * can be animated
    * Support is all over the map
    
#### CSS3

##### More review

* pseudo-element selectors
    * `nth-child` selector
        * Starts from zero, like other programming languages
    * `:first-child`
    * `:last-child`
    * etc.
* CSS specificity
    * `1000 pts.` – inline style
    * ` 100 pts.` –  #id
    * `  10 pts.` – .class [attribute] :pseudo-class
    * `   1 pt.` – element :before :after
* Media Queries
    * screen & print styles
    * Work in `link` elements and inside stylesheets
    * Lots more queries
        * `min-width`
        * `max-device-width`
        * etc.
    * Used to target mobile devices, high density displays, etc.
* Box model
    * joy. know it. love it. hate it.
    * Or, use `box-sizing: border-box` to use the IE-style box model
        * Means `width` includes padding and border, rather than adding to the box size
        
##### New stuff

* `text-shadow`
* `box-shadow`
* `border-radius`
* background gradients
    * don't forget about [CSS3please.com](http://css3please.com)
* Web fonts
    * file format is all over the place
* Flexbox
    * New layout method
    * Still being finalized
    * Allows for table-like layouts, fluid columns, etc.
* Transforms
    * rotations, etc.
    * Can be 3D
* Transitions
    * Animation of CSS properties
    * Most useful for `color`, `border-width`, `text-shadow`, etc. on links
    * Can also be used for transforms to get basic animations w/o JS
* Keyframes
    * Used to mark specific stages of an animation
    
        .keyframes1 {
            -webkit-animation: colorflash 5s infinite linear;
        }
        
    * Fourth argument is a timing function (e.g., `ease-in`, `ease-out`, etc.)
* Tying in to JS
    * Transitions have a JS event for when the transition finishes

### Ben Alman

[@cowboy](http://twitter.com/cowboy)

#### JS Basics

Best basic JS docs are at the [MDN](http://mdn.mozilla.org)

##### Raw gist content:

Copying in this gist content: https://gist.github.com/08e517bb19abcf3d0cf5#file_javascript_fundamentals.js

    //////////////////////////
    // JavaScript Fundamentals
    //////////////////////////



    ////////////
    // Variables
    ////////////

    // JavaScript (the language AND the name) is case sensitive.
    var foo = 1;
    var FOO = 2;
    foo // 1
    FOO // 2

    // Variable values are initialized to `undefined` by default.
    var foo;
    foo // undefined

    // But a value can be assigned at the time the variable is declared.
    var bar = 1;
    bar // 1

    // It's possible to set a global variable without using a `var` statement,
    // but it's considered bad practice.
    abc = 123;
    abc // 123


    // Variables are "scoped" (or local) to the function they're declared in,
    // or, for variables declared outside any function, to the "global" scope.
    var foo = 123;
    function test() {
      var foo = 456;
    }
    foo // 123
    test();
    foo // 123

    // If the `var` statement is omitted, a local variable is NOT created.
    var bar = 123;
    function test2() {
      bar = 456;
    }
    bar // 123
    test2();
    bar // 456



    // These are all valid variable names:

    var foo, foo123;  // Identifiers can contain numbers, but can't start with one.
    var foo_bar;      // Underscores aren't idiomatic JavaScript...
    var fooBar;       // ...but camelCased names are.
    var FooBar;       // Initial caps are used for constructor functions.
    var $foo;         // $ is (supposed to be) reserved for machine-generated names.
    var _foo;         // By convention, leading-underscore indicates "private."
    var __foo__;      // Double-underscore is usually reserved for internals.



    // You can declare multiple variables in a single `var` statement, using a
    // comma to separate them.
    var a = 1, b = 2, c = 3;

    // Although it can be more legible (and safer) to do this:
    var a = 1;
    var b = 2;
    var c = 3;

    // Why safer? Imagine you formatted your var declarations like this (this is
    // a popular format people use) but forgot a comma after one of the lines:
    var a = 1,
        b = 2   // <-- missing comma!
        c = 3;

    // JavaScript automatically inserts a semicolon after the second line,
    // setting a *global* variable c to 3. Whoops!
    var a = 1,
        b = 2;
    c = 3;



    ///////////////////
    // Global variables
    ///////////////////

    // In browser JavaScript, the global object can be accessed via "window".
    // All global variables are also accessible as properties of that object.
    var foo = 123;
    function test() {
      bar = 456;
    }
    test();
    foo // 123
    bar // 456
    window.foo // 123
    window.bar // 456






    ////////////
    // Functions
    ////////////

    // "function" declares code to be run at a future time. The code inside
    // will not run until you explicitly tell it to, by putting () parens after
    // its name.

    // This syntax is also sometimes called a "function declaration" or
    // "function statement."
    function addTwoNumbers(a, b) {
      return a + b;
    }
    addTwoNumbers(1, 2) // 3

    // "return" specifies the value to be returned by a function. If no value is
    // explicitly returned, the function returns `undefined`.
    function doNothing() {
      /* nothing */
    }
    doNothing() // undefined

    // Functions can also be defined using the "function expression" syntax.
    var addTwoNumbers = function(a, b) {
      return a + b;
    };
    addTwoNumbers(1, 2) // 3

    // Function expressions are often specified as arguments to other functions.
    ["zero", "one", "two"].forEach(function(item, index) {
      console.log(item, index);
    });
    // "zero" 0
    // "one" 1
    // "two" 2



    // This code is repetitive, and thus harder to maintain.
    function prettyName(first, last) {
      var capitalizedFirst = first.charAt(0).toUpperCase() + first.substring(1).toLowerCase();
      var capitalizedLast = last.charAt(0).toUpperCase() + last.substring(1).toLowerCase();
      return capitalizedFirst + " " + capitalizedLast;
    }
    prettyName("bENjamIN", "alMan") // "Benjamin Alman"



    // Creating a function allows us to reuse code and avoid repetition.
    function capitalize(str) {
      return str.charAt(0).toUpperCase() + str.substring(1).toLowerCase();
    }
    capitalize("bENjamIN") // "Benjamin"

    function prettyName(first, last) {
      return capitalize(first) + " " + capitalize(last);
    }
    prettyName("bENjamIN", "alMan") // "Benjamin Alman"



    // Like variables, functions declared inside other functions are local
    // to the outer function. Additionally, they can access any other functions
    // and variables declared within the outer function.
    function prettyName(first, last) {
      function capitalize(str) {
        return str.charAt(0).toUpperCase() + str.substring(1).toLowerCase();
      }
      return capitalize(first) + " " + capitalize(last);
    }
    prettyName("bENjamIN", "alMan") // "Benjamin Alman"
    capitalize // ReferenceError: capitalize is not defined






    /////////////////////
    // Function arguments
    /////////////////////

    // JavaScript initializes any argument whose value has been omitted to
    // `undefined` and ignores any extra arguments for which a named argument
    // has not been specified.
    function test(a, b, c) {
      return [a, b, c];
    }

    test()              // [undefined, undefined, undefined]
    test(1, 2)          // [1, 2, undefined]
    test(1, 2, 3, 4, 5) // [1, 2, 3]

    // The `arguments` object is an array-like object inside of every function that
    // has some useful properties. It's not accessible outside of a function.

    // Iterate over all arguments using the .length property and [idx].
    function logEachArgument(a, b, c) {
      for (var i = 0; i < arguments.length; i++) {
        console.log(arguments[i]);
      }
    }
    logEachArgument(1, 2, 3, 4, 5);
    // logs: 1 2 3 4 5


    // You can look at arguments.length to determine the number of arguments
    // that were specified when the function was invoked.
    var _value;
    function getOrSet(value) {
      if (arguments.length === 0) {
        return _value;
      } else {
        _value = value;
      }
    }






    /////////////////////////////////////////////
    // Variable and function declaration hoisting
    /////////////////////////////////////////////

    // Variable hoisting.
    var foo = 1;
    function bar() {
      if (!foo) {
        var foo = 10;
      }
      return foo;
    }

    bar() // What does this return?

    // What's really happening:
    var foo = 1;
    function bar() {
      var foo; // Variable declarations (not assignments) are hoisted!
      if (!foo) {
        foo = 10;
      }
      return foo;
    }

    bar() // 10



    // Function declaration hoisting.
    var foo = 1;
    function bar() {
      foo = 10;
      return;
      function foo() {}
    }

    bar();
    foo // What is this value?

    // What's really happening:
    var foo = 1;
    function bar() {
      function foo() {} // Function declarations are hoisted!
      foo = 10;
      return;
    }

    bar();
    foo // 1



    // Where does function declaration hoisting matter?
    function whoops(state) {
      if (state) {
        function getValue() {
          return "you expect this";
        }
      } else {
        function getValue() {
          return "you get this, no matter what";
        }
      }
      return getValue();
    }
    whoops(false) // "you get this, no matter what"
    whoops(true) // "you get this, no matter what"

    // This is what's really happening:
    function whoops(state) {
      // Both function declarations get hoisted...
      function getValue() {
        return "you expect this";
      }
      // And the latter overrides the former.
      function getValue() {
        return "you get this, no matter what";
      }
      // This if-else does nothing.
      if (state) {
      } else {
      }
      // The wrong value is returned.
      return getValue();
    }

    // How do we fix this? Don't use function declaration inside blocks! Use
    // function expressions instead!
    function fixed(state) {
      var getValue;
      if (state) {
        getValue = function() {
          return "state was truthy";
        };
      } else {
        getValue = function() {
          return "state was falsy";
        };
      }
      return getValue();
    }
    fixed(false) // "state was falsy"
    fixed(true) // "state was truthy"






    //////////////////
    // Primitive Types
    //////////////////

    // There are five primitive types: undefined, null, boolean, string, number.
    // Everything else is an object. Note that when using `new` with a constructor
    // function, an object (not a primitive) will always be returned.

    typeof true                       // "boolean"
    typeof new Boolean(true)          // "object"

    typeof 9000                       // "number"
    typeof new Number(9000)           // "object"

    typeof "hello world"              // "string"
    typeof new String("hello world")  // "object"



    ///////////
    // Booleans
    ///////////

    true  // true
    false // false

    true !== false  // true
    true === !false // true

    if (true) { /* this code will execute */ }
    if (!false) { /* this code will execute */ }



    //////////
    // Strings
    //////////

    // These are all valid strings.
    'foo'
    "bar"
    '\u0041'
    "this is on the first line\nand this the second"

    // This is not.
    "hello
    world" // SyntaxError: Unexpected token ILLEGAL

    // The backslash character is used in strings as an escape character.
    "foo\nbar"  // foo<linebreak>bar
    "foo\tbar"  // foo<tab>bar
    "foo\"bar"  // foo"bar
    "foo\\bar"  // foo\bar

    // Strings have lengths.
    "testing".length // 7

    // And methods.
    "Hello World".indexOf("W")  // 6
    "Hello World".toLowerCase() // "hello world"
    "Hello World".split(" ")    // ["Hello", "World"]
    "Hello World".charAt(0)     // "H"
    "Hello World".substring(6)  // "World"

    // Strings aren't mutable.
    var test = "Hello World";
    test.toLowerCase() // "hello world"
    test // "Hello World"

    // But you can override values in variables by re-setting them.
    test = test + "? " + "Hello World".toUpperCase() + "!";
    test // "Hello World? HELLO WORLD!"



    //////////
    // Numbers
    //////////

    // In Javascript, there's only one type of number, and it's a 64-bit float.

    // These are all the same number.
    1234
    1234.0
    1.234e3

    // Beware of rounding issues when doing math.
    0.1 + 0.2       // 0.30000000000000004
    0.01 + 0.02     // 0.03
    0.0001 + 0.0002 // 0.00030000000000000003

    // Scaling fractional numbers can prevent these rounding issues, but it's
    // not always practical.
    ((10000 * 0.0001) + (10000 * 0.0002)) / 10000 // 0.0003



    // Beware of NaN and computational errors.
    Math.sqrt(-1) // NaN

    var result = "five" - "four";
    result // NaN

    // You can test for NaN with the global isNaN() function.
    isNaN(result) // true



    // `Infinity` is a number.
    1 / 0 // Infinity

    // If you want to test that a number is finite, use the global
    // isFinite function!
    isFinite(Infinity) // false



    // You can parse strings into integers:
    parseInt("12")      // 12
    parseInt("012")     // 10 (string with leading 0 interpreted as octal)
    parseInt("012", 10) // 12 (force parseInt to use base-10)
    parseInt("345", 2)  // NaN (no part of the string can be parsed as base-2)
    parseInt("1.2", 10) // 1
    parseInt("1e3", 10) // 1
    parseInt("1xy", 10) // 1

    // Or non-integers:
    parseFloat("3.14")        // 3.14
    parseFloat("314e-2")      // 3.14
    parseFloat("0.0314E+2")   // 3.14
    parseFloat("3.14foobar")  // 3.14



    ///////////////////
    // Null & Undefined
    ///////////////////

    // Variable values are initialized to `undefined` by default.
    var foo;
    foo // undefined

    // So are object properties.
    var obj = {};
    obj.foo // undefined

    // Functions return `undefined` by default.
    function doNothing() {}
    doNothing() // undefined

    // So does the `void` operator.
    void 0 // undefined



    // So, variables can be undefined.
    var foo;

    // Variables can contain values or references to objects.
    foo = 123;
    foo // 123

    // And variables can be explicitly set to `null`.
    foo = null;
    foo // null


    // If it helps, think of undefined as the "default" non-value, while
    // null is the "explicitly set" non-value.






    //////////////////////////
    // Coercion and Comparison
    //////////////////////////

    // Coerce values by passing a value into a primitive type's function.

    // You can coerce to booleans:
    Boolean(0)          // false \
    Boolean("")         // false  | Note: these five values are JavaScript's
    Boolean(null)       // false  | "falsy" values! They get treated just
    Boolean(undefined)  // false  | like false in "if" statement conditions.
    Boolean(NaN)        // false /
    Boolean(false)      // false
    Boolean(true)       // true
    Boolean("foo")      // true
    Boolean(" ")        // true
    Boolean(1)          // true
    Boolean({a: 1})     // true
    Boolean([1, 2, 3])  // true
    Boolean(Boolean)    // true

    // You can coerce to strings:
    String(123)         // "123"
    String(true)        // "true"
    String(false)       // "false"
    String(null)        // "null"
    String(undefined)   // "undefined"
    String([1, 2, 3])   // "1,2,3"
    String({a: 1})      // "[object Object]"
    String(String)      // "function String() { [native code] }"

    // You can coerce to numbers:
    Number("12")        // 12
    Number("012")       // 12
    Number("1.2")       // 1.2
    Number("1e3")       // 1000
    Number("1xy")       // NaN
    Number("")          // 0
    Number(" ")         // 0
    Number(false)       // 0
    Number(true)        // 1



    // When an object is coerced to a string, its .toString() method is called.
    // Array values are joined on comma. "Plain" objects return the relatively
    // useless "[object Object]" string. Etc.
    var fn = function(a, b) { return a + b; };
    var arr = [1, 2, 3];
    var obj = {a: 1, b: 2};

    fn.toString()   // "function (a, b) { return a + b; }"
    arr.toString()  // "1,2,3"
    obj.toString()  // "[object Object]"
    String(fn)      // "function (a, b) { return a + b; }"
    String(arr)     // "1,2,3"
    String(obj)     // "[object Object]"

    // You can change how an object is stringified by defining a .toString method.
    obj.toString = function() { return this.a + this.b; };
    String(obj)     // "3"



    // Many of JavaScript's operators perform type coercion. For example, because
    // the + operator does both addition and concatenation, it will coerce its
    // operands to either numbers or strings, depending on the operand types.
    1 + 2         // 3
    1 + "2"       // "12"
    - "1"         // -1
    + "1"         // 1
    + "a"         // NaN
    +new Date()   // 1292604183838
    1 + true      // 2

    function foo() { alert("hi!"); }
    foo + ""      // "function foo() { alert("hi!"); }"

    1 == true     // true (because true gets coerced to 1)

    // FWIW, these produce the same result:
    String(val) === "" + val
    Number(val) === +val
    Boolean(val) === !!val






    ///////////////////////////
    // The == and === Operators
    ///////////////////////////

    // "The Strict Equality Comparison Algorithm"
    // How does the === operator work? Given x === y:

    // Type(x)          Values                                Result
    // Type(x) different from Type(y)...                      false
    // Undefined or Null                                      true
    // Number           x same value as y (but not NaN)       true
    // String           x and y are identical characters      true
    // Boolean          x and y are both true or both false   true
    // Object           x and y reference same object         true
    // Otherwise...                                           false



    // "The Abstract Equality Comparison Algorithm"
    // How does the == operator work? Given x == y:

    // Type(x)              Type(y)               Result
    // If x and y are the same type...            Follow === operator rules.
    // Null                 Undefined             true
    // Undefined            Null                  true
    // Number               String                x == toNumber(y)
    // String               Number                toNumber(y) == x
    // Boolean              (any)                 toNumber(x) == y
    // (any)                Boolean               x == toNumber(y)
    // String or Number     Object                x == toPrimitive(y)
    // Object               String or Number      toPrimitive(x) == y
    // Otherwise...                               false



    ///////////////////
    // Truthy and Falsy
    ///////////////////

    // In addition to the proper Boolean value false, JavaScript has five "falsy"
    // values: 0, "", null, undefined, NaN. These values are equivalent to false in
    // most scenarios, but they are NOT false.
    var a = 0;
    var b = "";
    var c = null;
    var d = undefined;
    var e = NaN;
    // Actually false.
    var f = false;

    // Passing a falsy value into an if statement works the same as passing false,
    // because falsy values get coerced to false.
    if (a) { /* This code will NOT execute */ }
    if (b) { /* This code will NOT execute */ }

    // Negate a falsy value by using the ! (logical NOT) operator.
    if (!c) { /* This code will execute */ }
    if (!d) { /* This code will execute */ }

    // Test to see if a value is actually false by using the === operator.
    if (e === false) { /* This code will NOT execute */ }
    if (f === false) { /* This code will execute */ }



    // Note that while all five falsy values can stand in for false in an if
    // statement, not all of them are == each other.

    // == returns true when comparing false, 0, ""
    false == 0         // true
    0 == ""            // true
    "" == false        // true

    // == returns true when comparing null and undefined
    null == undefined  // true

    // Note that null and undefined are, indeed, two different values.
    null === undefined // false

    // And, of course, NaN isn't === or == anything (LOLWUT).
    NaN == NaN         // false



    // Every value that's not falsy (or false) is truthy.
    var g = -3;
    var h = "hello world";
    var i = [];
    var j = [1, 2, 3];
    var k = {a: 1, b: 2};
    var l = function() {};
    var m = /^hello/i;
    // And of course, true is true.
    var n = true;

    if (g) { /* This code will execute */ }
    if (h) { /* This code will execute */ }
    // etc.



    // Because of the way == works, booleans can be coerced to primitives.
    1 == true   // true
    0 == false  // true

    // Even though a number or string might be truthy, when compared to true using
    // the == operator, it won't evaluate to true.
    var value = 5;
    if (value) { /* While this code will execute... */ }
    if (value == true) { /* This code will not, because 5 != 1 */ }



    // Summary: When you're looking for a truthy or falsy value, pass the value
    // into your if statement, negating with ! if necessary. When you're looking
    // specifically for true or false, use === or !==. Finally, use == or != only
    // when you want to test for null or undefined with == null or != null.






    //////////
    // Objects
    //////////

    // Everything that's not a primitive is an object.

    // You can create a new object using the "new" keyword and the Object
    // constructor function.
    var obj = new Object();

    // But using the object literal syntax is less to type.
    var obj = {};

    // Objects are passed and compared by reference, while primitives are compared
    // by their value.
    var obj1 = {foo: 123};
    var obj2 = {foo: 123};

    obj1 === obj2         // false (obj1 and obj2 are two different objects)
    obj1.foo === obj2.foo // true (both properties have the same primitive value)



    // You can initialize properties at the time an object is created. Note that
    // properties defined in an object literal need to be quoted if they contain
    // special characters.
    var obj = {foo: 123, 'bar': 456, "I can't wait!!": 789};



    // Object propery names are always strings. You can access, or dereference,
    // them via the "square bracket" syntax:
    obj["I can't wait!!"]  // 789

    var key = "foo";
    obj[key]               // 123

    // Or via the "dot" syntax, if the name doesn't contain special characters:
    obj.bar                // 456



    // What does "object property names are always strings" mean?
    var obj = {};
    obj["test"] = 100;

    // obj now looks like this:
    {
      "test": 100
    }


    // Let's make a function.
    function test() { return 123; }
    test() // 123

    // And let's invoke the function.
    obj[test()] = 200;

    // obj now looks like this:
    {
      "123": 200,
      "test": 100
    }


    // What happens if we don't invoke the function? (Hint: WHOOPS)
    obj[test] = 300;

    // obj now looks like this:
    {
      "123": 200,
      "test": 100,
      "function test() { return 123; }": 300
    }


    // Remember, object property names are *always* strings.
    obj[obj] = 400;

    // obj now looks like this:
    {
      "123": 200,
      "test": 100,
      "function test() { return 123; }": 300,
      "[object Object]": 400
    }


    // What happens if we define a .toString method on obj?
    obj.toString = test;
    obj[obj] = 999;

    // obj now looks like this:
    {
      "123": 999,
      "test": 100,
      "function test() { return 123; }": 300,
      "[object Object]": 400
    }



    ////////////////////////////////
    // Variables are not properties!
    ////////////////////////////////

    // A variable.
    var value = "variable";

    // An object with a property.
    var obj = {};
    obj.value = "property";

    value     // "variable"
    obj.value // "property"

    // A function that logs both the variable and the property.
    obj.logValues = function() {
      console.log(value);
      console.log(obj.value);
    };

    obj.logValues();
    // "variable"
    // "property"






    ////////////////////
    // Object Prototypes
    ////////////////////

    // While you can define properties directly on objects...
    var obj = {};
    obj.foo = 123;
    obj.hasOwnProperty("foo") // true

    // Objects inherit properties from their prototype.
    obj.hasOwnProperty("toString") // false
    obj.toString() // "[object Object]"

    Object.prototype.hasOwnProperty("toString") // true

    // You can define properties on the object prototype, BUT DON'T DO THIS!
    Object.prototype.bar = 456;
    obj.bar // 456

    // Why not? Because once the Object prototype is modified, EVERY for-in loop
    // over ANY instance of ANY OBJECT will be "tainted".
    var prop;
    for (prop in obj) {
      console.log(prop, obj[prop]);
    }
    // logs: "foo" 123
    // logs: "bar" 456



    // You can test to see if a property is in an object.
    "foo" in obj   // true
    "bar" in obj   // true

    // And you can delete properties from objects.
    delete obj.foo;
    delete Object.prototype.bar;

    "foo" in obj   // false
    "bar" in obj   // false






    /////////////////////
    // Self-aware Objects
    /////////////////////

    var awesome = "Horrible"; // <-- Dramatic foreshadowing

    var obj = {};
    obj.awesome = "Awesome";

    // You can hard-code objects by name.
    obj.getAwesome = function(word) {
      console.log(obj.awesome + " " + word);
    };

    obj.getAwesome("sauce"); // logs: "Awesome sauce"


    // Or you can use the more portable "this" value instead.
    obj.getAwesomeUsingThis = function(word) {
      console.log(this.awesome + " " + word);
    };

    obj.getAwesomeUsingThis("possum"); // logs: "Awesome possum"


    // What's the downside?

    // This example works, because "this" wasn't used in .getAwesome.
    ["sauce", "possum"].forEach(obj.getAwesome);
    // "Awesome sauce"
    // "Awesome possum"

    // But depending on how functions get invoked, the "this" value could
    // be the object, or it could be the GLOBAL OBJECT (whoops)
    ["sauce", "possum"].forEach(obj.getAwesomeUsingThis);
    // "Horrible sauce"
    // "Horrible possum"



    // When functions are invoked as they are being dereferenced from an
    // object, the "this" value inside the function refers to that object.

       obj.getAwesomeUsingThis("sauce");
    // ^^^ the "this" value inside of the .getAwesomeUsingThis function.

    // But if the dereferencing...
    var myFunction = obj.getAwesomeUsingThis;

    // ...and the invoking are in two different steps, like when you pass
    // a function into another function... VERY BAD THINGS HAPPEN
    myFunction("fail"); // logs: "Horrible fail"



    // Every function has a .call method, that's invoked just like the
    // function, except it takes one additional argument up-front. The
    // "this" value.
    myFunction.call(obj, "sauce"); // logs: "Awesome sauce"

    // And an .apply method, that works the same way but takes an array
    // of arguments (or an "arguments" object).
    myFunction.apply(obj, ["sauce"]); // logs: "Awesome sauce"


    // So, how do we solve our earlier problem? We can use .bind, which returns
    // a new function that has its "this" value locked-in.
    var getAwesome = obj.getAwesomeUsingThis.bind(obj);
    ["sauce", "possum"].forEach(getAwesome);
    // "Awesome sauce"
    // "Awesome possum"

    // Also, the Array iterator methods accept a second argument, that if
    // specified, gets used as the "this" value.
    ["sauce", "possum"].forEach(obj.getAwesomeUsingThis, obj);
    // "Awesome sauce"
    // "Awesome possum"






    //////////////////////
    // The typeof Operator
    //////////////////////

    typeof 1                    // "number"
    typeof "amazing"            // "string"
    typeof true                 // "boolean"

    typeof {}                   // "object"
    typeof []                   // "object" (unfortunately)
    typeof new Number(1)        // "object" (new + Contructor returns an object)
    typeof new String("yo!")    // "object" (new + Contructor returns an object)
    typeof new Boolean(true)    // "object" (new + Contructor returns an object)
    typeof new Date("1/1/1999") // "object" (new + Contructor returns an object)

    typeof Date("1/1/1999")     // "string" (didn't use the new keyword)

    typeof function() {}        // "function"
    typeof /^foo$/i             // "function" (in some browsers)

    typeof undefined            // "undefined"
    typeof null                 // "object" ?!

    typeof NaN                  // "number" ?!?!







    //////////////////////////
    // The instanceof Operator
    //////////////////////////

    // The instanceof operator tests the presence of constructor.prototype in
    // object's prototype chain.
    object instanceof constructor

    // Constructor functions used for primitive types return primitives unless
    // the new keyword is used.

    1                         instanceof Number   // false (primitive)
    "amazing"                 instanceof String   // false (primitive)
    true                      instanceof Boolean  // false (primitive)
    new Number(1)             instanceof Number   // true (object)
    new String("amazing")     instanceof String   // true (object)
    new Boolean(true)         instanceof Boolean  // true (object)

    // Constructor functions for other built-in types return objects, regardless of
    // whether the new keyword is used.

    var obj = {};           // sample object
    var fn = function() {}; // sample function

    obj                       instanceof Object   // true
    []                        instanceof Array    // true
    fn                        instanceof Function // true
    /^bar$/i                  instanceof RegExp   // true
    Object()                  instanceof Object   // true
    Array(1, 2, 3)            instanceof Array    // true
    Function("return 1")      instanceof Function // true
    RegExp("^bar$", "i")      instanceof RegExp   // true
    new Object()              instanceof Object   // true
    new Array(1, 2, 3)        instanceof Array    // true
    new Function("return 1")  instanceof Function // true
    new RegExp("^bar$", "i")  instanceof RegExp   // true

    // If Date is called without the new keyword, it returns a string, not a Date
    // object.

    Date("1/1/1999")          instanceof Date     // false
    new Date("1/1/1999")      instanceof Date     // true

    // And, for what it's worth, everything that was a instanceof a type is also
    // instanceof Object, because all types inherit from Object (the base type).

    obj                       instanceof Object   // true
    []                        instanceof Object   // true
    fn                        instanceof Object   // true
    /^bar$/i                  instanceof Object   // true
    Array(1, 2, 3)            instanceof Object   // true
    Function("return 1")      instanceof Object   // true
    RegExp("^bar$", "i")      instanceof Object   // true
    Object()                  instanceof Object   // true
    new Number(1)             instanceof Object   // true
    new String("amazing")     instanceof Object   // true
    new Boolean(true)         instanceof Object   // true
    new Date("1/1/1999")      instanceof Object   // true
    new Array(1, 2, 3)        instanceof Object   // true
    new Function("return 1")  instanceof Object   // true
    new RegExp("^bar$", "i")  instanceof Object   // true






    ////////////////////////
    // Smarter Type Checking
    ////////////////////////

    // The built-in Object type has a .toString method on its prototype, so all
    // objects get that method automatically.
    var obj = {};
    obj.toString() // "[object Object]"

    // While all other built-in types have their own .toString method that returns
    // a meaningful value:
    var arr = [1, 2, 3];
    arr.toString() // "1,2,3"

    // The Object .toString method can be run using call invocation, thus changing
    // this `this` value inside the function.
    var toString = Object.prototype.toString;

    toString.call(false)              // "[object Boolean]"
    toString.call(new Boolean(true))  // "[object Boolean]"

    toString.call(0)                  // "[object Number]"
    toString.call(new Number(1))      // "[object Number]"

    toString.call("a")                // "[object String]"
    toString.call(new String("z"))    // "[object String]"

    toString.call([1, 2, 3])          // "[object Array]"
    toString.call({a: 1})             // "[object Object]"
    toString.call(/^foo$/)            // "[object RegExp]"
    toString.call(new Date())         // "[object Date]"
    toString.call(null)               // "[object Null]"
    toString.call(undefined)          // "[object Undefined]"


    // This is a very simple type-checking function that works for both
    // primitives and objects:
    function type(value) {
      if (type == null) {     // Test for null or undefined, as Object .toString
        return String(value); // doesn't work reliably for them in all browsers.
      } else {
        return Object.prototype.toString.call(value).slice(8, -1).toLowerCase();
      }
    }

    type(false)              // "boolean"
    type(new Boolean(true))  // "boolean"
    type(0)                  // "number"
    type(new Number(1))      // "number"
    type("a")                // "string"
    type(new String("z"))    // "string"
    type([1, 2, 3])          // "array"
    type({a: 1})             // "object"
    type(/^foo$/)            // "regexp"
    type(new Date())         // "date"
    type(null)               // "null"
    type(undefined)          // "undefined"

#### jQuery Basics

* Using a querySelectorAll-supported selector will be significantly faster in modern browsers.
* Do as much work off-document as possible
    * I.e., modify things before placing them back in the document
* For deferreds:
    * http://api.jquery.com/category/deferred-object/ 
    * http://vimeo.com/22687950

##### Raw gist content:

Copying in this gist content: https://gist.github.com/08e517bb19abcf3d0cf5#file_jquery_fundamentals.js

    //////////////////////
    // jQuery Fundamentals
    //////////////////////



    //////////////////////
    // The jQuery function
    //////////////////////

    // Select some elements on the page using either this:
    var elems = jQuery(selector);

    // Or this:
    var elems = $(selector);

    // (jQuery and $ are references to the same global function)
    jQuery === $ // true

    // So instead of this mouthful:
    var elem = document.getElementById("header1");
    if (elem) {
      elem.innerHTML = "Lame.";
    }

    // You can just do this:
    $("#header1").html("Awesome!");






    //////////////////////
    // What is $, anyways?
    //////////////////////

    // Just to prove a point.
    var $ = function(selector) {
      return selector + " is a selector string, whatev";
    };

    $("#header1"); // "#header1 is a selector string, whatev"



    // Unlike many other languages, the "$" character has no special meaning in
    // JavaScript. It's just another valid character used in named identifiers,
    // like letters, numbers and underscores.
    var $foo = 123;
    var bar$ = 456;
    var $o$m$g$ = 789;
    var $$_$$_sUp3r_$_dUp3r_$$_$$ = "wtf, dude";






    ////////////////////////////////
    // jQuery objects are array-Like
    ////////////////////////////////

    // Select some elements, and store a reference to the resulting jQuery
    // object in a variable.
    var elems = $(".nonexistent");

    // While you CAN test if elements were selected like this:
    if (elems.length > 0) {
      elems.html("Nothing happens.");
    }

    // In most cases, you'll just want to do this. jQuery implicitly iterates
    // when you call jQuery methods on jQuery objects, so you don't need to
    // loop explicitly.
    $(".nonexistent").html("Nothing happens, but with much less code!");

    // If 0 elements were selected, jQuery does nothing. If 1 element was
    // selected, jQuery updates the html of that one element. If 9001 elements
    // were selected, jQuery updates the html of all 9001 elements.
    $("derp").html("Awesome!");
    $("#header1").html("Awesome!");
    $("li").html("Awesome!");






    ///////////////////////////////
    // jQuery objects are snapshots
    ///////////////////////////////

    // When you select elements from the document, you select them as they
    // exist in the document at the moment the jQuery function is called.
    var allDivsInTheDocument = $("div");

    // So if there were 10 elements...
    allDivsInTheDocument.length // 10

    // And you add a few more...
    $("<div/><div/><div/>").appendTo("body");

    // The existing jQuery objects you have don't change!
    allDivsInTheDocument.length // 10

    // Selecting elements from the document by calling the jQuery function
    // again will create a new snapshot.
    var allDivsInTheDocumentNow = $("div");
    allDivsInTheDocumentNow.length // 13






    /////////////////////
    // Selecting elements
    /////////////////////

    // You can use standard CSS selectors.
    var allDivsInTheDocument = $("div");
    var anchorChildrenOfParagraphs = $("p > a");
    var emailInputsInsideMyform = $("#my-form input[name='email']");

    // Along with standard CSS selectors, you can use custom jQuery selectors:
    var currentlyAnimatingDivs = $("div:animated");

    // Although custom jQuery selectors are much more useful when used in
    // scenarios like this.
    $("p").on("click", function() {
      var elem = $(this);
      if (!elem.is(":animated")) {
        elem.slideUp(3000).slideDown(500);
      }
    });

    // How can we write the previous example in a more concise way, using
    // implicit iteration?
    $("p").on("click", function() {
      $(this).not(":animated").slideUp(3000).slideDown(500);
    });

    // Avoid custom jQuery selectors when you don't need them, because they
    // prevent jQuery from taking advantage of native DOM methods.
    $("form input:submit").submit();

    // Using a querySelectorAll-supported selector will be significantly
    // faster in modern browsers.
    $("form input[type='submit']").submit();






    //////////////////////
    // Know your selectors
    //////////////////////

    // Keep your selectors simple!
    var overlySpecific = $("body p#paragraph1");
    var specificEnough = $("#paragraph1"); // Single #id selectors are fast!

    // Know the difference between selectors?

    // What's the difference?
    $("li:odd").addClass("highlight");
    $("li:nth-child(odd)").addClass("selected");

    // What's the difference?
    $("li:first").addClass("highlight");
    $("li:first-child").addClass("selected");

    // What's the difference?
    $("p > a").addClass("highlight");
    $("p a").addClass("selected");
    $("p:has(a)").addClass("highlight");






    ///////////////////////
    // Other ways to select
    ///////////////////////

    // Not only can you select elements with a selector string:
    var inputs = $("form input[name='first']");

    // You can pass a object into jQuery:
    var win = $(window);

    // Or even an array of objects:
    var winAndDoc = $([window, document]);

    // Since jQuery 1.4, you can easily get an empty set, if you need it.
    var emptySet = $();


    // Where else do we commonly pass an object into jQuery?
    $("a").on("click", function() {
      $(this).addClass("highlight"); // <---- right there with $(this)!
    });

    // Or:
    $("a").each(function() {
      $(this).addClass("selected"); // <---- right there with $(this)!
    });






    /////////////////
    // Filtering sets
    /////////////////

    // Given this jQuery object...
    var divs = $("div");

    // The "not" method filters the selected set of elements down to the
    // subset that doesn't match the given selector. This could be anywhere
    // from 0 to all of the initial set of elements.
    var divsNotAnimating = divs.not(":animated");

    // Using the ":not" selector inside the "filter" method will yield
    // equivalent results.
    var divsNotAnimating = divs.filter(":not(:animated)");

    // Of course, given the option, you could choose to do everything with a
    // single selector string.
    var divsNotAnimating = $("div:not(:animated)");

    // There are many jQuery custom selectors that can be used for filtering.
    var firstDiv = $("div:first");
    var lastDiv = $("div:last");
    var secondDiv = $("div:eq(1)");
    var divsContainingAnchors = $("div:has(a)");

    // And for most of them, there exists a corresponding filtering method.
    var firstDiv = divs.first();
    var lastDiv = divs.last();
    var secondDiv = divs.eq(1);
    var divsContainingAnchors = divs.has("a");






    /////////////////////
    // Traversing the DOM
    /////////////////////

    var form = $("#my-form");

    // You can find all descendant elements of an element.
    var inputsInForm = form.find("input");

    // Or all children of an element.
    var childrenOfForm = form.children();

    // There are all kinds of traversal methods. Parents, children, siblings,
    // you name it.
    $("h1").siblings().children(":first-child").next().addClass("highlight");
    $("li").parent().prevAll().addClass("highlight");

    // Elements don't have to be in the document to be traversable.
    $("<p><i/><b/></p>");                               // [<p><i></i><b></b></p>]
    $("<p><i/><b/></p>").children();                    // [<i></i>, <b></b>]
    $("<p><i/><b/></p>").children().text("x");          // [<i>x</i>, <b>x</b>]
    $("<p><i/><b/></p>").children().text("x").parent(); // [<p><i>x</i><b>x</b></p>]






    //////////////////////
    // Getters and setters
    //////////////////////

    // jQuery methods are both setters, modifying every selected element...
    $("li").html("<b>Hello</b> <i>world</i>");
    $("li").text("<b>Hello</b> <i>world</i>");

    // And getters. Note that methods that work as both getter and setter
    // will only return the value for the FIRST selected element.
    $("li").html(); // "<i>item 1</i> content"

    // With a few notable exception, of course.
    $("li").text(); // "item 1 contentitem 2 content item 3 contentitem 4 content"

    // Most methods that work as setters and getters will also accept a
    // callback that can be used to programmatically change values. Think
    // of this as a "combo" getter + setter.
    $("li").html(function(index, value) {
      return "<b>" + index + "</b> " + value;
    });






    ////////////////////////////
    // Attributes and properties
    ////////////////////////////

    var img = $("img").first();

    // Set the src attribute of the image.
    img.attr("src", "/static/img/sample.gif");

    // Get the src attribute.
    console.log( img.attr("src") ); // "/static/img/sample.gif"

    // Get the src property with jQuery.
    console.log( img.prop("src") ); // "http://bocoup.com/static/img/sample.gif"

    // But if you already have a DOM element reference, you can access
    // properties directly from the element. This is very efficient!
    console.log( this.src );        // "http://bocoup.com/static/img/sample.gif"

    // Also, this is how you set and unset a boolean attribute. To disable an
    // element, you set the "disabled" attribute to "disabled". To re-enable
    // the element, you remove the attribute.
    img.attr("disabled", "disabled");
    img.removeAttr("disabled");

    // To disable or re-enable an element using a boolean property, you just
    // set the property value to true or false. Much nicer!
    img.prop("disabled", true);
    img.prop("disabled", false);



    // Change form element values.
    $("form input[name='first']").val("Ben");

    // Add or remove classes.
    $("div").addClass("foo").removeClass("bar").toggleClass("foo bar");

    // Change inline style properties.
    $("p").css({
      color: "#fff",
      opacity: 0.75,
      fontWeight: 700,
      "background-color": "#007"
    });

    // Get and set inline style properties.
    $("p").css("color", "#0a0");
    $("p").css("color"); // "rgb(0, 170, 0)" (Note: value format may change!)

    // Change width and height. Also see .innerHeight() and .outerHeight().
    $("img").width(30).height(150);

    // Change offsets.
    $("img:first").offset({left: 300, top: 200});






    ///////////////////////////////////////////////////////
    // Modifying jQuery objects doesn't update the document
    ///////////////////////////////////////////////////////

    // If you select some elements from the document...
    var myElement = $("#my-element");

    // And then modify that jQuery object...
    myElement.id = "another-value";

    // It doesn't actually change the DOM or any selected elements!
    myElement.prop("id") // "my-element"

    // It just changes the property of that jQuery object.
    myElement.id // "another-value"

    // If you want to modify elements, use jQuery methods!
    myElement.prop("id", "another-value");






    ////////////////////////
    // Creating new elements
    ////////////////////////

    // When creating elements, you can add attributes, properties, content, etc.
    var graph = $('<p id="test" class="fancy"><b>hello</b> <i>world</i></p>');

    // You can do the same things (and more) with jQuery methods.
    var graph = $("<p/>");
    graph.prop("id", "test");
    graph.addClass("fancy");
    graph.html("<b>hello</b> <i>world</i>");
    graph.on("click", function() {
      console.log( $(this).text() );
    });

    // Ever since jQuery 1.4, you can also pass in an options object as the
    // second argument to the jQuery function when creating a new element.
    var graph = $("<p/>", {
      id: "test",
      className: "fancy",
      html: "<b>hello</b> <i>world</i>",
      click: function() {
        console.log( $(this).text() );
      }
    });






    ////////////////////////////
    // Manipulating the document
    ////////////////////////////

    // Once you've created something, how do you attach it to the document?
    var graph = $("<p>new content</p>");

    graph.prependTo("#target");    // Inside #target, at the beginning.
    graph.appendTo("#target");     // Inside #target, at the end.
    graph.insertBefore("#target"); // Outside #target, before.
    graph.insertAfter("#target");  // Outside #target, after.
    graph.replaceAll("#target");   // Replace #target completely.

    // These methods do similar things, but chain a little differently.
    $("#target").prepend("<p>new content</p>");
    $("#target").append("<p>new content</p>");
    $("#target").insert("<p>new content</p>");
    $("#target").after("<p>new content</p>");
    $("#target").replaceWith("<p>new content</p>");



    // Note that when you append an element to the DOM, it gets MOVED to
    // the new location, NOT copied. Elements can exist in only one place
    // in the document (or in a fragment in memory) at a time.
    var elem = $(".my-element");
    elem.length // 1

    // Move elem somewhere else.
    elem.appendTo("#new-parent");

    // Yep, there's still only one of them.
    $(".my-element").length // 1



    // If you really want to duplicate an element, clone it!
    var elem = $(".my-element");
    elem.length // 1

    // First, clone elem. Then, move the clone somewhere else.
    elem.clone().appendTo("#new-parent");

    // When you clone an element with an id, you need to change (or remove)
    // the id before appending it into the document, because HTML doesn't allow
    // duplicate ids in the document!
    elem.clone().removeAttr("id").appendTo("#new-parent");

    // If you also want to clone event handlers and data, pass true to .clone().
    $("a").first().clone(true).insertAfter("#new-parent");






    ///////////////////////////////////////////
    // Do as much work off-document as possible
    ///////////////////////////////////////////

    // This adds the class AFTER the element has been appended to the
    // document, which causes an unnecessary reflow.
    $("<p>new content</p>").appendTo("#target").addClass("highlight");

    // This adds the class before appending the element, while it is still
    // only in memory.
    $("<p>new content</p>").addClass("highlight").appendTo("#target");






    ///////////
    // Chaining
    ///////////

    // You can select elements, filter them, and manipulate them in multiple
    // steps, using variables.
    var graphs = $("p");
    var graphsWithAnchors = graphs.has("a");
    graphsWithAnchors.addClass("highlight");

    // Because jQuery methods are chainable, you can often forgo variables.
    $("p").has("a").addClass("highlight");

    // Although it's a good idea to store a jQuery object in a variable
    // instead of re-selecting the same set of elements later on!
    var graphs = $("p").has("a");

    graphs.addClass("highlight");

    $("#my-button").on("click", function() {
      graphs.removeClass("highlight");
    });



    // Whenever you reduce a set of elements down to a subset using a jQuery
    // filtering method, get all new elements using a jQuery traversal method,
    // or use a jQuery method as a setter, jQuery returns a jQuery object.

    // When a jQuery method returns a jQuery object, you can chain.

    // Let's break this chain down:
    $("ul").children().not(":last-child").addClass("highlight").html();

    $("ul") // select: returns a jQuery object.
      .children() // traverse: returns a new jQuery object.
        .not(":last-child") // filter: returns a new jQuery object.
          .addClass("highlight") // set: returns the same jQuery object.
            .html(); // get: returns a string of HTML, not a jQuery object!






    /////////
    // Events
    /////////



    // Use the "on" method for binding event handlers.
    $(window).on("resize", function() {
      repositionModalDialog();
    });

    // Just note that when you use the "off" method to unbind event handlers,
    // you unbind ALL event handlers of that type.
    $(window).off("resize");


    // But if you bind using a named function...
    $(window).on("resize", repositionModalDialog);

    // ...and unbind using the same named function, only the event handlers
    // bound using that function will be unbound, leaving other event
    // handlers of that type untouched.
    $(window).off("resize", repositionModalDialog);


    // And if you bind using namespaces...
    $(window).on("resize.mymodal", function() {
      repositionModalDialog();
    });

    // ...and unbind using the same namespace, only the event handlers
    // bound with that namespace will be unbound, leaving other event
    // handlers of that type untouched.
    $(window).off("resize.mymodal");


    // You can even bind multiple event types at once, with optional
    // namespaces...
    $(window).on("resize.mymodal scroll.mymodal", function() {
      repositionModalDialog();
    });

    // ...and unbind them ALL at once, using just the namespace.
    $(window).off(".mymodal");






    ///////////////////
    // Event Delegation
    ///////////////////

    // Instead of binding event handlers to every individual element...
    $("#my-list li").on("mouseover mouseout", function(event) {
      $(this).toggleClass("highlight");
    });

    // Consider using event delegation to bind a single event handler to an
    // ancestor element.
    $(document).on("mouseover mouseout", "#my-list li", function(event) {
      $(this).toggleClass("highlight");
    });

    // Not only does event delegation do less work up-front, but it also
    // allows matched elements to be added after-the-fact.
    $("#my-list").append("<li>OMG</li><li>SUPER</li><li>AWESOME</li>");

    // It's recommended that you attach the event handler to the closest
    // ancestor element that makes sense. Like the list, table or "widget."
    $("#my-list").on("mouseover mouseout", "li", function(event) {
      $(this).toggleClass("highlight");
    });






    ///////
    // Ajax
    ///////

    // jQuery's $.ajax() method accepts an options object where we can specify
    // extra data we want to send, which HTTP method (GET, POST, etc) to use,
    // what type of data we expect to receive, and how to react when the request
    // succeeds or fails.
    $.ajax("/data/people.json", {
      data: {count: 3},
      type: "GET",
      dataType: "json",
      success: function(res) {
        $("#target").html("<h2 class=well>" + res.people[0].name + "</h2>");
      },
      error: function(req, status, err) {
        console.error("Something went wrong! Status: %s (%s)", status, err);
      }
    });



    // jQuery provides a number of Ajax convenience methods that are basic
    // wrappers around the $.ajax() method.

    // The $.get() method accepts a url, optional data object, optional success
    // handler, and optional data type.
    $.get("/data/people.json", {count: 3}, function(res) {
      console.log("Response", res);
    });

    // It's basically just a shorter way of writing this:
    $.ajax("/data/people.json", {
      data: {count: 3},
      type: "GET",
      success: function(res) {
        console.log("Response", res);
      }
    });

    // The $.post() method is just like the $.get() method but explicitly
    // specifies a type of "POST" (HTTP method)
    $.post("/data/save", {name: "Bocoup"}, function(res) {
      console.log("Response", res);
    }, "json");

    // The $.getJSON() method is just like the $.get() method but explicitly
    // specifies a dataType of "json"
    $.getJSON("/data/people.json", {count: 3}, function(res) {
      console.log("Response", res);
    });

    // The $.getScript() method is just like the $.get() method but explicitly
    // specifies a dataType of "script"
    $.getScript("/assets/js/test.js");

    // And if you need to run JavaScript after your JavaScript, you can.
    $.getScript("/assets/js/test.js", function() {
      $("#target h2").append("!!!").attr("class", "alert alert-success");
    });

    // You actually don't need to specify a success callback for any of the
    // Ajax methods.
    $.ajax("/data/people.json");
    $.get("/data/people.json");
    $.getJSON("/data/people.json");
    $.post("/data/save", {name: "Bocoup"});



    // But if you don't specify a success callback, how can you do something
    // with the inevitable response? Because Ajax methods return a jqXHR
    // object, and that object has methods of its own.
    var jQXHR = $.getJSON("/data/people.json");

    jQXHR.then(function(res) {
      $("#target").html("<h2 class=well>" + res.people[0].name + "</h2>");
    }, function(req, status, err) {
      console.log("Something went wrong! Status: %s (%s)", status, err);
    });

    // We can specify as many success handlers as we want, using the .done()
    // method, as many error handlers as we want, using the .fail() method, and
    // a single success (and optional error) handler using the .then() method.
    var req = $.getJSON("/data/people.json");
    req.done(onSuccess1, onSuccess2);
    req.fail(onError1, onError2, onError3);
    req.done(onSuccess3);
    req.then(onSuccess4, onError4);

    // If we want to specify a handler that runs whether or not the request
    // succeeds or fails, we can use the .always() method.
    req.always(onSuccessOrError);



    // Have you ever done this? You want to execute code when multiple Ajax
    // requests have completed, and the easiest way is to do them serially by
    // nesting callbacks. But this is gross.
    $.getJSON("/data/person.json", function(data) {
      $.get("/templates/person.tmpl", function(tmpl) {
        // This code executes once both requests have resolved.
        doSomething(data, tmpl);
      });
    });

    // Using the $.when() method, we can combine multiple Ajax requests into
    // a single object that behaves just like a jQXHR. The object that $.when
    // returns is known as a Deferred (jQXHR objects are Deferreds as well).
    var dataReq = $.getJSON("/data/person.json");
    var tmplReq = $.get("/templates/person.tmpl");

    $.when(dataReq, tmplReq).then(function(data, tmpl) {
      // This code executes once both requests have resolved.
      doSomething(data[0], tmpl[0]);
    });



    // You can even create your own Deferred objects. In this example, the
    // getTemplate function returns a Deferred object. When the underlying
    // Ajax request completes successfully, the Deferred object is resolved
    // with the compiled template.
    var getTemplate = function(id) {
      var dfd = $.Deferred();
      $.get("/templates/" + id + ".tmpl").when(function(res) {
        dfd.resolve( _.template(res) );
      }, function(req, status, err) {
        dfd.reject(status);
      });
      return dfd.promise();
    };

    var dataReq = $.getJSON("/data/person.json");
    var tmplReq = getTemplate("person");

    $.when(dataReq, tmplReq).then(function(data, tmplFn) {
      // This code executes once both requests have resolved.
      doSomething(data[0], tmplFn);
    });







    ////////////////
    // Learn the API
    ////////////////

    // Bookmark api.jquery.com and go there EVERY SINGLE DAY!

    // Find cool utilities like $.type:
    $.type(1)               // "number"
    $.type(new Number(1))   // "number"
    $.type({a: 1})          // "object"
    $.type([2, 3])          // "array" Awesome!

    // Or the more-specific type-related functions:
    $.isArray([2, 3])       // true
    $.isFunction($)         // true
    $.isPlainObject({})     // true

    // Or the $.extend() method for cloning and merging objects:
    var obj = {a: [1,2,3], b: [4,5,6]};

    // Shallow clone an object.
    var shallowClone = $.extend({}, obj);

    // Deep clone an object.
    var deepClone = $.extend(true, {}, obj);

    // Merge objects, preserving the original object.
    var mergedObj = $.extend({}, obj, {b: true, c: false});

    // Merge objects, modifying the original object.
    $.extend(obj, {b: true, c: false});

#### Debugging Essentials

* Preso given using Google Chrome Canary (beta build of Chrome)
* `$0` is a shorthand for the element selected in the Web Inspector
* Stop using `alert()` for debugging
* Use `console` for writing things to the console
    * IE <= 7, there is no console object
    * IE 8, the console only exists after you've opened it (F12)
    * This means test that it exists:
    
        function log(msg) {
            if (window.console && console.log) {
                console.log(msg);
            }
        }

* Four levels of writing to console:
    * `console.log()`
    * `console.info()`
    * `console.warn()`
    * `console.error()` - may throw an exception
* If you want the raw JS object:
    * `console.dir()` is the way to go
* Debugging inline `<script>` is very hard. Use external files
* Sources tab has the ability to to catch exceptions
    * blue   = all exceptions
    * purple = uncaught exceptions
* If you know where you want to stop & trigger your console to catch, you can just include `debugger` to trigger the console at a specific point
* Breakpoints allow you to stop at specific points in the code execution to see what's what
* Watch Expressions allow you to specify variables & properties to watch
* The Call Stack can show you where your code triggers an error in a library
    * Pretty Print button (two braces) can unminify a library to aid in this
    * Or, better yet, use the unminified version of the library!

### Rebecca Murphey

[@rmurphey](http://twitter.com/rmurphey)
[GitHub](https://github.com/rmurphey)

See the gist ([original](https://gist.github.com/31b7d31e9eea610d71b9), [my fork](https://gist.github.com/dfa400c97585997d76a4) )

Most of the info is [here](https://gist.github.com/dfa400c97585997d76a4#file_notes.js).

Big stuff:
* IIFEs are the way to handle scope in JS
    * In-depth: http://benalman.com/news/2010/11/immediately-invoked-function-expression/
* Read up on the module pattern:
    * http://www.adequatelygood.com/2010/3/JavaScript-Module-Pattern-In-Depth
* There's quite a few patterns to utilize, one would be a constructor
* First style of handling dependency loading & building was Dojo
    * Was synchronous; great for builds, terrible for dev
* AMD = *A*synchronous *M*odule *D*efinition
    * require.js is the current popular way to do this 

## Day 2 - 2012.12.04

### Ben Alman

#### Grunt

* Very new - April 2012
* Website - http://gruntjs.com/
* automation tool
    * Lint code
    * Unit testing
    * concatenate files very simply
* cross-platform, written in JS, using Node.js
* Grunt requires a grunt.js file at the root level of a project
* Can be inited for a new project from a template
    * Includes a jQuery plugin template, among others
* grunt.js is a JavaScript, not JSON, config file
* Grunt supports underscore.js templates for config stuff
* concat - multi-task
    * concat one or more files & output a new, concat'd file
* min - minifies things
    * has been changed to "uglify" in 0.4
    * Can be a next step after concat, can take the output file from the concat step, for example
* Tasks are run synchronously
    * Errors prevent further tasks from running
    * Example workflow:
        * lint
        * unit test
        * concat
        * minify
* Similar to Capistrano, but meant for building, not deploying

### Rebecca Murphey

#### Writing Testable JS

* Writing tests helps plan through how the code works
* Can take as much time as the coding itself
    * Prevents lots of debugging later, however
* Difficulty w/ testable JS:
    * anonymous functions, lack of structure
    * complex, oversized functions
        * example given of a `$.ajax` method in jQuery
    * lack of configurability
    * hidden or shared state
    * tightly coupled
* Rebecca's 4 areas of concern for JS testing:
    1. presentation & interaction
    2. data/server communication
    3. application state
    4. setup
* Helpful guiding principles:
    * use constructors to create instances
        * more OO
        * refer to yesterday's discussion of IIFEs and modular JS dev
    * support configurability
    * keep methods simple
        * good rule: if method is more than 5 lines, think about it & maybe break it up
        * lots of conditional logic is probably not good
    * don't intermingle responsibilities
        * e.g., a search form shouldn't know about the results list it spawns
* Write tests first
    * see `testable-javascript/test/tests/views/likes.js` for example tests
    * test's code can look very similar (both in length & form) to implementation code
        * idea here is that your implementation might be mere typing, not thinking
    * for testing data/server communication:
        * don't want to test that the server works, just that the request is identical to what's expected
            * e.g., test that the URL matches what's expected
        * use `sinon.useFakeXMLHttpRequest()` to fake these connections
        * if using AJAX, you can test that you receive a promise (i.e., a jQHR object)
            * assert that there's a `then` method for this
* exisiting applications:
    * audit existing manual tests & begin automating
* awesome tools for testing:
    * grunt + qunit + phantomjs – out-of-the-box stack
    * grunt-mocha – Rebecca's favorite
        * has great async API, unlike qunit
        * bring your own assertion library (e.g., chai, expect.js)
    * grunt-jasmine – appeals to rubyists
    * sinin.js – allows for "spying" on requests
    * chai.js – assertion library
* [Links on Rebecca's pinboard](http://pinboard.in/u:rmurphey/t:testable-javascript/)

### Dan Heberden

#### Getting a grip on Git

* yay version control
* Basics of git usage
* Branching!
* Fun stuff from nthdegreeburns:
    * git commit -v (make a commit w/ the diff so you can triple check your work…)
    * git add -p (interactive git add to pick out lines of code to commit that are related in a ton of intermingled code changes)
    * git rebase -i (NEVER do a rebase without it being interactive -- delete any lines that don't have commits you recognize, or you add dupe commits to the history)
    
#### Deploy!

* more git goodness
* Good way to think of remotes: just a label for another folder elsewhere
* Most of preso has been how to work w/ remotes
* No actual deploy stuff, sadly. Mostly about sharing code, not deploying it, with exception of quick mention of Gith

### Rebecca Murphey (again)
#### Build an app
* example app is to talk to an [Arduino](http://www.arduino.cc/)

Process:

1. sketch out app physically
    * whiteboard, pen & paper, etc.
2. configure require.js
3. write tests & code
4. connect pieces
5. write functional tests
6. connect to real data

* setting up require.js is a bit of a process
    * if using Backbone.js, there's a Backbone Boilerplate (grunt has a bbb plugin)
* whoa intense.