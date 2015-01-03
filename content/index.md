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
9. nghooks to add your own conventions to angcli.

# Getting Started

Angular cli ships with handful of commands to set up and build your project from scratch, run below command to see if you have successfully
installed angcli globally.

```"javascript
ng version
```
this will output the running version on your machine, something like -

```
Version 0.0.1
```
If above command worked fine and version on your machine matches to the current version at the top of this page, then you are good to go.

## Prerequisites

Angular cli makes the best use of existing tools by bundling them together, i have listed all the required and optional tools which are required
before you get your hands dirty with **angcli**.

### gulp

Gulp is quite similar to Grunt but with different approach, it uses streams to run build tasks. You can read more about gulp [here][5949351f]. Or simply install it.

```"markup
npm install -g gulp
```

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
* app.js (Concatenated version of your controllers, directives and other entities. )
* app.css (Concatenated version of styles).

### serve

```"markup
ng serve
```
It works same as build command, in addition it runs a local server with livereload.

### sync

```"markup
ng sync
```

Angular cli behind the scenes runs a series of hooks which empowers angcli commands, These hooks are bundled with angcli and can also be
part of your app.

In short hooks are npm modules with some special configuration and init method.

For example

ng new command is a combination of following hooks.

1. **ng-project-blueprint** - To create project blueprint.
2. **ng-scaffold-coffee** - To create required files in coffeescript.
3. **ng-scaffold-js** - To create required files in javascript.
4. **ng-dependencies-install** - Install list of dependencies inside bower.json and welcome.json.

Above hooks are bundled with angcli, whereas you can also add your own hooks which are just npm modules. You can read more about hooks inside <placeholder> hooks section.

### generate

Generator helps you in generating controllers, directives,initializers, filters,services and factories right from your command line.

```"markup
ng generate controller home
```

will create 2 files

1. **homeCtrl.js** inside /controllers
2. **homeCtrl.test.js** inside /tests/spec/controllers

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
│ ├── constants.js
│ ├── routes.js
|── bower_components/
|── core/
│ ├── boot.js
|── dist/
|── node_modules/
|── tests/
|── .jshintrc
|── bower.json
|── index.html
|── karma.conf.js
|── ngconfig.json
|── package.json

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

### core

Core is something that ships with angcli, and for now it only contains one file boot.js, which bootstraps angular app.

### bower_components

Bower dependencies

### dist

Build folder, this folder contains final build files which are

* **vendor.js**
* **app.js**
* **app.css**

### node_modules

npm dependencies

### .jshintrc

Jshint config file to lint js code

### index.html

Your app entry point .html file.

### karma.conf.json

Config file for karma unit tests.

### ngconfig.json

Angular cli config file , let's spend some time understanding this file

```
{
  "preffered_coding_style": "Javascript",
  "css_preprocessor": "css",
  "app_name": "angularApp",
  "uglify_js": false,
  "prefix_css": true,
  "minify_css": true,
  "port": 3080,
  "host": "127.0.0.1",
  "live_reload": true,
  "run_server": true,
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
  "hooks_to_ignore": []
}
```

#### preffered_coding_style

It can be Javascript or Coffeescript

#### css_preprocessor

Which css preprocessor you want to use, possible values can be one of the following :-

* css
* stylus
* compass
* less

#### app_name

Your angular module name, by keeping app_name here it makes it easy for you to change at any point of time, without messing up number of
files.

#### uglify_js

Boolean whether to minfiy js or not.

#### minify_css

Boolean whether to minify css or not.

#### port

Server port number.

#### host

Server host

#### live_reload

Whether you want to reload server on file change.

#### run_server

Serve files using inbuilt local server

#### vendors

Vendors are list of 3rd party libraries, it is very important to define them here, so that they will be part of vendor.js not app.js.

#### hooks_to_ignore

Array of hooks you want to ignore.

# Ecosystem

So far we have spent time understanding

* what is ngcli ?
* how to run commands ?
* directory structure and important files

Now we will talk about the ecosystem, which is very important to debug your apps, and add your own quick hacks.

## CommonJs

angcli uses [browserify][db0c6c83] , [debowerify][a31895cb] and [deamdify][294cda20] enabling node js style
module require.

3rd party vendor libraries get bundled inside dist/vendor.js, whereas your local app files becomes part of dist/app.js

## ngConfig

ngConfig is the place where you app config lives in, it can be used for global settings like **app_name**, or can be used by hooks to specifiy local settings for example **auto_index** used by ng-index-entities.

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

## Ignoring Hooks

ng-hooks have no idea about you and your project, instead they have been created using industry specific conventions. At time you may start hating some hook as you are trying to achieve something else. You can easily turn off that hook inside your ngconfig.json file.

**ngconfig.json**

```
"hooks-to-ignore": ["ng-index-entities"] // example
```

You can simply pass the name of hook you want to disable permanently for this project. You may reference npm to find hook-name.

## Understanding Vendors

It is really important to understand the difference between **dist/vendor.js** and **dist/app.js**, all 3rd libraries using bower should be part of vendor.js resulting in faster incremental builds and all local source files should be part of app.js.

Deciding which files will be part of vendor file is done using ngconfig.json inside vendors key.

```
"vendors": [
  {
    "angular-deferred-bootstrap": "angular-deferred-bootstrap"
  },
  {
    "angular": "angular"
  },
  {
    "angular-route": "angular-route"
  },
  {
    "ng-table": "ng-table"
  }
],
```

Left hand side assignment is the name of the folder inside bower_components whereas right side assignment is the key you
want to use in order to require this library. Any library which is not mentioned inside this file will be bundled with app.js (which is not recommended).

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
@name: homeCtrl
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

Now it can a tedious task to register entities urself by going back and forth again. This is very **ng-index-entities** hook comes into the picture.

You can read more about ng-index-entities at <placeholder>

## Generators

Generators helps you in creating entities right from your command line and below is the list of generators.

1. controller
2. directive
3. filter
4. factory
5. services
6. initializer

## Build

Building your source files into a bundle is done using gulp and browserify.

### Browserify

Browserify converts commonjs modules to something what browsers understands, it makes use of debowerify and deamdify to
make sure all bundled modules are well transformed for browsers.

### Gulp

Gulp is responsible for running all build tasks, even browserify transformations is a part of gulp task. All tasks are part of ng-task-runner.

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

# ChangeLog

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
[294cda20]: https://github.com/jaredhanson/deamdify "deamdify"
[a31895cb]: https://github.com/eugeneware/debowerify "debowerify"
[db0c6c83]: http://browserify.org/ "browserify"
