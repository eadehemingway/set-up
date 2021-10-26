# More ESLint 

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
