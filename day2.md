## Reading notes
### You-Dont-Know-JS/get-started
#### ch2
- `var` does not have block scoping
- `===` sometimes can lie
  - use `Number.isNan(..)` and `Object.is(...)` (more precise than `===`) instead
  - ```
    NaN === NaN;            // false
    0 === -0;               // true 
    ```
- Two organization patterns in JS
  - Classes and Classes inheritance
  - Modules
    - no `this` and `new` used, data and methods can be hidden
    - ```
      function Publication(title,author,pubDate) {
      var publicAPI = {
        print() {
            console.log(`
                Title: ${ title }
                By: ${ author }
                ${ pubDate }
            `);
        }
      };
      return publicAPI;
      }
      function Book(bookDetails) {
      var pub = Publication(
        bookDetails.title,
        bookDetails.author,
        bookDetails.publishedOn
      );

      var publicAPI = {
        print() {
            pub.print();
            console.log(`
                Publisher: ${ bookDetails.publisher }
                ISBN: ${ bookDetails.ISBN }
            `);
          }
        };

        return publicAPI;
      }
      var YDKJS = Book({
        title: "You Don't Know JS",
        author: "Kyle Simpson",
        publishedOn: "June 2014",
        publisher: "O'Reilly",
        ISBN: "123456-789"
      });
      YDKJS.print();
      ```
  - ES modules
    - modern way of modules
    - ED module vs classic module
      1. No wrapping function
      2. Use `export` to expose methods
      3. Use `import` to instantiate, thus singleton. If multiple instances required, then the classical module or class must be used, which can be imported using from ES modules as well