# Front End Coding and Formatting - LESS

 * [Namespacing](#namespacing)
 * [Formatting](#formatting)
 * [Selectors](#selectors)

------------------------------------------------

## Preface

The goal of this document is not to give rules that result in perfect code. It is so that with minimal effort the code will:
* Do what it is supposed to do
* Reduce the lead time required to understand an implementation
* Make it easier to establish what code can be reused
* Clarify how updates to an implementation should be styled or structured 

## Styles

<a name="namespacing">Namespacing</a>
  - All classes should be namespaced. In LESS this is relativly straight forward, wrap the entire document with a class that is the same as the pagename.
    - LESS

    ```css
    .PAGE_NAME-namespace {
      .class1 {
        // styles
      }
      .class2 {
        // styles
      }
    }
    ```

    - CSS

    ```css
    .PAGE_NAME-namespace .class1 {
      // styles
    }
    .PAGE_NAME-namespace .class2 {
      // styles
    }
  ```

<a name="formatting">Formatting</a>
  - Do not create a class for only one element; use the element ID instead
  - When specifying length values, do not specify units for a zero value, e.g., left: 0px; becomes left: 0;  
  - Use single quotes instead of double quotes for all strings
  - Where equivalent, use the opacity property instead of rgba(0, 0, 0, a)

<a name="selectors">Selectors</a>
  - Use the dash-format to name classes
  ```css
  .class-name-dashed {
    // styles
  }
  ```


  - Use two colons when addressing a pseudo-element (i.e. ::after, ::before, ::-webkit-scrollbar) for readability
  
  ```css
  a::after {
    // styles
  }
  ```

  - Only one selector should be on each line

  ```css
  // Good
  .raw-button-one,
  .raw-button-two,
  .raw-button-three {
    // styles
  }

  // Bad    
  .raw-button-one, .raw-button-two, .raw-button-three {
    // styles
  }
  ```

----------