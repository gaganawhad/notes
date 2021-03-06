#### Good coding practices (General)

- Generally avoid writing procedural code (like `each` loops) because it has a tendency to grow in complexity and become progressively difficult to understand and maintain.

- Temporary variables within methods are troublesome because they tend to change state within a method. As a method grows longer, this makes it easier to introduce bugs based on poor understanding of the state of that variable at any given moment in the method. If anything goes wrong in any of the times the local variable is initialized, it is difficult to track down where the problem is occuring.


From: _The RSpec Book_

- Using memoization on class methods is an antipattern. Use Rails caching if necessary. It should be safe to use memoization on instance methods

  ted dumitrescu [careful what you memoize](http://cmme.org/tdumitrescu/blog/2014/01/careful-what-you-memoize/)
