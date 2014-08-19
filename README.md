grunt-spec / collaborator
=========================

grunt-spec
----------

Generate spec files in the relevant folder using grunt spec plugin
```
grunt spec:namepspace/calculator
```
This will create a new AMD spec file in spec/namespace/calculator.js


To run "grunt", either install globally with "npm install -g grunt-cli" or run locally with:
```
node_modules/.bin/grunt
```

In the spec itself, use the spec! requirejs plugin to force creating of module that doesn't exist yet. The following spec will be created by grunt spec:
```javascript
define(['spec!namespace/calculator'], function(calculator) {
    describe('Namespace Calculator', function() {
        it('is an instance of Calculator', function() {
            expect(calculator.constructor.name).toBe('Calculator');
        });
    });
});
```

On running "grunt jasmine", the spec! requirejs plugin will cause a calculator module to be created in src/namespace/caculator.js if none exists yet. The default pattern is an object factory which will look like this:
```javascript
define(function() {
    function Calculator() {
        //@todo: create methods here
    }

    return new Calculator();
});
```

collaborator
------------

Use require-js as  DIC to provide collaborators for jasmine specs.

Edit the file collaborators.js to provide a definition of your tests collaborators.
Specify the names of the collaborators methods explicitly, and a jasmine spy will be created for them.
If you use 'null' for the method names, an existing module will be expected to be found in the src/ directory.

```javascript
define(['collaborator!parser', 'spec!calculator'], function(calculator) {
    describe('Calculator', function() {
        it('is a Calculator', function() {
            expect(something).toBe(whatever);
        });
    });
});
```

Specifiy all expected collaborators and their methods in the file collaborators.js:
```javascript
define(function() {
    return {
        '*': {
            parser: ['parse']
        }
    };
});
```

To install the required modules run:
```
npm install
```


