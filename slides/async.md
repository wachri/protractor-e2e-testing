# Async vs. Flow

---

## Flow (deprecated)

* The `Web Driver Control Flow` is / was used to synchronize your commands
* You write synchronous code which is executed asynchronous in the background with the flow
---

## Flow (deprecated)

```ts
describe('example', () => {
    it('click should click on the button', () => {
        console.log('test1');
        click(actionsPage.clickBtn);
        waitToBeDisplayed(actionsPage.clickResult);
        
        click(actionsPage.clickBtn);

        expect(actionsPage.clickResult.isDisplayed()).toBe(true);
        console.log('test2');
    });
 });

``` 
The console logs are directly logged, but the second click is executed in the browser only after the 
`waitToBeDisplayed` is ready.
---

## Async
```ts
describe('async actions', () => {
    const actionsPage: ActionsPage = new ActionsPage();

    beforeEach(async () => {
        await actionsPage.navigateTo();
    });

    it('click should click on the button', async () => {
        await click(actionsPage.clickBtn);
        await waitToBeDisplayed(actionsPage.clickResult);

        await expect(actionsPage.clickResult.isDisplayed())
            .toBe(true);
    });

    it('hover should hover on the button', async () => {
        await hover(actionsPage.hoverBtn);
        await waitToBeDisplayed(actionsPage.hoverResult);

        await expect(actionsPage.hoverResult.isDisplayed())
            .toBe(true);
    });
});
```
---
## Protractor config
```js
exports.config = {
  // ...
  
  SELENIUM_PROMISE_MANAGER: false,

  // ...
};
```

To disable the control flow
