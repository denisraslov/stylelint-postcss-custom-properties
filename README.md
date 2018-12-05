# Value No Exposed Custom Properties <img src="https://jonathantneal.github.io/stylelint-logo.svg" alt="stylelint" width="90" height="90" align="right">

A [stylelint](https://github.com/stylelint/stylelint) rule to disallow usage of exposed custom properties.

A error from the plugin looks like this:
```
1:1  ✖  The value (or a part of it) should be presented as a custom property: "#FFF" is "--white"
```

## Installation

```
npm install stylelint-value-no-exposed-custom-properties
```

## Usage

Add [Value No Exposed Custom Properties] to your [stylelint configuration].

```js
{
  "plugins": [
    "stylelint-value-no-exposed-custom-properties"
  ],
  "rules": {
    "stylelint/value-no-exposed-custom-properties": true || false || null
  }
}
```

## Options

### true

If the first option is `true`, then [Value No Exposed Custom Properties] 
requires defined custom properties to be used instead of exposed values, and the following pattern are
_not_ considered violation:

```css
:root {
  --white: #FFF;
}

.example {
  color: var(--white);
}
```

While the following pattern are considered violation:

```css
:root {
  --white: #FFF;
}

.example {
  color: #FFF;
}
```

Custom Properties can be imported using the second option.

### false

If the first option is `false` or `null`, then
[Value No Unknown Exposed Properties] does nothing.

---

### importFrom

When the first option is `true`, then the second option can specify sources
where Custom Properties should be imported from by using an `importFrom` key.
These imports might be CSS, JS, and JSON files, functions, and directly passed
objects.

```js
// .stylelintrc
{
  "plugins": [
    "stylelint-value-no-exposed-custom-properties"
  ],
  "rules": {
    "stylelint/value-no-exposed-custom-properties": [true, {
      "importFrom": [
        "path/to/file.css", // => :root { --white: #FFF; }
        "path/to/file.json" // => { "custom-properties": { "--white": "#FFF" } },
        "path/to/file.js" // => { module.exports = { customProperties: { "--white": "#FFF" } } }
      ]
    }
  }
}
```
