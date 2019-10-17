# npm-run-all-npm-run-bug

Repository to exploit a bug (?) between `npm.run()` and `npm-run-all`.

The [index.js](index.js) file is the following:
```js
const npm = require("npm");
npm.load(() => npm.run("run:examples:s"));
```

The result is (in the end you can find the bug itself):

- ✅ running `$ npm run run:examples:s`
```
> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**


> npm-run-all-npm-run-bug@1.0.0 example:1 /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> echo "example:1"

example:1

> npm-run-all-npm-run-bug@1.0.0 example:2 /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> echo "example:2"

example:2
```

- ✅ running `$ npm run run:examples:p`
```
> npm-run-all-npm-run-bug@1.0.0 run:examples:p /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -p example:**


> npm-run-all-npm-run-bug@1.0.0 example:2 /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> echo "example:2"


> npm-run-all-npm-run-bug@1.0.0 example:1 /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> echo "example:1"

example:2
example:1
```

- ❌ running `$ npm run bug`
```
> npm-run-all-npm-run-bug@1.0.0 bug /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> node index.js


> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**


> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**


> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**

# infinite loop
```

- ❌ running `node index.js`
```
> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**


> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**


> npm-run-all-npm-run-bug@1.0.0 run:examples:s /Users/noriste/Sites/test/npm-run-all-npm-run-bug
> npm-run-all -s example:**

# infinite loop
```

- it's the same (if not worse because the log pace is higher) if the [index.js](index.js) file runs `run:examples:p` instead of `run:examples:s`

I've created this repository after have written the [Launching “$ npm run” programmatically with npm.run()](https://dev.to/noriste/launching-npm-run-programmatically-with-npm-run-3mmc) post and have created the [nprr](https://github.com/NoriSte/nprr) utility.
