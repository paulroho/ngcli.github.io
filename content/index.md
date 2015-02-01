Angular cli is a command line interface to scaffold and build angular apps using nodejs style (commonJs) modules.

Not only it provides you scalable project structure, instead it handles all common tedious tasks for you
out of the box.

## Goodies

1. Nodejs style require module , so you can simply say
  ```javascript
  require('controllers');
  ```
2. Support for coffeescript.
3. Asset pipelining.
4. Css Preprocessors.
  * Less
  * Stylus
  * Compass
5. Auto annotated angular components, so you no more have to manage DI annotations

  ```javascript
  // EARLIER
  app.controller('home',['$scope',function($scope){

  }]);
  // NOW
  app.controller('home',function($scope){

  });
  ```

6. App Initializers
  > Biggest dilemma to work with angular apps is how to fetch and preserve data before starting angular app.AND INITIALERS LET YOU DO THAT OUT OF BOX.

7. Testing First.
8. Command line blueprints to get you up and running in seconds.
9. ngcli addons to add your own conventions and build tasks to angcli.

# Getting Started

Angular cli ships with handful of commands to set up and build your project from scratch, run below command to see if you have successfully
installed angcli globally.

```"javascript
ng version
```
this will output the running version on your machine, something like -

```
Version 0.0.3
```
If above command worked fine and version on your machine matches to the current version at the top of this page, then you are good to go.

## Prerequisites

Angular cli makes the best use of existing tools by bundling them together, i have listed all the required and optional tools which are required
before you get your hands dirty with **angcli**.

### bower

Bower is dependency manager for web, similar to npm for node. **angcli** uses bower to manage third party dependencies like angularjs,
angular-routes and many more.

Visit [http://bower.io/][f65bad8b] or install it.

```"markup
npm install -g bower
```

That's all you need to get started with angular cli, you may need your favourite css pre-processor like Sass, Less or Stylus. Less and stylus
does not require any installation, whereas you have to install ruby and sass to use awesomeness provided by Sass/Compass.

## Commands

### List of commands

```"markup
ng -h
```

above command will list all the available commands and their description, should look something like below.

![](img/nghelp.png)

Let's discuss these commands in detail

### new

```"markup
ng new <path_to_project>

```

Above command will create a new project for you by installing required dependencies using bower and npm.

### build

```"markup
ng build

```
Above command will build your project inside /dist folder, it outputs 3 different files and assets by default.

* vendor.js (Concatenated 3rd party libraries).
* vendor.css (Concatenated 3rd party css files).
* app.js (Concatenated version of your controllers, directives and other entities. )
* app.css (Concatenated version of styles).
* index.html (Your main html file).

### serve

```"markup
ng serve
```
It works same as build command, in addition it runs a local server with livereload.

### generate

Generator helps you in generating controllers, directives,initializers, filters,services and factories right from your command line.

```"markup
ng generate controller home
```

will create 2 files

1. **home.js** inside /controllers
2. **home.js** inside /tests/spec/controllers

Also, you can run

```"markup
ng generate directive <name>
ng generate initializer <name>
ng generate filter <name>
ng generate service <name>
ng generate factory <name>
```

### test

```"markup
ng test
// OR
ng test -w // (run tests and watch for changes)
```

Above will run karma unit tests.

### hook

```"markup
ng hook <hook_name>
```

Run any hook using its name, make sure you have installed the hook you are about to execute.

## Project Structure

Angular cli follows simple/flat project structure.

```
├── app/
│ ├── assets/
│ ├── controllers/
│ ├── directives/
│ ├── filters/
│ ├── hooks
│ │ ├── config.js
│ │ ├── index.js
│ │ ├── run.js
│ ├── initializers/
│ ├── services/
│ ├── store/
│ ├── styles/
│ ├── templates/
│ ├── app.js
│ ├── index.html
│ ├── constants.js
│ ├── routes.js
│── bower_components/
│── core/
│ ├── boot.js
│── dist/
│── vendors/
│ ├── vendors.js
│ ├── vendors.css
│── node_modules/
│── tests/
│── .jshintrc
│── bower.json
│── karma.conf.js
│── ngconfig.json
│── webpack.config.js
│── package.json

```

Lets discusss above project structure in detail now.

### app

App folder contains all required directories and files you will be working with most of the time.

#### app/assets

Assets can contain any static files from images, fonts to video and audio.

#### app/controllers

This directory contains list of controllers created by you, **index.js** is reserved for indexing which
means you cannot create controller inside index.js file.

**Example**

```javascript
/* @ngInject */
module.exports = function($scope) {
  $scope.greeting = 'Hello world! This is ngCLI Boilerplate.';
};
```

#### app/directives, app/filters, app/initializers, app/services, app/store

List of entities and follows same rules as controller directory

#### app/hooks

Angular js app/routing cycle events/hooks are stored inside this directory, by default it contains 2 files
run.js and config.js.

#### app/templates

List of angular templates with .html file extension.

#### app.js

app.js is the entry point to your app, which extends core/boot.js to start angular app and register all
entities.

#### constants.js

You can store any constants inside this file to keep your code clean, if I said constants if means they cannot be changed or overridden
at runtime.

#### routes.js

Your app routes.

**Example**

```javascript
var routeMap;

routeMap = [{
  url: '/',
  templateUrl: "welcome.html",
  controller: 'welcomeCtrl'
}];

module.exports = routeMap;

```

#### index.html

Your app entry point .html file.


### core

Core is something that ships with angcli, and for now it only contains one file boot.js, which bootstraps angular app.

### bower_components

Bower dependencies

### dist

Build folder, this folder contains final build files which are

* **vendor.js**
* **vendor.css**
* **app.js**
* **index.html**
* **app.css**

### vendors

Manages 3rd party dependencies.

#### vendors.js

require third party script files inside this file.

```javascript
require("angular");
require("angular-route");
```

#### vendors.css

require third party css files inside this file.

```css
@import url("/path/to/file");
```
All of the above imports will be inlined inside `dist/vendor.css`.


### node_modules

npm dependencies

### .jshintrc

Jshint config file to lint js code

### karma.conf.json

Config file for karma unit tests.

### ngconfig.json

Angular cli config file , let's spend some time understanding this file

```
{
  "app_name": "angularApp",
  "uglify_js": true,
  "port": 3080,
  "live_reload": true,
  "lrPort": 35729,
  "run_server": true,
  "host": "127.0.0.1"
}
```

#### app_name

Your angular module name, by keeping app_name here it makes it easy for you to change at any point of time, without messing up number of
files.

#### uglify_js

Boolean whether to minfiy js or not.

#### port

Server port number.

#### lrPort

Live Reload port number.

#### host

Server host

#### live_reload

Whether you want to reload server on file change.

#### run_server

Serve files using inbuilt local server


# Ecosystem

So far we have spent time understanding

* what is ngcli ?
* how to run commands ?
* directory structure and important files

Now we will talk about the ecosystem, which is very important to debug your apps, and add your own quick hacks.

## CommonJs

angcli uses [webpack][db0c6c83] enabling node js style module require.

3rd party vendor libraries get bundled inside dist/vendor.js, whereas your local app files becomes part of dist/app.js

## ngConfig

ngConfig is the place where your app config lives in, it can be used for global settings like **app_name**, or can be used by hooks to specifiy local settings for example **auto_index** used by ng-index-entities.

As ngconfig is available to all hooks, it becomes the centric point to manage all settings.

## Extending Boot

app/app.js is the entry point to your angular app and it extends core/boot.js (which is responsible for bootstraping angular app).

**app/app.js**
```javascript
var boot;
boot = require("../core/boot");
boot();
require("./validations");
require("./filters");
require("./services");
require("./store");
require("./directives");
require("./templates");
require("./controllers");

```

This is how it looks after removing all comments, It is quite obvious that your app will have extra dependencies, so instead of running down to core/boot.js and add dependencies there, you can simply pass an array of dependencies to your boot method.

Let's start by installing ng-table using bower

```
bower install ng-table --save
```
Now you can simple require it and extend your boot method by passing ngTable as required dependency.

**app/app.js**
```
require("ng-table");
boot(["ngTable"]);
```
and you are good to go.

You can simply pass the name of hook you want to disable permanently for this project. You may reference npm to find hook-name.

## Understanding Vendors

It is really important to understand the difference between **dist/vendor.js** and **dist/app.js**, all 3rd libraries using bower should be part of vendor.js resulting in faster incremental builds and all local source files should be part of app.js.

Deciding which files will be part of vendor file is done using vendors/vendors.js inside vendors key.

```
require("angular");
require("angular-routes");
...
```

Requires mentioned inside `vendors/vendors.js` will be bundled inside dist/vendors.js .

## Initializers

Initializers are not part of angular by default but for realtime apps it is very important to fetch some data from server before booting angular app.

### Reading

Initializers can be used to read data from the server or from anywhere for that matter, and should return a promise after
doing its job.

Example

```javascript
module.exports = {
  provider: 'config',
  resolve: /*@ngInject*/ function($q,$http){
   var deferred = $q.defer();
   $http.get('app/config').success(function(){
     deferred.resolve('i pinged server');
   });
   return deferred.promise;
  }
}
```

### Storing

You may want to store the above config and need some way to access it across your angular app. It can be done quite easily. All initializers get converted to constants after boostraping angular app. Which means you can inject them to
your controllers, directives infact anywhere.

```javascript
module.exports = {
  provider: 'config',
  resolve: /*@ngInject*/ function($q,$http){
    var deferred = $q.defer();
    $http.get('app/config').success(function(config){
      deferred.resolve({data:config});
    });
    return deferred.promise;
  }
}
```
Now I can access it inside my controller

```javascript
module.exports = function($scope,config){
  console.log(config.data);
}
```

## Indexing Entities

All angular entities like controllers, directives etc have index.js files inside their root folder. This is the place where all entities get registered so that they can be used inside angular app.

Let's take this example

**controllers/home.js**

```javascript
/**
@name: homeController
*/
/*@ngInject*/
module.exports = function($scope){
  $scope.greeting = 'Hi i am homeCtrl';
};
```
Now we will register this module as a controller inside index.js file

**controllers/index.js**

```javascript
app = angular.module('{@= app_name @}')
app.controller('homeCtrl',require('./home'));
```

#### What's going on ?

As angular cli uses node style modules every entity is a module and can be require anywhere, now in order to tell angular that home.js is a homeCtrl we need to register this as a controller, this is what we do inside index.js file inside the root of every entity.

Now it can a tedious task to register entities urself by going back and forth again.So generator auto index entities for you.

## Generators

Generators helps you in creating entities right from your command line and below is the list of generators.

1. controller
2. directive
3. filter
4. factory
5. services
6. initializer

## Build

Building your source files into a bundle is done using broccoli and webpack.

### WebPack

Webpack converts commonjs modules to something what browsers understands. 

### Broccoli Js

Broccoli Js is responsible for running all build tasks, even webpack transformations are part of broccoli tasks.

## Constants

Almost every keep needs some constants to keep code clean and dry. Angular constants are injectable services which may be overhead for a simple constant like base_url.

angcli ships with a special file called app/constants.js , here you can define key/value pairs which you can later use inside your angular app. Let's start with an example.

**app/constants.js**
```javascript
var CONSTANTS;

CONSTANTS = {
  "base_url": "http://example.com"
};

module.exports = CONSTANTS;

```

Using above constant

**app/store/user.js**
```javascript
module.exports = function($http){
  return{
    getUserData: function(){
      var userUrl = "{@= LET.base_url @}/user"
      return $http.get(userUrl);
    }
  }
}
```
Here is the special syntax to access your constants anywhere inside your angular app. {@= LET.[constant_name] @} , and it will be replaced with the value of constant on build time ensuring there is no extra manipulation on runtime and it keeps your code dry.

# Hooks

## What are hooks ?

Hooks are npm modules with special configuration to work with angular cli. Below is an example of hello world hook.

**package.json**

```
"ng-hook": {
  "name": "ng-hello-world",
  "hook-for": "build",
  "weight": 1
}  
```

With above key value pair inside your package.json will help you in defining ng-hooks.

1. **name** - Name is required and should be unique.
2. **hook-for** - Every hook is attached to some process/command, available commands.
   * build
   * serve
   * new
   * generate:controller
   * generate:service
   * generate:factory
   * generate:service
   * generate:filter
   * generator:initializer
   * test
3. **weight** - Smaller the weight , earliest it will be executed.
4. **after (optional)** - An array of hooks after which you want your hook to be executed.

## Using hooks

You can browse and install hooks using npm , list of available hooks can be find here on [https://github.com/ngCli](https://github.com/ngCli).

## Writing hooks

Writing hook is pretty simple , all you need is an **init** method inside your index.js file and make that method return Promise and that's all. You can browse existing hooks for example.

Sample hook file

```javascript
(function(){
  "use strict";

  var Promise = require("bluebird");
  var Hook = function () {};
  var hook = new Hook();

  Hook.prototype.init = function(output,ngconfig,args,store){
    var defer = Promise.defer();
    /*
      Your code goes here
    */
    return defer.promise;
  };
  module.exports = hook;

}).call(this);

```

It accepts 4 arguments.

1. **output** - Output of last hook
2. **ngconfig** - ngconfig object.
3. **args** - Command arguments
4. **store** - Incremental store to save and fetch data from.

# Tutorials

1. Angular Cli - Getting Started on http://amanvirk.me/angular-cli-getting-started/
2. Upgrading ngCli to v3 http://amanvirk.me/upgrading-ngcli-to-v3/

# ChangeLog

## Version 0.0.3

1. Changed ngconfig , removed pre-defined options

**Old File**
  ```
{
    "preffered_coding_style": "Javascript",
    "css_preprocessor": "compass",
    "app_name": "angularApp",
    "uglify_js": true,
    "prefix_css": true,
    "minify_css": true,
    "port": 3080,
    "live_reload": true,
    "run_server": true,
    "host": "127.0.0.1",
    "vendors": [
        {
            "angular-deferred-bootstrap": "angular-deferred-bootstrap"
        },
        {
            "angular": "angular"
        },
        {
            "angular-route": "angular-route"
        }
    ],
    "hooks-to-ignore": []
}
  ```
**New File**

```
{
  "app_name": "angularApp",
  "uglify_js": true,
  "port": 3080,
  "live_reload": true,
  "lrPort": 35729,
  "run_server": true,
  "host": "127.0.0.1"
}
```

2. Replaced browserify with [webpack][db0c6c83].
3. Replace [gulp][5949351f] with [broccoli][db0c6c84].
4. Added vendors folder with vendors.js and vendors.css .
5. Added support to create ngcli-addons.
6. Removed ng-hooks ignore options.


## Version 0.0.1

1. Ability to run hooks in sequence depending upon their weight and after dependency.
2. Option to remove hooks using ngconfig file.
3. Added initializers.
4. Generators for directives,controllers,services,factories,filters and initializers.
5. Unit testing using karma.
6. All entities are testable.
7. Browserify and gulp for build tasks.
8. Less,Sass,Stylus and plain css supported.
9. cp assets supported.
10. Well tested with bower components.

[5949351f]: http://gulpjs.com/ "here"
[f65bad8b]: http://bower.io/ "http://bower.io/"
[db0c6c83]: http://webpack.github.io/docs/ "webpack"
[db0c6c84]: https://github.com/broccolijs/broccoli "broccolijs"
