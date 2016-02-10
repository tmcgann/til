If you build a constructor the typical way using `this` it's easy to leverage the prototype.

```javascript
function TypicalConstructor(str) {
    var privateVar = 'private ' + str;

    this.publicVar = 'public ' + str;
    this.publicFunc = publicFunc;

    function privateFunc() {
        return 'private func';
    }

    function publicFunc() {
        return privateVar;
    }
}

TypicalConstructor.prototype.protoFunc = function () {
    return this.publicFunc();
}

var typicalServ = new TypicalConstructor('foo');
typicalServ.protoFunc(); // private foo
```

If you want to get rid of `this` you can simply return an object literal from the constructor. Only problem is it destroys the protoype chain, which may or may not be a problem.

```javascript
function AtypicalConstructor(str) {
    var privateVar = 'private ' + str;
    var publicVar = 'public ' + str;

    return {
        publicFunc: publicFunc,
        publicVar: publicVar
    };

    function privateFunc() {
        return 'private func';
    }

    function publicFunc() {
        return privateVar;
    }
}

AtypicalConstructor.prototype.protoFunc = function () {
    return this.publicFunc();
}

var atypicalServ = new AtypicalConstructor('bar');
atypicalServ.protoFunc(); // Uncaught TypeError: atypicalServ.protoFunc is not a function
```
