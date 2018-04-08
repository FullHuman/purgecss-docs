# Whitelisting

You can whitelist selectors to stop purgecss from removing them from your CSS. This can be accomplished with the purgecss options `whitelist` and `whitelistPatterns`, or directly in your CSS with a special comment.

## Specific selectors

You can whitelist selectors with `whitelist`.

```javascript
const purgecss = new Purgecss({
    content: [], // content
    css: [], // css
    whitelist: ['random', 'yep', 'button']
})
```

In the example, the selectors `.random`, `#yep`, `button` will be left in the final CSS.

## Patterns

You can whitelist selectors based on a regular expression with `whitelistPatterns` and `whitelistPatternsChildren`.

```javascript
const purgecss = new Purgecss({
    content: [], // content
    css: [], // css
    whitelistPatterns: [/red$/]
})
```

In the example, selectors ending with `red` such as `.bg-red` will be left in the final CSS.

Patterns are regular expressions. You can use [regexr](https://regexr.com) to verify the regular expressions correspond to what you are looking for.

## In the CSS directly

You can whitelist directly in your CSS with a special comment.

```css
/* purgecss ignore */
h1 {
    color: blue;
}
```

