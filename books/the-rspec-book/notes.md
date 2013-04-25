#### Chapter 12 - Code Examples

- Describe and context are aliases. `describe` is used for objects and `context` to describe contexts. 

- When no block is passed to `it`, RSpec considers it to be pending. When a block is passed when nothing is written in it, RSpec considers it to be a passing test. You can also use `pending` to explicitly write a message for why it's pending. Especially useful when you have written a failing test but don't want it to break the test suite.

- It is a bad practice to use `before(:all)` to initailize instance variables that get passed throught he tests - ie the `it` blocks. This is because the state leaks into other `it` blocks and causes problems / bugs that are _very_ hard to fix.

- `after(:each)` is guaranteed to run after each example, even if there are failures or errors - so it is reliable
