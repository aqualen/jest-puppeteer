# jest-environment-puppeteer

[![Build Status][build-badge]][build]
[![version][version-badge]][package]
[![MIT License][license-badge]][license]

Run your tests using Jest & Puppeteer 🎪✨

```
npm install jest-environment-puppeteer
```

## Usage

Update your Jest configuration:

```json
{
  "globalSetup": "jest-environment-puppeteer/globalSetup",
  "globalTeardown": "jest-environment-puppeteer/globalTeardown",
  "testEnvironment": "jest-environment-puppeteer/testEnvironment"
}
```

Use Puppeteer in your tests:

```js
describe('Google', () => {
  beforeAll(async () => {
    await mainPage.goto('https://google.com')
  })

  it('should display "google" text on page', async () => {
    const text = await mainPage.evaluate(() => document.body.textContent)
    expect(text).toContain('google')
  })
})
```

## Recipes

### Writing test using Puppeteer

Writing test using Puppeteer is simple, you can find all available methods in [Puppeteer documentation](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md).

### Extend PuppeteerEnvironment

Sometimes you want to use your own environment, to do that you can extend `PuppeteerEnvironment`.

```js
const PuppeteerEnvironment = require('jest-environment-puppeteer')

class CustomEnvironment extends PuppeteerEnvironment {
  async setup() {
    await super.setup()
    // Your setup
  }

  async teardown() {
    // Your teardown
    await super.teardown()
  }
}

module.exports = CustomEnvironment
```

### Access `globalSetup` or `globalTeardown`

It is possible to access `globalSetup` or `globalTeardown` in your scripts.

```js
import { globalSetup, globalTeardown } from 'jest-environment-puppeteer'

async function setup() {
  await globalSetup()
  // ...
}

async function teardown() {
  // ...
  await globalTeardown()
}
```

## API

### `global.browser`

Give access to the [Puppeteer Browser](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#class-browser).

```js
it('should open a new page', async () => {
  const page = await browser.newPage()
  await page.goto('https://google.com')
})
```

### `global.mainPage`

Give access to a [Puppeteer Page](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#class-page) opened at start (you will use it most of time).

```js
it('should fill an input', async () => {
  await page.type('#myinput', 'Hello')
})
```

## Inspiration

Thanks to Fumihiro Xue for his great [Jest example](https://github.com/xfumihiro/jest-puppeteer-example).

## License

MIT

[build-badge]: https://img.shields.io/travis/smooth-code/jest-environment-puppeteer.svg?style=flat-square
[build]: https://travis-ci.org/smooth-code/jest-environment-puppeteer
[version-badge]: https://img.shields.io/npm/v/jest-environment-puppeteer.svg?style=flat-square
[package]: https://www.npmjs.com/package/jest-environment-puppeteer
[license-badge]: https://img.shields.io/npm/l/jest-environment-puppeteer.svg?style=flat-square
[license]: https://github.com/smooth-code/jest-environment-puppeteer/blob/master/LICENSE