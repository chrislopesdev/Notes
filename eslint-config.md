# ESLINT CONFIG SETTINGS

Install Eslint Dev Dependencies
```terminal
npm i -D eslint prettier eslint-plugin-prettier eslint-config-prettier eslint-plugin-node eslint-config-node
```

<br />

Install AirBnB Style
```terminal
npx install-peerdeps --dev eslint-config-airbnb
```

<br />

Create Config Files
```
touch .prettierrc
```

```json
{
  "singleQuote": true
}
```

We can use the terminal to create our `.eslintrc` file.
```terminal
eslint --init
```
Follow the prompts to install your `eslintrc.json` file.

You can now edit your `eslintrc.json` file to your specifications. Brad Traversy Example:

```json
{
    "extends": [
        "airbnb",
        "prettier",
        "pluging:node/recommended"
    ],
    "plugins": [
        "prettier"
    ],
    "rules": {
        "prettier/prettier": "error",
        "no-unused-vars": "warn",
        "no-console": "off",
        "func-names": "off"
    }
}
```