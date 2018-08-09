# Page Object

---
## What is a Page Object?

* The page object stores all information about a "page"
* All necessary selectors are stored here
* If possible we can cache elements here
* It contains all actions like "fill form" or "click on contact button"


---
## What it looks like
```
export class ActionsPage {
    readonly url: string = '/actions';
    readonly urlRegex: RegExp = /actions/;
    readonly selectSelector: string = '[data-test=select]';
    readonly optionSelector: string = 'option';

    navigateTo(): webdriver.promise.Promise<void> {
        return browser.get(this.url);
    }

    get clickBtn(): ElementFinder {
        return element(by.css('[data-test=click-btn]'));
    }

    get clickResult(): ElementFinder {
        return element(by.css('[data-test=click-result]'));
    }

    get hoverBtn(): ElementFinder {
        return element(by.css('[data-test=hover-btn]'));
    }

    get hoverResult(): ElementFinder {
        return element(by.css('[data-test=hover-result]'));
    }

    get sendKeysInput(): ElementFinder {
        return element(by.css('[data-test=send-keys-input]'));
    }

    get inputResult(): ElementFinder {
        return element(by.css('[data-test=input-result]'));
    }

    get select(): ElementFinder {
        return element(by.css(this.selectSelector));
    }

    get selectResult(): ElementFinder {
        return element(by.css('[data-test=select-result]'));
    }
}
```

---
## And the test?
```
describe('flow actions', () => {
    const actionsPage: ActionsPage = new ActionsPage();

    beforeEach(() => {
        actionsPage.navigateTo();
    });

    it('click should click on the button', () => {
        click(actionsPage.clickBtn);
        waitToBeDisplayed(actionsPage.clickResult);

        expect(actionsPage.clickResult.isDisplayed()).toBe(true);
    });

    it('hover should hover on the button', () => {
        hover(actionsPage.hoverBtn);
        waitToBeDisplayed(actionsPage.hoverResult);

        expect(actionsPage.hoverResult.isDisplayed()).toBe(true);
    });

    it('sendKeys should send keys to input the button', () => {
        const text = 'keys to send';
        sendKeys(actionsPage.sendKeysInput, text);
        waitForTextToBe(actionsPage.inputResult, text);

        expect(getText(actionsPage.inputResult)).toBe(text);
    });

    it('selectOption should select an option', () => {
        const option = 'option2';
        selectOption(
            actionsPage.select.element(by.cssContainingText(
                actionsPage.optionSelector,
                option
            ))
        );
        waitForTextToBe(actionsPage.selectResult, option);
        expect(getText(actionsPage.selectResult)).toBe(option);
    });

    it('selectOptionByIndex should select an option', () => {
        const option = 'option2';
        selectOptionByIndex(actionsPage.select, 1);
        waitForTextToBe(actionsPage.selectResult, option);
        expect(getText(actionsPage.selectResult)).toBe(option);
    });

    it('selectOptionByText should select an option', () => {
        const option = 'option2';
        selectOptionByText(actionsPage.select, option);
        waitForTextToBe(actionsPage.selectResult, option);
        expect(getText(actionsPage.selectResult)).toBe(option);
    });
});
```
(Test written with `protractor-test-helper`)

---
## Advantages
* You store the information about a component / page in a single file
* Makes refactoring easier because you have a interface to your actions which hides the implementation