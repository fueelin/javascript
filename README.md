# FPI JavaScript Style Guide

*Originally forked from the Airbnb style guide.*


## Table of Contents
  1. [Introduction](#introduction)
  1. [Naming Conventions](#naming-conventions)
  1. [Line Length](#line-length) 
  1. [Modules](#modules)
  1. [Classes](#classes)
  1. [Class Structure](#class-structure)
  1. [Functions](#functions)
  1. [Whitespace](#whitespace)
  1. [Variables](#variables)
  	1. [Hoisting](#hoisting)
  1. [Blocks](#blocks)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Enums](#enums)
  1. [Properties](#properties)
  1. [Conditional Expressions & Equality](#conditional-expressions--equality)
  1. [Type Inspection, Casting, & Coercion](#type-inspection-casting--coercion)
  1. [Promises](#promises)
  1. [Events](#events)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Comments](#comments)
  	1. [Regions](#regions)
  1. [Abbreviations](#a	bbreviations)
  1. [Third Party](#third-party)
  	1. [jQuery](#jquery)
  	1. [Knockout](#knockout)
  	2. [Require](#require)
  1. [Appendices](#appendices)
  	1. [Revision History](#revision-history)
  	1. [Resources](#resources)
  	1. [License](#license)


## Introduction

The goal of this document is to promote consistent, expressive code.  As team size and project scope increases, readability becomes much more important.  New developers will be brought on.  Experienced developers will more-frequently be working on code they've never seen before.  Focusing on readability and consistency will greatly accelerate these developers' familiarization with new code.

*A note on naming:*

Choosing expressive, clear names for classes, properties, and functions can be a surprisingly difficult process.  It's worth the effort though, as naming has as big an impact on the intuitiveness of a piece a code as nearly any other factor.  Well-chosen property and function names lead to code that reads almost like a sentence.  Being closer to natural language, the intent and effects of this code will be much more obvious to a developer.  Fewer comments will be necessary.

This style guide has a [Naming Conventions](#naming-conventions) section that addresses a number of specific cases, but it's important to have a general focus on investing the necessary time and effort into using clear and expressive names on top of that.

*A note on white space:*

It is often our instinct, as developers, to try to make our code smaller and more concise.  There are benefits to this, but it's important not to go too far and sacrifice readability as a consequence.  The real benefits come not from a smaller lines-of-code count but instead from expressing ideas and process more succinctly, as well as removing redundant code paths.     

We should should use white space liberally, taking advantage of its ability to improve readability.  The most important use, which comes up in a number of rules below, is to visually group properties and code in logical ways by spacing it out.  This helps the developer see and interpret the code in manageable, comprehensible chunks.  By allowing the code to 'breathe', we make a function or module much less intimidating for a new developer to learn.  

This should all be covered by specific rules in this guide.  Most of these rules are contained in the [Whitespace](#whitespace) section, so pay special attention there.    

**[⬆ back to top](#table-of-contents)**


## Naming Conventions

  - Be descriptive with your naming.

	```javascript
	// bad
	var count = add(l1, l2).length;

	// good
	var customerCount = addCustomerLists(customerList1, customerList2).length;
	```

  - Boolean property names should ask a question.

	```javascript
	// bad
	var readOnly = false;

	// good
	var isReadOnly = false;
	```

  - Avoid single letter names. 

    ```javascript
    // bad
    function q() {
      
    }

    // good
    function query() {
      
    }
    ```

  - Use camelCase when naming properties, enums, objects, functions, and instances.

    ```javascript
    // bad
    var OBJEcttsssss = {};

    var this_is_my_object = {};

    function c() {}

    var u = new user({
      	name: 'Bob Parr'
    });

    // good
    var thisIsMyObject = {};

    function thisIsMyFunction() {}

    var user = new User({
      	name: 'Bob Parr'
    });
    ```

  - Use PascalCase when naming constructors or classes.

    ```javascript
    // bad
    function user(options) {
      	this.name = options.name;
    }

    var bad = new user({
      	name: 'nope'
    });

    // good
    function User(options) {
      	this.name = options.name;
    }

    var good = new User({
      	name: 'yup'
    });
    ```

  - Use a leading underscore `_` when naming properties that are 'theoretically' private but technically public.  For     example, this approach is required to allow a subclass to access its base class' private members.

    ```javascript
    // bad
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';

    // good
    this._firstName = 'Panda';
    ```

  - When saving a reference to `this` use `_this` (except nested classes).

    ```javascript
    function Customer() {
      var _this = this;

      return function() {
      	console.log(_this);
      };
    }
    ```
    
  - When saving a reference to `this` in a nested class, use `__this`.
  
  ```javascript
  function Customer() {
  	var _this = this;
  	
  	function Address() {
  		var __this = this;
  	}
  }
  ```

  - Save references to a base class as `_base`.

	```javascript
	function CollateralWidget() {
		var _base = $.copyFunctions(Widget.call(this, name, parent, data));
	
		// ...logic...
	}
	```
	
  - Indicate factory functions with either the prefix `make` or the suffix `Factory`.
  
  ```javascript
  	function makeGridRow(data) {
  		return new GridRow(data);
  	}
  	
  	this.scopeFactory = function scopeFactory (data) {
  		return new Scope(data);
  	};
  ```

**[⬆ back to top](#table-of-contents)**

## Line Length

  - Lines of code should not exceed 135 columns in length.

**[⬆ back to top](#table-of-contents)**

## Modules

  - Module names should match the returned type.
  
  - Modules that return a class/constructor should be named in Pascal case.
  
  - Modules that return a namespace/singleton should be named in Camel case.

**[⬆ back to top](#table-of-contents)**


## Classes

  - Define properties on `this`, not `_this`, during construction.  
   
  ```javascript
  // bad
  function Customer () {
  	var _this = this;
  	
  	_this.id;
  	// ...etc...
  }
  
  // good
  function Customer () {
  	var _this = this;
  	
  	this.id;
  	// ...etc...
  }
  ```

  - Group properties logically, with newlines separating these groupings.
  	
	```javascript
	// bad
	function Customer () {
		var _this = this;

		this.id;
		this.fullName;
		this.phone;
		this.firstName;
		this.address;
		this.lastName;
	}

	// good
	function Customer () {
		var _this = this;

		this.id;

		this.firstName;
		this.lastName;
		this.fullName;

		this.phone;
		this.address;
	}
	```

  - Assign methods to the prototype object, instead of overwriting the prototype with a new object. Overwriting the prototype makes inheritance impossible: by resetting the prototype you'll overwrite the base!

    ```javascript
    function Jedi() {
      	console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      	fight: function fight() {
        	console.log('fighting');
      	},

      	block: function block() {
        	console.log('blocking');
      	}
    };

    // good
    Jedi.prototype.fight = function fight() {
      	console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      	console.log('blocking');
    };
    ```

  - Methods on the prototype can return `this` to help with method chaining.

    ```javascript
    // bad
    Jedi.prototype.jump = function() {
      	this.jumping = true;

      	return true;
    };

    Jedi.prototype.setHeight = function(height) {
      	this.height = height;
    };

    var luke = new Jedi();

    luke.jump(); // => true
    luke.setHeight(20) // => undefined

    // good
    Jedi.prototype.jump = function() {
      	this.jumping = true;

      	return this;
    };

    Jedi.prototype.setHeight = function(height) {
      	this.height = height;

      	return this;
    };

    var luke = new Jedi();

    luke.jump()
    	.setHeight(20);
    ```

  - It's okay to write a custom toString() method, just make sure it works successfully and causes no side effects.

    ```javascript
    function Jedi(options) {
      	options || (options = {});

      	this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName() {
      	return this.name;
    };

    Jedi.prototype.toString = function toString() {
      	return 'Jedi - ' + this.getName();
    };
    ```

**[⬆ back to top](#table-of-contents)**

## Class Structure

  - ViewModel classes (widgets, views, etc.) should be organized into the following sections:
  
    + 1. **Base Class Settings** 
      - Property overrides for base class.  
      - Denoted by `####` comment.
    + 2. **Properties**
      - Public properties first, followed by private. 	
      - Denoted by `####` comment.
    + 3. **Event Model***
      - Overrides of ViewModel lifecycle functions, plus their (exclusive) helpers.
      - Enclosed in a region.
    + 4. **Features**
      - Functions, computed observables, and configs grouped by logical purpose.
      - Enclosed in a region, with sub-regions for each feature.
    + 5. **Nested Classes**
      - Enclosed in a region.
      
  ```javascript 
  function SearchWidget() {
  	var _this = this;
  	
  	//#### Base Class Settings ####
  	this.screenCde = fpiEnums.screens.search;
  	
  	//#### Properties ####
  	this.customerName = ko.observable();
  	
  	var isDirty = ko.observable(false);
  	
  	//#region Event Model
  	
  	this.loading = function () {
  		// ...stuff...
  	}
  	
  	//#endregion
  	
  	//#region Features
  	
  	//#region Search
  	
  	var searchParams = ko.computed({
  		// ...stuff...
  	});
  	
  	this.runSearch = function () {
  		// ...stuff...
  	}
  	
  	//#endregion
  	
  	//#endregion
  	
  	//#region Nested Classes
  	
  	function SearchData() {
  		// ...stuff...
  	}
  	
  	//#endregion
  }
  ```
  
  - **Note:** Empty sections should be omitted.
  
  - Non-ViewModel classes use the same scheme, but omit the `Base Class Settings` and `Event Model` sections.

**[⬆ back to top](#table-of-contents)**

## Functions

  - Function expressions:

    ```javascript
    // private function expression
    function named() {
    	return true;
    }

	// public anonymous function expression
	this.getName = function () {
		return 'test';
	};

	// public named function expression
	this.getName = function getName() {
		return 'test';
	};

    // immediately-invoked function expression (IIFE)
    (function() {
    	console.log('Welcome to the Internet. Please follow me.');
    })();
    ```
  
  - Naming promise callbacks is optional, but should be done for complex logic that may require debugging.

  ```javascript
  // good
  _this.loading().then(function () {
  	// ...stuff...
  });
  
  // good
  $.when(getLoanData, getCollateralData).then(function mergeCollateralData (loanData, collateralData) {
  	// ...stuff...
  });
  ```
  
  - Always name the `read` and `write` callbacks used to define a computed observable.  The function names should be the same as the computed's name, but with 'read' or 'write' prepended.
   
  ```javascript
  // bad
  var isVisible = ko.computed(function () {
  	// ...stuff...
  });
  
  //bad
  var isVisible = ko.computed({
  	read: function () {
  		// ...stuff...
  	},
  	write: function () {
  		// ...stuff...
  	},
  });
  
  // good
  var isVisible = ko.computed(function readIsVisible () {
  	// ...stuff...
  });
  
  //good
  var isVisible = ko.computed({
  	read: function readIsVisible () {
  		// ...stuff...
  	},
  	write: function writeIsVisible () {
  		// ...stuff...
  	},
  });
  ```

  - Never declare a function in a non-function block (`if`, `while`, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently.

    ```javascript
    // bad
    if (currentUser) {

    	function test() {
    		console.log('Nope.');
    	}
    }

    // good
    var test;

    if (currentUser) {

    	test = function test() {
    		console.log('Yup.');
    	};
    }
    ```

  - Never name a parameter `arguments`, this will take precedence over the `arguments` object that is given to every function scope.

    ```javascript
    // bad
    function nope(name, options, arguments) {
    	// ...stuff...
    }

    // good
    function yup(name, options, args) {
    	// ...stuff...
    }
    ```

  - Avoid single line function definitions as they don't work well with debuggers and are less readable.

	```javascript
	// bad
	function logError(ex) { console.log(ex.message); }

	//good
	function logError(ex) {
		console.log(ex.message);
	}
	```

**[⬆ back to top](#table-of-contents)**


## Whitespace
  
  - Place 1 space before the leading brace.

    ```javascript
    // bad
    function test(){
      	console.log('test');
    }

    // good
    function test() {
      	console.log('test');
    }

    // bad
    dog.set('attr',{
      	age: '1 year',
      	breed: 'Bernese Mountain Dog'
    });

    // good
    dog.set('attr', {
      	age: '1 year',
      	breed: 'Bernese Mountain Dog'
    });
    ```

  - Set off operators with spaces.

    ```javascript
    // bad
    var x=y+5;

    // good
    var x = y + 5;
    ```

  - Precede new blocks with a newline.
  
	```javascript
	// bad
	var customer = selectedCustomer();
	if (customer) {
		console.log(customerr);
	}

	// bad
	var allCustomers = customerList();
	allCustomers.forEach(function (customer) {
		if (customer.isBusiness) {
			console.log(customer);
		}
	});

	// good
	var customer = selectedCustomer();

	//Precede 'if' block with newline.
	if (customer) {
		console.log(customerr);
	}

	// good
	var allCustomers = customerList();

	//Precede 'function' block with newline.
	allCustomers.forEach(function (customer) {

		//Precede 'if' block with newline.
		if (customer.isBusiness) {
			console.log(customer);
		}
	});
	```  

  - Precede multi-line statements with a newline.

	```javascript
	// bad
	var errorBase = 'Error: ';
	console.log(errorBase 
		+ ex.message 
		+ application.fullName
	);

	// good
	var errorBase = 'Error: ';

	console.log(errorBase 
		+ ex.message 
		+ application.fullName
	);
	```

  - Precede `return` statements with a newline, unless they're the only line in a block.

	```javascript
	// bad
	function getCustomer(id) {
		var customer = customerCache[id];
		return customer;		
	}
	
	// bad
	function getCustomer(id) {
		var customer = customerCache[id];
		
		if (customer) {
		
			return customer;
		}
		
		return 'No customer found';
	}

	// good
	function getCustomer(id) {
		var customer = customerCache[id];

		return customer;		
	}
	
	// good
	function getCustomer(id) {
		var customer = customerCache[id];
		
		if (customer) {
			return customer;
		}
		
		return 'No customer found';
	}
	```

  - Use newlines to logically group code to improve comprehension.

	```javascript
	// bad 
	function createCustomerTooltip(customer) {
		var address,
			tooltipText;
		address = customer.streetAddress
			+ customer.city
			+ customer.state;
		tooltipText = customer.fullName + ' ' + address;
		console.log(tooltipText);
		return tooltipText;
	}

	// good
	function createCustomerTooltip(customer) {
		var address,
			tooltipText;

		address = customer.streetAddress
			+ customer.city
			+ customer.state;
			
		tooltipText = customer.fullName + ' ' 
			+ address;

		console.log(tooltipText);

		return tooltipText;
	}
	```

  - Use indentation when making long method chains.

    ```javascript
    // bad
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // good
    $('#items')
      	.find('.selected')
        	.highlight()
        	.end()
      	.find('.open')
        	.updateCount();

    // bad
    var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
        .attr('width',  (radius + margin) * 2).append('svg:g')
        .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        .call(tron.led);

    // good
    var leds = stage.selectAll('.led')
        	.data(data)
      	.enter()
			.append('svg:svg')
        	.class('led', true)
        	.attr('width',  (radius + margin) * 2)
      	.append('svg:g')
        	.attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
        	.call(tron.led);
    ```

**[⬆ back to top](#table-of-contents)**


## Variables

  - Always use `var` to declare variables. Not doing so will result in global variables. We want to avoid polluting the global namespace. 

    ```javascript
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - Use one `var` declaration for multiple variables and declare each variable on a newline.

    ```javascript
    // bad
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
    ```

  - Declare unassigned variables last. This is helpful when later on you might need to assign a variable depending on one of the previous assigned variables.

    ```javascript
    // bad
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    var i, items = getItems(),
        dragonball,
        goSportsTeam = true,
        len;

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball,
        length,
        i;
    ```

  - Assign variables at the top of their scope when possible. This helps avoid issues with variable declaration and assignment hoisting related issues.

    ```javascript
    // bad
    function() {
		test();

		console.log('doing stuff..');
		
		//..other stuff..
		
		var name = getName();
		
		if (name === 'test') {
			return false;
		}
		
		return name;
    }

    // good
    function() {
      	var name = getName();

      	test();

      	console.log('doing stuff..');

      	//..other stuff..

      	if (name === 'test') {
        	return false;
      	}

      	return name;
    }

    // bad
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      return true;
    }

    // good
    function() {

      if (!arguments.length) {
        return false;
      }

      var name = getName();

      return true;
    }
    ```


### Hoisting

  - Variable declarations get hoisted to the top of their scope, their assignment does not.

    ```javascript
    // we know this wouldn't work (assuming there
    // is no notDefined global variable)
    function example() {
    	console.log(notDefined); // => throws a ReferenceError
    }

    // creating a variable declaration after you
    // reference the variable will work due to
    // variable hoisting. Note: the assignment
    // value of `true` is not hoisted.
    function example() {
      	console.log(declaredButNotAssigned); // => undefined

      	var declaredButNotAssigned = true;
    }

    // The interpreter is hoisting the variable
    // declaration to the top of the scope.
    // Which means our example could be rewritten as:
    function example() {
      	var declaredButNotAssigned;

      	console.log(declaredButNotAssigned); // => undefined

      	declaredButNotAssigned = true;
    }
    ```

  - Anonymous function expressions hoist their variable name, but not the function assignment.

    ```javascript
    function example() {
      	console.log(anonymous); // => undefined

      	anonymous(); // => TypeError anonymous is not a function

      	var anonymous = function() {
        	console.log('anonymous function expression');
      	};
    }
    ```

  - Named function expressions hoist the variable name, not the function name or the function body.

    ```javascript
    function example() {
      	console.log(named); // => undefined

      	named(); // => TypeError named is not a function

      	superPower(); // => ReferenceError superPower is not defined

      	var named = function superPower() {
        	console.log('Flying');
      	};
    }

    // the same is true when the function name
    // is the same as the variable name.
    function example() {
      	console.log(named); // => undefined

      	named(); // => TypeError named is not a function

      	var named = function named() {
        	console.log('named');
      	}
    }
    ```

  - Function declarations hoist their name and the function body.

    ```javascript
    function example() {
      	superPower(); // => Flying

      	function superPower() {
        	console.log('Flying');
      	}
    }
    ```

  - For more information refer to [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting) by [Ben Cherry](http://www.adequatelygood.com/)

**[⬆ back to top](#table-of-contents)**


## Blocks

  - Avoid single-line blocks.
  	
	```javascript
	// bad
	if (test) { count++; }

	// good
	if (test) {
		count++;
	}
	```

  - Use braces with all multi-line blocks.

    ```javascript
    // bad
    if (test)
      	return false;

    // good
    if (test) {
      	return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
      	return false;
    }
    ```

  - `else` blocks should be preceded by a newline.
  
	```javascript
	// bad
	if (customer) {
		// ...logic...
	} else {
		// ...logic...
	}

	// good
	if (customer {
		// ...logic...
	}
	else {
		// ...logic...
	}
	```

**[⬆ back to top](#table-of-contents)**


## Objects

  - Use the literal syntax for object creation.

    ```javascript
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - Don't use [reserved words](http://es5.github.io/#x7.6.1) as keys.

    ```javascript
    // bad
    var superman = {
      	default: { clark: 'kent' },
      	private: true
    };

    // good
    var superman = {
      	defaults: { clark: 'kent' },
      	hidden: true
    };
    ```

  - Use readable synonyms in place of reserved words.

    ```javascript
    // bad
    var superman = {
    	class: 'alien'
    };

    // bad
    var superman = {
    	klass: 'alien'
    };

    // good
    var superman = {
    	type: 'alien'
    };
    ```

**[⬆ back to top](#table-of-contents)**


## Arrays

  - Use the literal syntax for array creation

    ```javascript
    // bad
    var items = new Array();

    // good
    var items = [];
    ```
    
  - Use the `forEach` function to iterate over an array, unless the loop needs to call `break`.
   
  ```javascript
  // bad
  for(var i = 0; i < numbers.length; i++) {
  	total += numbers[i];
  }
  
  // good
  numbers.forEach(function (number) {
  	total += number;
  });
  ```
  
  - Use `for` ... `in` for loops that that need to call `break`.
  
  ```javascript
  for(var i = 0; i < results.length; i++) {
  	
  	if(results[i] === 'error') {
  		break;
  	}
  	
  	successes++;
  }
  ```
  
  - Use reverse `for ... in` for loops that need to remove items.

  ```javascript
  for(var i = array.length - 1; i >= 0; i--) {
                
    if (array[i] === "b") {
      array.splice(i, 1);
    }
  }
  ```

  
  - Use `find` when searching an array for a single element and `filter` or `filterBy` when searcing for multiple elements.

  - If you don't know array length use `Array.push`.

    ```javascript
    var someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  - When you need to copy an array use `Array.slice`. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```javascript
    var len = items.length,
        itemsCopy = [],
        i;

    // bad
    for (i = 0; i < len; i++) {
    	itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

  - To convert an array-like object to an array, use `Array.slice`.

    ```javascript
    function trigger() {
    	var args = Array.prototype.slice.call(arguments);
      
		...
    }
    ```

**[⬆ back to top](#table-of-contents)**


## Strings

  - Use single quotes `''` for strings

    ```javascript
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

  - Strings longer than 80 characters should be written across multiple lines using string concatenation.
  
    ```javascript
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // good
    var errorMessage = 'This is a super long error that was thrown because ' +
      	'of Batman. When you stop to think about how Batman had anything to do ' +
      	'with this, you would get nowhere fast.';
    ```

**[⬆ back to top](#table-of-contents)**

## Enums

  - Avoid 'magic numbers', instead using enum values.
   
  ```javascript
  // bad
  function UserScreen() {
  	var _this = this;
  	
  	this.screenCde = 3;
  }
  
  // good
  function UserScreen() {
  	var _this = this;
  	
  	this.screenCde = fpiEnums.screens.user;
  }
  ```
  
  - Enum values that share a name with a Javascript keyword must be defined and used via string property access.
   
  ```javascript
  // bad
  var dataOperations = {
  	delete: 3,
  };
  
  // good
  var dataOperations = {
  	'delete': 3,
  };
  
  // bad
  var isDelete = row.dataOperation == dataOperations.delete;
  
  // good
  var isDelete = row.dataOperation == dataOperations['delete'];
  ```

**[⬆ back to top](#table-of-contents)**

## Properties

  - Use dot notation when accessing properties.

    ```javascript
    var luke = {
    	jedi: true,
    	age: 28
    };

    // bad
    var isJedi = luke['jedi'];

    // good
    var isJedi = luke.jedi;
    ```

  - Use subscript notation `[]` when accessing properties with a variable.

    ```javascript
    var luke = {
    	jedi: true,
    	age: 28
    };

    function getProp(prop) {
    	return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

**[⬆ back to top](#table-of-contents)**


## Conditional Expressions & Equality

  - Use `===` and `!==` over `==` and `!=`.
  
  - Conditional expressions are evaluated using coercion with the `ToBoolean` method and always follow these simple rules:

    + **Objects** evaluate to **true**
    + **Undefined** evaluates to **false**
    + **Null** evaluates to **false**
    + **Booleans** evaluate to **the value of the boolean**
    + **Numbers** evaluate to **false** if **+0, -0, or NaN**, otherwise **true**
    + **Strings** evaluate to **false** if an empty string `''`, otherwise **true**

    ```javascript
    if ([0]) {
      	// true
      	// An array is an object, objects evaluate to true
    }
    ```

  - Use shortcuts.

    ```javascript
    // bad
    if (name !== '') {
      	// ...stuff...
    }

    // good
    if (name) {
      	// ...stuff...
    }

    // bad
    if (collection.length > 0) {
      	// ...stuff...
    }

    // good
    if (collection.length) {
      	// ...stuff...
    }
    ```

  - For more information see [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll

  - Use multiple lines for complex conditionals, starting each line with a conditional operator (e.g. `&&`).

	```javascript
	// bad
	function isReadOnly() {
		return _this.hasLock && _this.status !== 'readonly' && !view.isReadOnly();
	}

	// good
	function isReadOnly() {

		return _this.hasLock 
			&& _this.status !== 'readonly' 
			&& !view.isReadOnly();
	}
	```
	
  - Never use multiline conditionals in `if` or `while` statements.  Instead, assign the result of the multiline conditional to an intermediary variable.
   
  ```javascript
  // bad
  function save() {
  
  	if(_this.hasLock 
		&& _this.status !== 'readonly' 
		&& !view.isReadOnly()) {
		// ...stuff...	
	}
  }
  
  // good
  function save() {
  	
  	var canSave = _this.hasLock 
		&& _this.status !== 'readonly' 
		&& !view.isReadOnly();
		
	if(canSave) {
		// ...stuff...
	}
  }
  ``` 
  
  - Use multiple lines for complex ternaries, starting each line with a ternary operator (`?` or `:`).
   
  ```javascript
  // bad
  function getCustomer(id) {
  	
  	return customerCache.hasCustomer(id) ?
  		customerCache.getCustomer :
  		customerService.getCustomer;
  }
  
  // good
  function getCustomer(id) {
  	
  	return customerCache.hasCustomer(id) 
  		? customerCache.getCustomer 
  		: customerService.getCustomer;
  }
  ```

**[⬆ back to top](#table-of-contents)**


## Type Inspection, Casting, & Coercion

  - Use the `Object.is<Type>` functions for simple type inspection (e.g. `Object.isFunction`).

  - Perform type coercion at the beginning of the statement.
  
  - Strings:

    ```javascript
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = '' + this.reviewScore + ' total score';

    // good
    var totalScore = this.reviewScore + ' total score';
    ```

  - Use `parseInt` for Numbers and always with a radix for type casting.

    ```javascript
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number(inputValue);

    // good
    var val = parseInt(inputValue, 10);
    ```

  - Booleans:

    ```javascript
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean(age);

    // good
    var hasAge = !!age;
    ```

**[⬆ back to top](#table-of-contents)**


## Promises

  - Always use promises for asynchronous code.
   
  ```javascript
  // bad 
  function renderWidgets(widgets) {
  	_this.widgets(widgets);
  	
  	setInterval(function () {
  		
  		if(getRenderedWidgetCount() === widgets.length) {
  			// ...stuff...
  		}
  	}, 100);
  }
  
  // good
  function renderWidgets(widgets) {
  	var dfdRender = $.Deferred();
  
  	_this.widgets(widgets);
  	
  	setInterval(function () {
  		
  		if(getRenderedWidgetCount() === widgets.length) {
  			dfdRender.resolve();
  		}
  	}, 100);
  	
  	return dfdRender.promise();
  }
  ```
  
  - Asynchronous functions must return promises, not deferreds, so they can control the resolution.
   
  ```javascript
  // bad
  function asyncOperation() {
  	var dfdDone = $.Deferred();
  	
  	// ...stuff...
  	
  	return dfdDone;
  }
  
  // good
  function asyncOperation() {
  	var dfdDone = $.Deferred();
  	
  	// ...stuff...
  	
  	return dfdDone.promise();
  }
  ```

  - Each function in a promise chain should by preceded by a newline.

	```javascript
	// bad
	return makeServiceCall().then(function (data) {
		return parseData(data);
	}).then(function (data) {
		console.log(data);
		
		return data;
	});

	// good
	return makeServiceCall()
		.then(function (data) {
			return parseData(data);
		})
		.then(function (data) {
			console.log(data);
			
			return data;
		});
	```
	
  - If one path returns a promise, all paths must return promises.
   
  ```javascript
  // bad
  function save(data) {
  
  	if(isValid) {
  		return Service.save(data)
  			.then(function (result) {
  				return true;
  			});
  	}
  	else {
  		return false;
  	}
  }
  
  // good
  function save(data) {
  
  	if(isValid) {
  		return Service.save(data)
  			.then(function (result) {
  				return true;
  			});
  	}
  	else {
  		return $.Deferred().reject(false);
  	}
  }
  ```
  
  - Use `when` to combine a fixed-length series of promises.
   
  ```javascript
  function loading() {
  	return $.when(loadLookups(lookups), loadModals(modals));
  }
  ```
  
  - Use `whenAll` to combine a varible-length array of promises.
   
  ```javascript
  function loading() {
  	var loadPromises = loadChildWidgets();
  
  	return $.whenAll(loadPromises);
  }
  ```

**[⬆ back to top](#table-of-contents)**


## Events

  - When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event. For example, instead of:

    ```js
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId) {
      	// do something with listingId
    });
    ```

    prefer:

    ```js
    // good
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function(e, data) {
      	// do something with data.listingId
    });
    ```

  **[⬆ back to top](#table-of-contents)**


## Commas

  - Avoid leading commas: 

    ```javascript
    // bad
    var once
      , upon
      , aTime;

    // good
    var once,
        upon,
        aTime;

    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
      	firstName: 'Bob',
      	lastName: 'Parr',
      	heroName: 'Mr. Incredible',
      	superPower: 'strength',
    };
    ```

  - Use the additional trailing comma:  

    ```javascript
    // bad
    var hero = {
      	firstName: 'Kevin',
      	lastName: 'Flynn'
    };

    var heroes = [
      	'Batman',
      	'Superman'
    ];

    // good
    var hero = {
      	firstName: 'Kevin',
      	lastName: 'Flynn',
    };

    var heroes = [
      	'Batman',
      	'Superman',
    ];
    ```

**[⬆ back to top](#table-of-contents)**


## Semicolons

  - End lines with semicolons.

    ```javascript
    // bad
    (function() {
      	var name = 'Skywalker'
      	
      	return name
    })()

    // good
    (function() {
      	var name = 'Skywalker';
      	
      	return name;
    })();

    // good (guards against the function becoming an argument when two files with IIFEs are concatenated)
    ;(function() {
      	var name = 'Skywalker';
      	
      	return name;
    })();
	```

  - [Read more](http://stackoverflow.com/a/7365214/1712802).

**[⬆ back to top](#table-of-contents)**


## Comments

  - Use `///` for multiline comments. Use `* *` to break the comments up by idea.
  
	```javascript
	// bad
	// Returns a tooltip string for a customer
	// Includes name, address, city, state,
	// branch, and phone
	// Additional fields are configurable
	function createCustomerTooltip(customer) {
	
	}
	
	// good
	///
	/// Returns a tooltip string for a customer
	/// * Includes name, address, city, state,
	///    branch, and phone
	/// * Additional fields are configurable
	function createCustomerTooltip(customer) {		
		
	}
	
	```

  - Comments describing functions can specify types and values for parameters and return values.

	```javascript
	// good
	///
	///  make() returns a new element
	///  based on the passed in tag name
	///
	///  @param <String> tag
	///  @return <Element> element
	function make(tag) {
	      ...
	
	      return element;
	}
	```

  - Use `####` for structural comments that describe multiple lines of code within a function.

	```javascript
	// good
	function createCustomerTooltip(customer) {
		var address,
			city,
			state
			tooltipText;

		//#### Create the address string ####
		city = getLookupValue(lookups.city, customer.cityCde);
		state = getLookupValue(lookups.state, customer.stateCde);

		address = customer.streetAddress
			+ city.name
			+ state.name;
			
		//#### Create and return tooltip string ####
		tooltipText = customer.fullName + ' ' 
			+ address;

		console.log(tooltipText);

		return tooltipText;
	}
	```

  - Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment.

    ```javascript
    // bad
    var active = true;  // is current tab

    // good
    // is current tab
    var active = true;

    // bad
    function getType() {
      	console.log('fetching type...');
      	// set the default type to 'no type'
      	var type = this._type || 'no type';

      	return type;
    }

    // good
    function getType() {
      	console.log('fetching type...');

      	// set the default type to 'no type'
      	var type = this._type || 'no type';

      	return type;
    }
    ```

  - Prefixing your comments with `HACK` or `TODO` helps other developers quickly understand if you're pointing out a problem that needs to be revisited. These are different than regular comments because they are actionable. 

  - Use `// HACK:` to note temporary fixes.

    ```javascript
    function formatDate(date) {

      	// HACK: Temporary solution, TP - B1234
      	return hackToFixDateTime(date);
    }
    ```

  - **Note:** If you're going to check in hacky code (and you had better have a good reason to do so), make sure to log an item in Teampulse to re-visit and update the code.  Include the Teampulse ID here.	

  - Use `// TODO:` to describe future enhancements or requirements.

    ```javascript
    function Calculator() {

      	// TODO: total should be configurable by an options param
      	this.total = 0;

      	return this;
    }
  ```


  ### Regions 

  - Use regions to group similar classes or functions, making it easier to navigate through larger files.

  - Include a newline between the region beginning/end and the enclosed functions.

	```javascript
	function Collateral() {
		var _this = this;	

		//#region Private Functions

		function getComponents() {

		}

		function getLinkedLoans() {

		}

		//#endregion

		//#region Public Functions

		this.create = function () {

		};		

		this.update = function () {
	
		};

		this.delete = function () {

		};

		//#endregion
	}
	```

  - **Note:** Don't use regions inside a function.  An individual function should not be big enough to require this.
  
  - **Note:** Javascript regions require the [Web Essentials](http://vswebessentials.com/) extension for Visual Studio. 

**[⬆ back to top](#table-of-contents)**

## Abbreviations

- The following domain-specific abbreviations are considered standard for use in property names, function names, etc:
 
  + ws: Workspace
  + scn: Scenario
  + secDoc: Security Document
  + dw: Data Wizard

**[⬆ back to top](#table-of-contents)**

## Third Party 

### jQuery

  - Prefix jQuery object variables with a `$`.

    ```javascript
    // bad
    var sidebar = $('.sidebar');

    // good
    var $sidebar = $('.sidebar');
    ```

  - Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      	$('.sidebar').hide();

      	// ...stuff...

      	$('.sidebar').css({
        	'background-color': 'pink'
      	});
    }

    // good
    function setSidebar() {
      	var $sidebar = $('.sidebar');
      	
		$sidebar.hide();

      	// ...stuff...

      	$sidebar.css({
        	'background-color': 'pink'
      	});
    }
    ```

  - For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  
  - Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

  - Use `on` to add event handlers - not `bind` or `live`. 
   
  - Use `_this.UI` as the context when binding events for ViewModel types.  This prevents unintentionally overlapping handlers.  These handlers must be registered in the ViewModel's `loaded` function.
  
  ```javascript
  // bad
  function SearchWidget() {
  	var _this = this;
  	
  	// ...stuff...
  	
  	$('.search-widget').on('click', 'button', someFunction);
  }
  
  // good
  function SearchWidget() {
  	var _this = this;
  	
  	// ...stuff...
  	
  	_this.UI.on('click', 'button', someFunction);
  }
  ```
  
  - **Note:** The exceptions to this are static event handlers, which are only required for events on widgets that appear in large numbers.

**[⬆ back to top](#table-of-contents)**


### Knockout

  - Use `ko.unwrap` and `ko.unwrapPeek` to access a value that may or may not be observable.
  
	```javascript

	// bad
	var value = ko.isObservable(property) ? property() : property;

	// bad
	var value = ko.getFieldValue(data, fieldName);

	// good
	var value = ko.unwrap(property);

	// good
	var value = ko.unwrap(data[fieldName]);

	```

  - **Note:** `ko.getFieldValue` is deprecated and should not be used. 
  
- Use `ko.pureComputed` over `ko.computed` by default.  `ko.computed` should only be used when the `read` function has side effects, which is uncommon.

- Always pass an object as the argument when creating a computed observable instead of just a `read` function.  	This makes it easier to extend in the future.

```javascript
// bad
var isVisible = ko.computed(function () {
	// ...stuff...
});

// good
var isVisible = ko.computed({
	read: function () {
	
	},
});
```

**[⬆ back to top](#table-of-contents)**


### Require

  - Inline `require` calls cannot be used - dependencies must be defined at the top of a module.
  
	```javascript

	// bad
	define('CustomerWidget',
		[],
		function () {
		
			function CustomerWidget() {
				var _this = this;
				
				function loadWidget() {
					this.popover = require('Popover').makePopover();	
				}
			}
		});
	
	//good
	define('CustomerWidget',
		['Popover'],
		function (Popover) {
		
			function CustomerWidget() {
				var _this = this;
				
				function loadWidget() {
					this.popover = Popover.makePopover();	
				}
			}
		});

	```

  - Modules must not reference other modules that they do not use.

**[⬆ back to top](#table-of-contents)**


## Appendices

### Revision History

Date       | Modified By   | Version | Note
---------- | ------------- | ------- | ------------------------------
11/17/2014 | Tim Beck      | 1.0     | Revisions from initial feedback.
02/17/2016 | Tim Beck      | 1.1     | Updated for Sprint 1.

### Resources

**Compatibility**

- [Kangax](https://twitter.com/kangax/)'s ES5 [compatibility table](http://kangax.github.com/es5-compat-table/)

**Performance**

  - [On Layout & Web Performance](http://kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](http://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](http://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](http://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](http://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](http://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](http://jsperf.com/ya-string-concat)

**Read This**

  - [Annotated ECMAScript 5.1](http://es5.github.com/)

**Tools**

  - Code Style Linters
    + [JSHint](http://www.jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/jshintrc)
    + [JSCS](https://github.com/jscs-dev/node-jscs) - [Airbnb Style Preset](https://github.com/jscs-dev/node-jscs/blob/master/presets/airbnb.json)

**Other Styleguides**

  - [Google JavaScript Style Guide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
  - [jQuery Core Style Guidelines](http://docs.jquery.com/JQuery_Core_Style_Guidelines)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwldrn/idiomatic.js/)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on Github](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban

**Books**

  - [JavaScript: The Good Parts](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](http://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](http://manning.com/vinegar/) - Ben Vinegar and Anton Kovalyov

**Blogs**

  - [DailyJS](http://dailyjs.com/)
  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](http://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](http://weblog.bocoup.com/)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](http://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [Dustin Diaz](http://dustindiaz.com/)
  - [nettuts](http://net.tutsplus.com/?s=javascript)

**[⬆ back to top](#table-of-contents)**

### License

(The MIT License)

Copyright (c) 2014 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
