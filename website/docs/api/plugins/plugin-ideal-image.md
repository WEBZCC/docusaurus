---
sidebar_position: 8
slug: /api/plugins/@docusaurus/plugin-ideal-image
---

# 📦 plugin-ideal-image

import APITable from '@site/src/components/APITable';

Docusaurus Plugin to generate an almost ideal image (responsive, lazy-loading, and low quality placeholder).

:::info

By default, the plugin is **inactive in development** so you could always view full-scale images. If you want to debug the ideal image behavior, you could set the [`disableInDev`](#disableInDev) option to `false`.

:::

## Installation {#installation}

```bash npm2yarn
npm install --save @docusaurus/plugin-ideal-image
```

## Usage {#usage}

This plugin supports the PNG and JPG formats only.

```jsx
import Image from '@theme/IdealImage';
import thumbnail from './path/to/img.png';

// your React code
<Image img={thumbnail} />

// or
<Image img={require('./path/to/img.png')} />
```

## Configuration {#configuration}

Accepted fields:

<APITable>

| Option | Type | Default | Description |
| --- | --- | --- | --- |
| `name` | `string` | `ideal-img/[name].[hash:hex:7].[width].[ext]` | Filename template for output files. |
| `sizes` | `number[]` | _original size_ | Specify all widths you want to use. If a specified size exceeds the original image's width, the latter will be used (i.e. images won't be scaled up). |
| `size` | `number` | _original size_ | Specify one width you want to use; if the specified size exceeds the original image's width, the latter will be used (i.e. images won't be scaled up) |
| `min` | `number` |  | As an alternative to manually specifying `sizes`, you can specify `min`, `max` and `steps`, and the sizes will be generated for you. |
| `max` | `number` |  | See `min` above |
| `steps` | `number` | `4` | Configure the number of images generated between `min` and `max` (inclusive) |
| `quality` | `number` | `85` | JPEG compression quality |
| `disableInDev` | `boolean` | `true` | You can test ideal image behavior in dev mode by setting this to `false`. **Tip**: use [network throttling](https://www.browserstack.com/guide/how-to-perform-network-throttling-in-chrome) in your browser to simulate slow networks. |

</APITable>

### Example configuration {#ex-config}

Here's an example configuration:

```js title="docusaurus.config.js"
module.exports = {
  plugins: [
    [
      '@docusaurus/plugin-ideal-image',
      // highlight-start
      {
        quality: 70,
        max: 1030, // max resized image's size.
        min: 640, // min resized image's size. if original is lower, use that size.
        steps: 2, // the max number of images generated between min and max (inclusive)
        disableInDev: false,
      },
      // highlight-end
    ],
  ],
};
```
