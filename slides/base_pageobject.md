# "Base" Page Object Architecture

---
> is build on the Page Object architecture

---
## The BasePageObject class
* Is the base class of all PageObjects
* It helps you to be DRY
* Contains helper to prevent `browser.sleep()` hacks
* Provides functionality like
    * click / hover helper
    * fill forms
    * upload files
    * switch tabs
    * ...

---
## Example
```
class BasePageObject {
    constructor(options) {
        // ...
        // Baseurl is set by parameter from outside
        this.url = baseurl + options.url;

        // ...
    }

    goTo() {
        // e.g.:
        // add check if we need to login
        // add check if we are on a angular page with set location
        // or if we need to navigation to a page

        browser.setLocation(self.url);
    }

    waitFor() {
        // Wait for the page to be displayed
        // e.g. wait for a specific class selector
    }

    waitForCssPresentAndDisplay() {}

    clickElement(cssSelector) {
        this.waitForCssPresentAndDisplay();
        el = element(by.css(cssSelector));
        browser.wait(protractor.ExpectedConditions.elementToBeClickable(el), 10000, 'Element ' + cssSelector + ' not clickable');
        el.click();
    }

    hover(cssSelector) {
        var el;
        this.waitForCssPresentAndDisplay(cssSelector);
        el = dv.findElement(By.css(cssSelector));
        dv.actions().mouseMove(el).perform();
    }

    hoverAndClick(cssSelector) {
        this.hover(cssSelector);
        this.clickElement(cssSelector);
    }

    // ...
}
```