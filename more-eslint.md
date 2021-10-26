# More ESLint 

## Config for bigger projects
For more advanced projects that require more detailed rules I follow this: https://github.com/wesbos/eslint-config-wesbos.

essentially: 
```
npx install-peerdeps --dev eslint-config-wesbos
```
Then if it is **not a react project** create `.eslintrc.js` file with this inside:
```javascript=
module.exports = {
  extends: ['wesbos'],
	rules: {
	    camelcase: 0, // I like camelcased variables
	  },
};
```

If it **is a react project** then you instead add the config to the package.json:

```javascript=
"eslintConfig": {
    "extends": [
      "wesbos"
    ], 
    "rules": {
      "camelcase": 0
    }
  },
  
```

## Scripts 
If you wish to create scripts to run eslint and to run fixes of eslint you can do so like this: 
```json
"scripts": {
    "lint": "eslint ." // or the directory you want to lint,
    "lint-fix": "eslint . --fix"
  },
```

## Extends vs Plugins
Extends uses an external config file. A plugin on the other hand provides you with a set of rules that you can individually apply depending on your need. Just having a plugin does not enforce any rule. You have to choose which rules you need. 

## Disabling eslint

Disabling the next line in a file: 
```
// eslint-disable-next-line
```
Disabling a rule (or making it less strict): 

```javascript
    extends: ['wesbos'],
    rules: {
        'no-unused-vars': 0, // this is how you turn a rule off. 
        'no-debugger': 1, // this turns them into warnings
        'no-dupe-keys': 2 // this turns them into errors
      },

```
By setting a rule to 0 you disable it, 2 means error and 1 means warning.
