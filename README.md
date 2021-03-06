# css-chunks-html-webpack-plugin

Plugin for injecting css chunks, extracted using extract-css-chunks-webpack-plugin, to HTML for html-webpack-plugin

Use in conjunction with
[extract-css-chunks-webpack-plugin](https://github.com/faceyspacey/extract-css-chunks-webpack-plugin) and
[babel-plugin-dual-import](https://github.com/faceyspacey/babel-plugin-dual-import)
to inject CSS chunks paths into your HTML file with
[html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin).

## Version

The current version is incompatible with Webpack 3 or older. In order to use this plugin with Webpack 3, use
`css-chunks-html-webpack-plugin@0.1.0`

```bash
npm install --save-dev css-chunks-html-webpack-plugin@0.1.0
```

## Recommended Installation

```bash
npm install --save-dev css-chunks-html-webpack-plugin \
 mini-css-extract-plugin babel-plugin-dual-import \
 html-webpack-plugin
```

_webpack.config.js_

```js
const ExtractCssPlugin = require('mini-css-extract-plugin');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const CssChunksHtmlPlugin = require('css-chunks-html-webpack-plugin');

module.exports = {
  // your other options
  plugins: [new ExtractCssPlugin(), new CssChunksHtmlPlugin({ inject: 'head' }), new HtmlWebpackPlugin()],
};
```

## Configuration

You can pass an object of configuration options to CssChunkHashPlugin. Allowed values are as follows:

* `inject`: `'head'` | `'body'` | `false` whether to inject chunks paths script into HTML, used for manually adding
  chunks paths using custom template for HtmlWebpackPlugin (default `true`)

The CSS chunks paths map is saved in `htmlWebpackPlugin.files.cssHash` in your template. So if you want to manually add
CSS chunks map you can do (if you are using EJS):

```ejs
<script type="text/javascript">
    window.__CSS_CHUNKS__ = JSON.parse('<%= JSON.stringify(htmlWebpackPlugin.files.cssHash) %>')
</script>
```

By default, it will inject script tag into `<head>`. If you want to inject the script tag with `window.__CSS_CHUNKS__`
into `<body>` set `inject: 'body'`,

## Example

There is a basic example of usage in [examples](examples)

# Contribution

You're free to contribute to this project by submitting [issues](https://github.com/mike1808/css-chunks-html-webpack-plugin/issues) and/or [pull requests](https://github.com/mike1808/css-chunks-html-webpack-plugin/pulls).

# License

This project is licensed under [MIT](LICENSE).
