# Front End Coding and Formatting - HTML

 * [Naming](#naming)
 * [Formatting](#formatting)
 * [Page Layout](#layout)

------------------------------------------------

## Preface

The goal of this document is not to give rules that result in perfect code. It is so that with minimal effort the code will:
* Do what it is supposed to do
* Reduce the lead time required to understand an implementation
* Make it easier to establish what code can be reused
* Clarify how updates to an implementation should be styled or structured 

## Styles

<a name="naming">Naming</a>
  - pageName.xsl file in the xsl/PATH/pages folder  
  - pageName.js file in the js/PATH/pages folder  
  - pageName.less file in the css/PATH/pages folder  

<a name="formatting">Formatting</a>
  - Indent all lines using two spaces
  - Do not use ```<br/>```, place blocking elements like ```<div>``` as appropriate
  - Do not use ```<div>``` tags for spacing-only, modify the margin of the surrounding ```<div>``` tags
  - Tag attributes should use double-quotes, not sinqle-quotes
  - Use the ```<button>``` element instead of ```<input type="button">```
  - Only use ```<table>``` elements when displayng tabular data
  - The id attribute should be in camelCase so that is matches the JavaScript conventions ```<div id="myPage">Contents</div>```
  - If tags contain more than a small amount of content then the opening and closing tags should be placed on separate lines

```html
<!-- Good -->
<div>
  <a href="#">Link Here</a>
  This is a test
</div>

<!-- Bad -->
<div><a href="#">Link Here</a>This is a test</div>
```

<a name="layout">Page Layout</a>  
  - The ```<body>``` tag should have the attribute class="pageName-ns" set  
  - Inline JavaScript - This should be avoided when possible. Use a binding event in the external pageName.js file.  
  - Inline CSS - This should be avoided when possible. When needed add a new class to the element and define the changes in the external PAGE_NAME.less file.

```html
<html>
  <header>
    <title>My Page</title>
    <link rel="stylesheet" type="text/css" href="bootstrap3.css" />
    <link rel="stylesheet" type="text/css" href="pageName.css" />
  </header>
  <body class="pageName-ns">
  </body>
  <footer>
  </footer>
  <script type="text/javascript" src="jquery-1.10.2.js">&#160;</script>
  <script type="text/javascript" src="pageName.js">&#160;</script>  
</html>
```

----------
