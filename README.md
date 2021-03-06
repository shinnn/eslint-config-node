# load-gh-token

[![npm version](https://img.shields.io/npm/v/load-gh-token.svg)](https://www.npmjs.com/package/load-gh-token)
[![Build Status](https://travis-ci.com/shinnn/load-gh-token.svg?branch=master)](https://travis-ci.com/shinnn/load-gh-token)
[![codecov](https://codecov.io/gh/shinnn/load-gh-token/branch/master/graph/badge.svg)](https://codecov.io/gh/shinnn/load-gh-token)

Get a [GitHub access token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line) from either an environment variable or a file

```javascript
const loadGhToken = require('load-gh-token');

// When `process.env.GITHUB_TOKEN === '36fae5325faa9b32edfd776f6b85bf71ac0a49bf'`

(async () => {
  const token = await loadGhToken(); //=> '36fae5325faa9b32edfd776f6b85bf71ac0a49bf'
})();
```

## Installation

[Use](https://docs.npmjs.com/cli/install) [npm](https://docs.npmjs.com/about-npm/).

```
npm install load-gh-token
```

## API

```javascript
const loadGhToken = require('load-gh-token');
```

### loadGhToken([*options*])

*options*: `Object`  
Return: `Promise<string>`

If there is an environment variable `GITHUB_TOKEN`, it reads its value.

If the variable `GITHUB_TOKEN` is not defined, then it reads a file `github-token.txt` at the current working directory.

```javascript
// When `process.env.GITHUB_TOKEN` is undefined but a file ./github-token.txt exists

(async () => {
  const token = await loadGhToken();
  // '... contents of github-token.txt without whitespaces ...'
})();
```

If both the `GITHUB_TOKEN` environment variable and the file `./github-token.txt` don't exist, the `Promise` will be rejected.

```javascript
(async () => {
  try {
    await loadGhToken();
  } catch (err) {
    err.message;
    // Tried to get a personal access token for GitHub API from the `GITHUB_TOKEN` environment variable or a file at '/Users/example/github-token.txt', but neither exists.

    err.code;
    //=> 'ERR_NO_GITHUB_TOKEN'
  }
})();
```

## License

[ISC License](./LICENSE) © 2018 - 2019 Watanabe Shinnosuke
