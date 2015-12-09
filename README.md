# CSS Documentation support for SourceJS

[![Gitter chat](https://badges.gitter.im/gitterHQ/gitter.png)](https://gitter.im/sourcejs/Source)

Appends rendered [KSS](https://github.com/kss-node/kss-node) documentation into SourceJS Spec pages.
Syntax for style documentation can be found [here](https://github.com/kss-node/kss/blob/spec/SPEC.md).

[SourceJS](http://sourcejs.com) plugin (for 0.5.0+ version).

## Install

To install middleware, run npm command in `sourcejs/user` folder:

```
npm install sourcejs-kss --save
```

After restarting your app, middleware will be loaded automatically. To disable it, remove npm module and restart the app.

## Usage

KSS works as SourceJS middleware, when Spec (documentation page) is requested, plugin is searching CSS files in Spec folder by defined mask.

All found CSS (or LESS/SASS/SCSS/Stylus) will be processed through [KSS](https://github.com/kss-node/kss-node) in runtime, during request.

Here's an example of Spec folder structure

```
specs/button
    button.css
    readme.md
    info.json
```

`button.css` contents:

```scss
// Default
//
// Your standard button suitable for clicking.
//
// Markup:
// <button class="button-pro">Click me</button>
//
// Styleguide 1
.button-pro {}

// Default Big
//
// Your enlarged button suitable for clicking.
//
// Markup:
// <button class="button-pro button-pro_big">Click me</button>
//
// Styleguide 1.1
.button-pro.button-pro_big {}

// Default Disabled
//
// Your button which is disabled
//
// Markup:
// <button class="button-pro button-pro_big">Click me</button>
//
// Styleguide 1.1
.button-pro.button-pro_disabled {}
```

Spec rendered result (http://127.0.0.1:8080/specs/button):

`readme.md` contents will be rendered at the top of Spec file. Other file types as `index.src` or `index.jade` (with [Jade plugin](https://github.com/sourcejs/sourcejs-jade)) could also be used.

**Note** that Spec file and `info.json` should be present in folder for page to load.

## Options

You can configure plugin options from `user/options.js`:

```js
{
    core: {},
    assets: {},
    plugins: {
        dss: {
           targetCssMask: '**/*.{css,less,stylus,sass,scss}',
           visibleCode: true,
           templates: {
               sections: path.join(__dirname, '../views/sections.ejs')
           }
        }
    }
}
```

### targetCssMask

Type: `String`
Default value: `**/*.{css,less,stylus,sass,scss}`

Glob mask for searching CSS files for KSS parsing, starting from requested Spec path (https://github.com/isaacs/node-glob).

### visibleCode

Type: `Boolean`
Default: `true`

Set `source_visible` to every `src-html` code containers to show code preview by default. Set to `false` if you prefer hiding code blocks by default (toggled from menu `Show source code`).

### templates

Type: `Object`

#### templates.item

Type: `String`
Default: `path.join(__dirname, '../views/sections.ejs')`

Set path to EJS template for rendering KSS JSON result. Currently this plugin uses only one template for sections.

## Other SourceJS middlewares

* https://github.com/sourcejs/sourcejs-jade
* https://github.com/sourcejs/sourcejs-smiles
