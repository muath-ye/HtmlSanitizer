# HtmlSanitizer

Very fast client-side HTML Sanitizer (i.e. needs a browser, won't work in server-side/backend enviroments like `Node` etc.).

> Please note: to prevent XSS attacks you should always sanitize input **on the server** too. *Never trust the client!*

Usage:

```html
<script src="HtmlSanitizer.js"></script>

<script>
    var input = HtmlSanitizer.SanitizeHtml("<div> <script> Alert('xss!'); </script> </div>");
    //input == "<div> </div>";
</script>
```

The sanitizer uses [whitelisting](https://en.wikipedia.org/wiki/Whitelisting) (as opposed to "blacklisting") approach to clear out everything that's not allowed.

## Speed

It uses browser/DOM to parse the html by creating an invisible "sandboxed" iframe (hense the browser "front-end only" requirement) which makes it **much faster** than many "pure JavaScript" sanitizers.

## Tags allowed by default

`a, abbr, b, blockquote, body, br, center, code, div, em, font, h1, h2, h3, h4, h5, h6, hr, i, img, label, li, ol, p, pre, small, source, span, strong, table, tbody, tr, td, th, thead, ul, u, video`

## Attributes allowed by default

`align, color, controls, height, href, src, style, target, title, type, width`

## CSS styles allowed by default

`color, background-color, font-size, text-align, text-decoration, font-weight`

Allowed tags, styles and attributes are listed in `tagWhiteList`, `attributeWhiteList` and `cssWhiteLisst` variables which you can modify (until we add a proper API).