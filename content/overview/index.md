## Overview

Angular cli is a command line interface to scaffold and build angular apps using nodejs style ( common js) modules.

Not only it provides you scalable project structure, instead it handles all common tedious tasks for you
out of the box.

### Here are some goodies

1. Nodejs style require module , so you can simply say

  ```language-javascript
  require('controllers');
  ```
2. Support for coffeescript.
3. Asset pipelining.
4. Css Preprocessors.
  * Less
  * Stylus
  * Compass
5. Auto annotated angular components, so you no more have to manage DI annotations.

  ```language-javascript
  // EARLIER
  app.controller('home',['$scope',function($scope){

  }]);
  // NOW
  app.controller('home',function($scope){

  });
  ```
6. App Initializers

  > biggest dilemma to work with angular apps is how to   fetch and preserve data before starting angular app.

  > AND INITIALERS LET YOU DO THAT OUT OF BOX.

7. Testing First.
8. Command line blueprints to get you up and running in seconds.
