# HS Lunch Bot



Install the project

```
npm install
```

Run all test

```
npm test
```

Run single test

```
mocha test/specs/{path_to_the_file}
```

## Project structure

At the root

```
/config
  |- index.js
  |- default.js
  |- dev.js
  |- prod.js
/lib
/src/
  |- /command  
  |- /core
  |- /error
  |- /model
  |- /util
/test
  |- /resources
  |- /specs
```

- **config** - Contains different environment config

- **lib** - Contains external libraries that are not available on NPM

- **src** - Contains all the project classes
	- **command** - You new command should be store here (Don't forget to extend **BaseCommand** class)
	- **core** - Contains core classes
	- **core** - Contains custom error classes
	- **model** - Contains datasource models like: DynamoDb, MongoDb, Redis, etc...
	- **util** - Contains helper functions

- **test** 
	- **resources** - Contains test resource files
	- **specs** - Contains unit test specs. Each classes' unit test should be organise following his directory structure. For example:
	
	```
	
	# A comman class
	/src/command/Hello.js
	
	# Unit test will be localted
	/test/specs/command/Hello.js
	```

## Environement
The application environment is defined with env variable `LUNCH_BOT_ENV`. 
The config module always load the `default.js` first then the environment config.

## Command interface
All commands must extend the `src/command/Base.js` or one of his subclass. You override the `run` method with the logic needed.
```
var Hello = Base.extend({
  run: function(resolve, reject) {
    resolve("Hi everyone");
  }
})
```

####Run method
The code for your command class is implemented inside the `run` method. The method has two callbacks `resolve` and `reject`. After your code execution, you invoke one of these callbacks, resolve for success and reject for error.

Example:
```
var cmd = Base.LunchTimeCommand({
  name: 'greeting',
  description: "Always nice",
  
  run: function(resolve, reject) {
    // ... more core
    resolve('Hi, are you hungry?');
  }
})
```

####Command options
A command may accept `options` that can be use by your code.
Example:
```
# This command has the lang option
var cmd = new GreetingCommand({ lang: 'french' });

# Inside the GreetingCommand run function
run: function(resolve, reject) {

  var text = 'Hi';
  
  if (this.options.lang == 'french') {
      text = 'Bonjour';
  }
  else if (this.options.lang == 'spanish') {
      text = '¡Hola';
  }

  resolve(text);
}
```

## NLP Engine


```
WOKRING ON THIS

```
