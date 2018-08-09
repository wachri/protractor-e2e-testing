## Setup

---
### Locally

You can run protractor test after installing it via `npm`
```bash
npm install -g protractor
webdriver-manager update
webdriver-manager start
```

```bash
protractor
```

```
// protractor.config.js
exports.config = {
  framework: 'jasmine',
  seleniumAddress: 'http://localhost:4444/wd/hub',
  specs: ['spec.js'],
  capabilities: {
    browserName: 'chrome'
  }
}
```

https://www.protractortest.org/#/tutorial

---
### Example scripts

```json
{
  "scripts": {
    "webdriver-manager": "webdriver-manager",
    "webdriver:update": "yarn run webdriver-manager update",
    "webdriver:start": "yarn run webdriver-manager start",
    "protractor": "protractor",
    "pree2e:only": "yarn run webdriver:update -- --standalone",
    "e2e": "npm-run-all -p -r e2e:server e2e:only",
    "e2e:only": "yarn run protractor"
  }
}
```
---
### Testing in the CI
![e2e-setup](./slides/img/e2e-setup.jpg)

---
### Example Pipeline
![pipline](./slides/img/test-pipline.png)

---
### Gitlab config
```yml
.e2e-chrome-fake: &e2e-chrome-fake
  <<: *hc-runner
  <<: *before_test
  stage: test
  image: docker.image
  services:
  - $IMAGE:$CI_COMMIT_SHA
  variables: &e2e-chrome-fake-variables
    BROWSER: "chrome"
    WEBDRIVER_HOST: "zalenium.zalenium.svc.cluster.local"
    DBUS_SESSION_BUS_ADDRESS: "/dev/null"  

e2e-chrome-owner-fake:
  <<: *e2e-chrome-fake
  variables:
    FE_TEST_NAME: owner
    <<: *e2e-chrome-fake-variables
  script:
  - yarn run e2e:owner
```
