### Route Templates

| Route Template                           | Example Matching URI    | The request URI…                                                            |
| ---------------------------------------- | ----------------------- | --------------------------------------------------------------------------- |
| `hello`                                  | `/hello`                | Only matches the single path `/hello`.                                      |
| `{Page=Home}`                            | `/`                     | Matches and sets `Page` to `Home`.                                          |
| `{Page=Home}`                            | `/Contact`              | Matches and sets `Page` to `Contact`.                                       |
| `{controller}/{action}/{id?}`            | `/Products/List`        | Maps to the `Products` controller and `List` action.                        |
| `{controller}/{action}/{id?}`            | `/Products/Details/123` | Maps to the `Products` controller and `Details` action with`id` set to 123. |
| `{controller=Home}/{action=Index}/{id?}` | `/`                     | Maps to the `Home` controller and `Index` method. `id` is ignored.          |
| `{controller=Home}/{action=Index}/{id?}` | `/Products`             | Maps to the `Products` controller and `Index` method. `id` is ignored.      |

### Complex segments

Complex segments are processed by matching up literal delimiters from right to left in a [non-greedy](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/routing?view=aspnetcore-11.0#complex-segments) way. For example, `[Route("/a{b}c{d}")]` is a complex segment. Complex segments work in a particular way that must be understood to use them successfully. The example in this section demonstrates why complex segments only really work well when the delimiter text doesn't appear inside the parameter values. Using a [regex](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expressions) and then manually extracting the values is needed for more complex cases.