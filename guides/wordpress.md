# Wordpress

Based on the [gist](https://gist.github.com/frnwtr/5647673bb15ca8893642469d3b400cba) made by @frnwtr, `purgecss-with-wordpress` is a set of templates for Wordpress CMS.

## Getting Started

### Installation

You need to install [purgecss](https://github.com/FullHuman/purgecss) first.

Install `purgecss-with-wordpress`:

```bash
npm i --save-dev purgecss-with-wordpress
```

## Usage

```javascript
import Purgecss from 'purgecss'
import purgecssWordpress from 'purgecss-with-wordpress'

const purgeCss = new Purgecss({
  content: ['**/*.html'],
  css: ['**/*.css'],
  whitelist: purgecssWorpress.whitelist,
  whitelistPatterns: purgecssWordpress.whitelistPatterns
})
const result = purgecss.purge()
```

