# JS Html Sanitizer

Very fast client-side HTML Sanitizer (front-end only, i.e. "needs a browser", won't work in `Node`) to prevent XSS and unwanted tags in UGC.

> Please note: to prevent XSS attacks you should always sanitize input **on the server too**. *Never trust the client!*

Usage:

```html
<script src="https://cdn.jsdelivr.net/gh/jitbit/HtmlSanitizer@master/HtmlSanitizer.js"></script>
<!-- or simply install locally: <script src="HtmlSanitizer.js"></script> -->

<script>
    var html = HtmlSanitizer.SanitizeHtml("<div> <script> Alert('xss!'); </sc" + "ript> </div>");
    //html == "<div>  </div>";
</script>
```

The sanitizer uses [whitelisting](https://en.wikipedia.org/wiki/Whitelisting) approach (as opposed to "blacklisting") to clean out everything that's not allowed.

## Speed

It uses browser/DOM to parse the html by creating an invisible "sandboxed" iframe (hence the browser "front-end only" requirement) which makes it **much faster** than "pure JavaScript" sanitizers.

Tested on `https://www.bbc.co.uk` homepage - the page is sanitized **~370 times per second** on an i5 core CPU in Firefox Quantum (tested via `benchmark.js`)

## Tags allowed by default

`a, abbr, b, blockquote, body, br, center, code, div, em, font, h1, h2, h3, h4, h5, h6, hr, i, img, label, li, ol, p, pre, small, source, span, strong, table, tbody, tr, td, th, thead, ul, u, video`

## Attributes allowed by default

`align, color, controls, height, href, src, style, target, title, type, width`

## CSS styles allowed by default

`color, background-color, font-size, text-align, text-decoration, font-weight`

## Schemas allowed by default

`http:, https:, data:`

(allowed in 'src', 'href' and similar "uri-attributes". To clean up stuff like `<a href='javascript:alert()'></a>`)

## Configuring

Allowed tags, attributes and styles are listed in `AllowedTags`, `AllowedAttributes` and `AllowedCssStyles` public properties. To disallow a tag remove it from the dictionary like this:

```javascript
delete HtmlSanitizer.AllowedTags['table']
```

To add an allowed tag:

```javascript
HtmlSanitizer.AllowedTags['script'] = true;
```

## Browser support

Supported by all major browsers, IE10 and higher.

## BUT WHY?

> Why create a front-end HTML sanitizer if the input has to be sanitized on the server anyway?

Users often copy-paste awful HTML generated by MS Word, MS Outlook or Apple Mail that needs a clean-up. Or you need to remove excessive formatting in an WYSIWYG editor. Or you need to display an (ugly) email message in a (beatuful) mobile app. Or (my favorite) you simply need to ease the load in the server-side sanitizer. And many many other use-cases.
