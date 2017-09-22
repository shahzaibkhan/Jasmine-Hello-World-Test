# Jasmine Hello World Test Example

Here are the steps that can help you setup a test enviornment:

## Expectation:

- You are familiar with Node.Js and How packages gets install

Tutorial:
1. Install normal node Node.js application and then browse to the folder via command prompt/shell

2. Using terminal run: "npm install jasmine-node --save-dev" for installing jasmine

3. Then install Request Node module: "npm install request --save" (The request module is by far the most popular (non-standard) Node package for making HTTP requests.) http://stackabuse.com/the-node-js-request-module/

4. Make a director "mkdir spec"

5. Add a file test_spec.js in it.

6. Open this file and do some basic test like server running.

		var request = require("request");
		var helloWorld = require("../app.js")
		var base_url = "http://localhost:3000/"

		describe("Hello World Server", function() {
		  describe("GET /", function() {
			it("returns status code 200", function(done) {
			  request.get(base_url, function(error, response, body) {
				expect(response.statusCode).toBe(200);
				done();
			  });
			});

			it("returns Hello World", function(done) {
			  request.get(base_url, function(error, response, body) {
				expect(body).toBe("Hello World");
				helloWorld.closeServer();
				done();
			  });
			});
		  });
		});

7. Integrate jasmine test file with the node.js application. Your app.js should look like this:

		var express = require('express');
		var app = express();
		var exports = module.exports = {};

		app.get('/', function(req, res){
		  res.send('Hello World');
		});

		var server = app.listen(3000, function(){
		  console.log('Magic is happening on port 3000');
		});

		exports.closeServer = function(){
		 server.close();
		};
		
8. In the package.json file mention the test:

		{
		  "name": "node-tutorial",
		  "version": "1.0.0",
		  "main": "app.js",
		  "dependencies": {
			"express": "^4.13.3",
			"request": "^2.65.0"
		  },
		  "devDependencies": {
			"jasmine-node": "^1.14.5"
		  },
		  "scripts": {
			"test": "jasmine-node spec"
		  },
		  "author": "",
		  "license": "ISC"
		}

8. Use "npm test" command to test through.