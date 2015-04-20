# jsAutomapper
Javascript implementation of AutoMapper by John Kalberer http://johnkalberer.com/2011/08/24/automapper-in-javascript/

Usage:

```JS
var atest = {
    same : 10,
    bleh : 4
};
var btest = {
    dumb: null,
    func: null,
    foo : null,
    bar : null,
    same : null
};
/* 
*  call 'createMap' where "a" and "b" are the name of your
*  models.  These values can be whatever you want but you 
*  must match the values when you call 'map'.
*/
automapper.createMap("a","b")
       // forAllMembers isn't necessary here but it allows you to
       // customize how you apply values to the destination model
      .forAllMembers(function(model, prop, value) { 
        model[prop] = value; 
      })
      .forMember("dumb", 12)
      .forMember("func", function() { return 8 })
      .forMember("foo", function() { this.ignore(); })
      .forMember("bar", function() { this.mapFrom("bleh"); });
     
automapper.map("a", "b", atest, btest);
```
Results:
```JS
atest
// Object {same: 10, bleh: 4}
btest
// Object {dumb: 12, func: 8, foo: null, bar: 4, same: 10}
```
