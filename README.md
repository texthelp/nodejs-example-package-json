# Example package.json

The `package.json` in this project contains the minimum amount of information you should include when creating a library for publishing to the internal NPM repository. You'll find explanations of each line below (because JSON files can't have comments 😔)

## Explanations

```json
"name": "package-json-example"
```

This is the name of your library. It's what users of your library are going to pass to `npm install` and `require`, for example:

```cmd
npm install package-json-example --save
```

and:

```js
// CommonJS
const library = require("package-json-example");
// ES6
import library from "package-json-example";
```

---
```json
  "version": "1.3.1"
```

The current semantic version number of your library. You should update this before each `npm publish`.

NPM provides a [handy command](https://docs.npmjs.com/cli/version) to do this:

```cmd
npm version 1.3.2
# OR
npm version patch
```

Which will not only update your `version` field, but also create a Git commit and tag if run within a Git repository.

---
```json
"description": "A description of what the library does"
```

A short description of the library. This is what will show up underneath your project on npm.texthelp.com.

---
```json
  "main": "node.js"
```

This is the main entrypoint to your library. If you are only supporting browsers (and not server-side NodeJS for whatever reason), you *only* need this field.

If your library is written that it doesn't rely on `window`, `document` or any other browser-specific Javascript, then you also *only* need this field. This is the way we should be trying to write our libraries to be as flexible as possible.

**Hint:** If you need DOM on the server, use [JSDOM](https://github.com/jsdom/jsdom).  
**Hint 2:** If you need `fetch` on the server, use [node-fetch](https://github.com/bitinn/node-fetch).  

If you're creating a library which needs two different versions: one for server-side NodeJS, then `main` will be your NodeJS entrypoint and you'll need an additional entrypoint:

---
```json
"browser": "browser.js"
```

From above. If you need two different bundles: one for server-side NodeJS and one for browser JS, then you need to point this at your browser bundle.

---
```json
"scripts": {
    "build": "gulp",
    "test": "jest"
}
```

This is a collection of scripts that can be run from `npm run`. This can be useful for build scripts and in most cases can be a replacement for things like Gulp.

You can run any shell command in here, for example:

```json
"scripts": {
    "build": "mkdir dist/ && cp -R file.js dist/ && webpack"
}
```

**Hint:** If things start to get complicated with NPM scripts, check out [NPS](https://github.com/kentcdodds/nps).

---
```json
"author": "Texthelp, Ltd."
```

The author of the library

---
```json
"license": "ISC"
```

The license assigned to the library, `ISC` by default