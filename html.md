# Front End Coding and Formatting - HTML

 * [Naming](#naming)
 * [Formatting](#formatting)
 * [Page Layout](#layout)

------------------------------------------------

## Preface

The goal of this document is not to give rules that result in perfect code. It is so that with minimal effort the code will:
* do what it is supposed to do
* be easily understood
* be easily maintained

## Styles

1. <a name="naming">Naming</a>
- PAGE_NAME.xsl file in the xsl/PATH/pages folder
- PAGE_NAME.js file in the js/PATH/pages folder
- PAGE_NAME.less file in the css/PATH/pages folder


2. <a name="formatting">Formatting</a>
- Indent all lines using two spaces
- Do not use <br/>, place blocking elements like <div> as appropriate
- Do not use <div> tags for spacing-only, modify the margin of the surrounding <div> tags
- Tag attributes should use double-quotes, not sinqle-quotes
- Use the <button> element instead of <input type="button">
- Only use <table> elements when displayng tabular data
- The id attribute should be in camelCase so that is matches the JavaScript that uses it more often

- If tags contain more than a small amount of content then the opening and closing tags should be placed on separate lines

```
Bad:
<div><a href="#">Link Here</a>This is a test</div>

Good:
<div>
  <a href="#">Link Here</a>
  This is a test
</div>

```

3. <a name="layout">Page Layout</a>
- The <body> tag should have the attribute class="PAGE-NAME-NS" set
- Inline JavaScript - This should be avoided when possible. Use a binding event in the external PAGE_NAME.js file.
- Inline CSS - This should be avoided when possible. When needed add a new class to the element and define the changes in the external PAGE_NAME.less file.


```
<html>
  <header>
    <title>My Page</title>
    <link rel="stylesheet" type="text/css" href="/css/shared/dhbootstrap3.css" />
  </header>
  <body class="page-name-ns">
  </body>
  <footer>
  </footer>
  <script type="text/javascript" src="/js/shared/jquery-1.10.2.js">&#160;</script>
</html>
```

----------