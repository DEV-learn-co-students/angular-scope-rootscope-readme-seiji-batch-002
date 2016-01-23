# $scope and $rootScope

## Overview

## Objectives

- Describe what a $scope is
- Describe what $rootScope is
- Describe how Angular utilises Prototypal Inheritance
- Create a $scope variable
- Bind the $scope variable to the View

## $scope

You might've noticed the magic of `$scope` in the last lesson - an object that we can assign values to and they appear in our view. `$scope` is named by Angular - we can't change the name of it, so make sure you refer to it as `$scope`! 

Angular introduces scopes into our application. Whenever we have a new instance of a controller, that controller has a `$scope`. Everything inside our controller can access this scope, however anything outside cannot. `$scope`s can access their parent scope.

## Using $scope in our views

We can access every property of `$scope` that we set in the controller inside our views. This is done using the `{{ }}` syntax that we used in our first lab. All we need to do is put the property key inside of the double curlys - such as for `$scope.name`, we use `{{ name }}`. We can also use `.` to access properties inside properties (for example, an object).

For example:

```js
function MainController($scope) {
  $scope.contact = {
    name: 'Bill Gates',
    phone: '01234567890'
  };
  
  $scope.year = '2016';
}
```

```html
<div ng-controller="MainController">

  <h2>{{ contact.name }}</h2>
  <h4>{{ contact.phone }}</h4>

  <div>
    Copyright {{ year }}.
  </div>
</div>
```

This would render out:

```html
<div ng-controller="MainController">

  <h2>Bill Gates</h2>
  <h4>01234567890</h4>

  <div>
    Copyright 2016.
  </div>
</div>
```

Neat, huh? 

However, if we tried to access items outside of our controller, such as:

```html
<div ng-controller="MainController">

  <h2>{{ contact.name }}</h2>
  <h4>{{ contact.phone }}</h4>

  <div>
    Copyright {{ year }}.
  </div>
</div>

{{ year }} {{ name }}
```

All we'd get rendered is:
 
 
```html
<div ng-controller="MainController">

  <h2>Bill Gates</h2>
  <h4>01234567890</h4>

  <div>
    Copyright 2016.
  </div>
</div>

{{ year }} {{ name }}
```

![Angular Scopes](https://docs.angularjs.org/img/guide/concepts-scope.png)

Look at the example above - each red rectangle is a scope. If we look at the first rectangle for the HTML element with `ng-controller` - this is currently what we have in our application. From this `$scope`, we'd be able to access the parent `$scope` (the big rectangle around the whole image), but not the `$scope` of the second HTML element with `ng-controller`.

### $rootScope

We also have the `$rootScope` - this is the first scope in our application. All of our `$scope`'s will end up linking to this scope eventually. Not to worry about this yet, you'll come to see it a lot more later on.
 
## What else does $scope offer?

`$scope` isn't just an object that can assign values to the view - it's also an extremely powerful API that allows us to do things, such as communicating between scopes, keep track of data state, watching for changes and much more - but we'll touch on this later.