# Page Object Test Architecture

---
## What is a Page Object?

* The page object store all information about a "page"
* All necessary selectors are stored here
* If possible we can cache here elements
* It contains all action like "fill form" or "click on contact button"


---
## How it look like
```
var AngularHomepage = function() {
  var nameInput = element(by.model('yourName'));
  var greeting = element(by.binding('yourName'));

  this.get = function() {
    browser.get('http://www.angularjs.org');
  };

  this.setName = function(name) {
    nameInput.sendKeys(name);
  };

  this.getGreeting = function() {
    return greeting.getText();
  };
};
```

---
## And the test?
```
describe('angularjs homepage', function() {
  it('should greet the named user', function() {
    var angularHomepage = new AngularHomepage();
    angularHomepage.get();

    angularHomepage.setName('Julie');

    expect(angularHomepage.getGreeting()).toEqual('Hello Julie!');
  });
});
```

---
### Advantages
* You store the information about an component / page in a single file
* Makes refactoring easier because you have a interface to your actions which hides the implementation