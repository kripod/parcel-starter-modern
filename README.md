# 📦 parcel-starter-modern

A modern Parcel starter aiming for high productivity with _mostly_ vanilla techniques.

## 🚀 Getting started

* Clone this project _(e.g. with `git clone`)_
* Run `yarn` or `npm install` inside the root directory of the cloned project to install all the required dependencies
* Start a development server by `yarn start` or `npm run start`
  * _Other scripts like [`build`][script-build], [`lint`][script-lint] and [`format`][script-format] are also available_

[script-build]: https://parceljs.org/production.html
[script-lint]: #linting
[script-format]: #automatic-code-formatting

## 🐠 Modern ECMAScript transforms

Use next generation JavaScript today with the help of [Babel][] and its [env preset][babel-preset-env], configurable to [support the browsers of your choice][].

> 💡 Stay up to date with the [latest ECMAScript proposals][] and utilize them without fear from lack of browser support.

[babel]: https://babeljs.io/
[babel-preset-env]: https://babeljs.io/docs/plugins/preset-env
[support the browsers of your choice]: #override-the-list-of-targeted-browsers
[latest ecmascript proposals]: https://github.com/tc39/proposals

## 💅 Enhanced style management

[SCSS][sass], a superset of CSS can be used for styling pages. The usage of Sass-specific extensions is optional, as every valid CSS stylesheet is a valid SCSS file with the same meaning.

The default style of browsers is normalized by [modern-normalize][].

Stylesheets are processed by [PostCSS][], providing proper browser support for modern CSS syntax through its [env preset][postcss-preset-env] and [Autoprefixer][].

[sass]: https://sass-lang.com/
[postcss]: http://postcss.org/
[postcss-preset-env]: https://github.com/jonathantneal/postcss-preset-env
[autoprefixer]: https://github.com/postcss/autoprefixer
[modern-normalize]: https://github.com/sindresorhus/modern-normalize

## ✨ Superior developer experience

### Automatic code formatting

[Prettier][] is an opinionated code formatter aiming to provide codebase consistency when multiple developers work on the same project. The main reason behind adopting Prettier is to [stop all the on-going debates over coding styles][].

[prettier]: https://prettier.io/
[stop all the on-going debates over coding styles]: https://prettier.io/docs/en/why-prettier.html

### Linting

[Linters][lint] are tools that analyze source code to flag programming errors, bugs, stylistic errors, and suspicious constructs.

* JavaScript files are linted by [ESLint][], enforcing the [Airbnb JavaScript Style Guide][] through an overridable set of rules provided by [eslint-config-airbnb-base][].
* SCSS files are linted by [stylelint][], adhering to the rules specified in [stylelint-config-recommended-scss][] and the [declaration order conventions of idiomatic-css][] _(enforced by [stylelint-config-idiomatic-order][])_.

[lint]: https://en.wikipedia.org/wiki/Lint_(software)
[eslint]: https://eslint.org/
[airbnb javascript style guide]: https://github.com/airbnb/javascript
[eslint-config-airbnb-base]: https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb-base
[stylelint]: https://stylelint.io/
[stylelint-config-recommended-scss]: https://github.com/kristerkari/stylelint-config-recommended-scss
[declaration order conventions of idiomatic-css]: https://github.com/necolas/idiomatic-css#declaration-order
[stylelint-config-idiomatic-order]: https://github.com/ream88/stylelint-config-idiomatic-order

### Construct flexible layouts with ease

[Bulma][] is a modular, mobile-first CSS framework. It can be used along with the [HTML viewport meta tag][] to build responsive websites with ease.

[bulma]: https://bulma.io/
[html viewport meta tag]: https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag

## 🛠️ Configurable with reasonable defaults

### Override the list of targeted browsers

By default, [Parcel targets modern browsers][]. This behavior [can be overrided in numerous ways][browserslist], e.g. by a `.browserslistrc` config file:

```
> 1%
last 2 versions
```

[parcel targets modern browsers]: https://github.com/parcel-bundler/parcel/blob/master/src/utils/getTargetEngines.js
[browserslist]: https://github.com/browserslist/browserslist

### Opt-in templating support

Building a multi-page website may introduce unwanted redundancy to your project. In this case, consider using an HTML templating solution.

> 💡 Pages with similar layout should rely on a single template instead of duplicated code.

#### Example

_To demonstrate the concept of templating, a "vanilla-like" solution will be used._

Firstly, install [posthtml-extend][] _(or the templating library of your choice)_:

```bash
yarn add posthtml-extend
```

After that, add a `.posthtmlrc` file to the root of your project, [as instructed by the official Parcel docs][parcel-transforms-posthtml]:

```json
{
  "plugins": {
    "posthtml-extend": {
      "root": "./src/layouts"
    }
  }
}
```

Finally, create a new layout and a page based on it.

`src/layouts/index.html`:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8" />

  <title>
    <block name="title"> | Website title</block>
  </title>
</head>

<body>
  <main>
    <block name="main" />
  </main>

  <footer>
    <block name="footer">Footer content</block>
  </footer>
</body>

</html>
```

`src/pages/index.html`:

```html
<!-- The line below refers to "src/layouts/index.html", as specified in ".posthtmlrc" -->
<extends src="index.html">
  <block name="title" type="prepend">Page title</block>

  <block name="main">
    <h1>Hello, templating!</h1>
    <p>Goodbye, code duplication!</p>
  </block>

  <block name="footer" type="append"> – Author name</block>
</extends>
```

The result should look as follows:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8" />

  <title>
    Page title | Website title
  </title>
</head>

<body>
  <main>
    <h1>Hello, templating!</h1>
    <p>Goodbye, code duplication!</p>
  </main>

  <footer>
    <block name="footer">Footer content – Author name</block>
  </footer>
</body>

</html>
```

[posthtml-extend]: https://github.com/posthtml/posthtml-extend
[parcel-transforms-posthtml]: https://parceljs.org/transforms.html#posthtml
