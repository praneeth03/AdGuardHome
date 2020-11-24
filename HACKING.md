 #  *AdGuardHome* Developer Guidelines

As of **2020-11-20**, this document is still a work-in-progress.  Some of the
rules aren't enforced, and others might change.  Still, this is a good place to
find out about how we **want** our code to look like.

The rules are mostly sorted in the alphabetical order.

##  *Git*

 *  Call your branches either `NNNN-fix-foo` (where `NNNN` is the ID of the
    *GitHub* issue you worked on in this branch) or just `fix-foo` if there was
    no *GitHub* issue.

 *  Follow the commit message header format:

    ```none
    pkg: fix the network error logging issue
    ```

    Where `pkg` is the package where most changes took place.  If there are
    several such packages, or the change is top-level only, write `all`.

 *  Keep your commit messages, including headers, to eighty (**80**) columns.

 *  Only use lowercase letters in your commit message headers.  The rest of the
    message should follow the plain text conventions below.

    The only exceptions are direct mentions of identifiers from the source code
    and filenames like `HACKING.md`.

##  *Go*

 *  <https://github.com/golang/go/wiki/CodeReviewComments>.

 *  <https://github.com/golang/go/wiki/TestComments>.

 *  <https://go-proverbs.github.io/>

 *  Add an empty line before `break`, `continue`, and `return`, unless it's the
    only statement in that block.

 *  Avoid `init` and use explicit initialization functions instead.

 *  Avoid `new`, especially with structs.

 *  Document everything, including unexported top-level identifiers, to build
    a habit of writing documentation.

 *  Constructors should validate their arguments and return meaningful errors.
    As a corollary, avoid lazy initialization.

 *  Don't put variable names into any kind of quotes.

 *  Don't use naked `return`s.

 *  Don't use underscores in file and package names, unless they're build tags
    or for tests.  This is to prevent accidental build errors with weird tags.

 *  Don't write code with more than four (**4**) levels of indentation.  Just
    like [Linus said], plus an additional level for an occasional error check or
    struct initialization.

 *  Eschew external dependencies, including transitive, unless
    absolutely necessary.

 *  Name benchmarks and tests using the same convention as examples.  For
    example:

    ```go
    func TestFunction(t *testing.T) { /* … */ }
    func TestFunction_suffix(t *testing.T) { /* … */ }
    func TestType_Method(t *testing.T) { /* … */ }
    func TestType_Method_suffix(t *testing.T) { /* … */ }
    ```

 *  Name the deferred errors (e.g. when closing something) `cerr`.

 *  No `goto`.

 *  No shadowing, since it can often lead to subtle bugs, especially with
    errors.

 *  Prefer constants to variables where possible.  Reduce global variables.  Use
    [constant errors] instead of `errors.New`.

 *  Put comments above the documented entity, **not** to the side, to improve
    readability.

 *  Use `gofumpt --extra -s`.

    **TODO(a.garipov):** Add to the linters.

 *  Use linters.

 *  Use named returns to improve readability of function signatures.

 *  When a method implements an interface, start the doc comment with the
    standard template:

    ```go
    // Foo implements the Fooer interface for *foo.
    func (f *foo) Foo() {
        // …
    }
    ```

 *  Write logs and error messages in lowercase only to make it easier to `grep`
    logs and error messages without using the `-i` flag.

 *  Write slices of struct like this:

    ```go
    ts := []T{{
            Field: Value0,
            // …
    }, {
            Field: Value1,
            // …
    }, {
            Field: Value2,
            // …
    }}
    ```

[constant errors]: https://dave.cheney.net/2016/04/07/constant-errors
[Linus said]:      https://www.kernel.org/doc/html/v4.17/process/coding-style.html#indentation

##  *Markdown*

 *  **TODO(a.garipov):** Define our *Markdown* conventions.

##  Text, Including Comments

 *  End sentences with appropriate punctuation.

 *  Headers should be written with all initial letters capitalized, except for
    references to variable names that start with a lowercase letter.

 *  Start sentences with a capital letter, unless the first word is a reference
    to a variable name that starts with a lowercase letter.

 *  Text should wrap at eighty (**80**) columns to be more readable, to use
    a common standard, and to allow editing or diffing side-by-side without
    wrapping.

    The only exception are long hyperlinks.

 *  Use U.S. English, as it is the most widely used variety of English in the
    code right now as well as generally.

 *  Use double spacing between sentences to make sentence borders more clear.

 *  Use the serial comma (a.k.a. *Oxford* comma) to improve comprehension,
    decrease ambiguity, and use a common standard.

 *  Write todos like this:

    ```go
    // TODO(usr1): Fix the frobulation issue.
    ```

    Or, if several people need to look at the code:

    ```go
    // TODO(usr1, usr2): Fix the frobulation issue.
    ```

##  *YAML*

 *  **TODO(a.garipov):** Define naming conventions for schema names in our
    *OpenAPI* *YAML* file.  And just generally OpenAPI conventions.

 *  **TODO(a.garipov):** Find a *YAML* formatter or write our own.

 *  All strings, including keys, must be quoted.  Reason: the [*NO-rway Law*].

 *  Indent with two (**2**) spaces.  *YAML* documents can get pretty
    deeply-nested.

 *  No extra indentation in multiline arrays:

    ```yaml
    'values':
    - 'value-1'
    - 'value-2'
    - 'value-3'
    ```

 *  Prefer single quotes for strings to prevent accidental escaping, unless
    escaping is required or there are single quotes inside the string (e.g. for
    *GitHub Actions*).

 *  Use `>` for multiline strings, unless you need to keep the line breaks.

[*NO-rway Law*]: https://news.ycombinator.com/item?id=17359376
