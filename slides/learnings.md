# Learnings

---

> You need experience to make your tests stable, but there are libraries out there which can help

---

> It reduces the time of manual testing a lot, especially when the projects get bigger and bigger

---

> If possible split up your test suit into pieces, so you can run them parallelized

---

> There will be always discussions if this is needed, but so far at the end everyone was lucky to have such a huge test suite

---

> It takes time to maintain the tests, but at the end you have no fear to deploy stuff on friday

---

> Fix your window size

e.g. in the `protractor.config.js` with

```js
onPrepare: () => {
    browser.ignoreSynchronization = true;

    browser.driver
        .manage()
        .window()
        .setSize(1440, 810);
}
```

---

> Run your tests in different user / access roles (if applicable) and also test what the user should not be able to do

(If you are honest, you normally test only as admin but there might be a bug as a normal user)

---

> Fix flaky tests as soon as possible

(else everybody in the team is wasting time to retry the test)


---

> Create helper functions for actions you are using frequently, like login, logout, ...

```ts
export function logOut(): void {
    flowLog('Logout');
    const topBarPage: TopBarPage = new TopBarPage();
    const loginPage: LoginPage = new LoginPage();
    browser.executeScript('window.scrollTo(0,0);');
    topBarPage.clickLogout();
    waitToBeDisplayed(loginPage.usernameInput);
    flowLog('Logged out');
    expect(loginPage.usernameInput.isPresent()).toBeTruthy();
}
```