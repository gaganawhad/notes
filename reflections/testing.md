#### Testing

- When writing tests, you should not focus on what an object is, but on what the object does. What this object does is vastly more important

- It is important that you write a failing test first and see if fail. If you don't do that you can't tell if the test you wrote doesn't capture the scenario story you need to implement and that the code you wrote does what you think it does

- Fast feedback cycle is important to a good design in general, and specifically when testing your code. It is important that your test suite runs as fast as you can get it to. 

- *Tradeoffs:* 'One expectation per example' is a good guildeline to follow. That way if one expectation fails, and you fix it you don't see the second expectation failing (for some other reason). The idea is that you should see all failing expectations at once so that you have accurate information. To have only one expectation per example, you would have to move setting up your data outside the example to DRY things up. Now, since it seems that using `before(:all)` is so highly discouraged, you would go to using `before(:each)`. But then thats going to slow down your test suite, and a slow test suite isn't fun. Just some refelctions about tradeoffs in these testing principles. Using the `let()` function is one way to handle things, because it comes with inbuilt memoization, but it still doesn't solve the situation of a database, ie creating and destroying the database for the example-group.

- BDD/TDD is a design practice not a tesing practice. Driving out behavior with examples fails to unearth all the corner cases, that will be naturally discovered by simply using the software. 
