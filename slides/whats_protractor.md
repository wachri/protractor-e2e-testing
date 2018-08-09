## Protractor

---
### What's protractor?
> Protractor is an end-to-end test framework for Angular applications. Protractor runs tests against your application running in a real browser, interacting with it as a user would.

---
> ... but works also on non angular pages!

---

### First test

```
describe('Protractor Demo App', function() {
  it('should add one and two', function() {
    browser.get('http://juliemr.github.io/protractor-demo/');
    element(by.model('first')).sendKeys(1);
    element(by.model('second')).sendKeys(2);

    element(by.id('gobutton')).click();

    expect(element(by.binding('latest')).getText()).
        toEqual('5'); // This is wrong!
  });
});
```
(quick but not recommended )
