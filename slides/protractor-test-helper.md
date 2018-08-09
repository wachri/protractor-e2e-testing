# Protractor Test Helper

---

## Protractor Test Helper
> The Protractor Test Helper provides functions which help to create robust and reliable end-to-end tests with Protractor
and reduces the pain of end-to-end tests to a minimum.
All provided action helpers perform checks that the element is in the correct state before the actual task is performed.

---

## Main features

* Robust actions like `click`, `sendKeys` or `hover`, for stuff you often do, which wait for their elements before the action is performed
* Lots of `waitfor…` functions to avoid `sleep`
* Provides better error messages with more details
* Custom matchers like `.toBePresent()` or `toBeDisplayed()`; 

---

## Example
```js
const { click, waitForTextToBe, sendKeys, getText } = require('protractor-test-helper');

describe('readme example', () => {
    // Simple example - better would be a Page Object
    const firstNumber = element(by.model('first'));
    const secondNumber = element(by.model('second'));
    const goButton = element(by.id('gobutton'));
    const latestResult = element(by.binding('latest'));

    beforeEach(() => {
        browser.get('http://juliemr.github.io/protractor-demo/');
    });

    it('should add one and two', () => {
        sendKeys(firstNumber, '1');
        sendKeys(secondNumber, '2');
        click(goButton);

        waitForTextToBe(latestResult, '3');
        expect(getText(latestResult), '3');
    });
});
```

---

## Protractor Test Helper
Is available at [https://www.npmjs.com/package/@hetznercloud/protractor-test-helper](https://www.npmjs.com/package/@hetznercloud/protractor-test-helper)
