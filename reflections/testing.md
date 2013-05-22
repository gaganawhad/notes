#### Testing

- When writing tests, you should not focus on what an object is, but on what the object does. What this object does is vastly more important

- It is important that you write a failing test first and see if fail. If you don't do that you can't tell if the test you wrote doesn't capture the scenario story you need to implement and that the code you wrote does what you think it does

- Fast feedback cycle is important to a good design in general, and specifically when testing your code. It is important that your test suite runs as fast as you can get it to. 

- *Tradeoffs:* 'One expectation per example' is a good guildeline to follow. That way if one expectation fails, and you fix it you don't see the second expectation failing (for some other reason). The idea is that you should see all failing expectations at once so that you have accurate information. To have only one expectation per example, you would have to move setting up your data outside the example to DRY things up. Now, since it seems that using `before(:all)` is so highly discouraged, you would go to using `before(:each)`. But then thats going to slow down your test suite, and a slow test suite isn't fun. Just some refelctions about tradeoffs in these testing principles. Using the `let()` function is one way to handle things, because it comes with inbuilt memoization, but it still doesn't solve the situation of a database, ie creating and destroying the database for the example-group.

- BDD/TDD is a design practice not a tesing practice. Driving out behavior with examples fails to unearth all the corner cases, that will be naturally discovered by simply using the software. 

- When you are testing code, it is really important that you don't test implementation (or what the object is) but behavior (i.e. what the object is doing). When applied that to acceptance testing, why should we test controllers?  

- Sandi Metz agrees that we shouldn't test controllers in acceptance testing - "Don't put any logic in controllers and don't test your controllers" 

- When you are writing Object Oriented Software, you think in terms of classes and think through where and how code should be organized. It makes sense to think through the structure when you are doing that. However, when writing tests focus solely on each test/example. The idea is that you write that tests well, and don't make it brittle. Don't worry about example groups, or setting up data efficiently. They are just tools to help you write better tests and maintain a better suite - but not at the cost of wirting a good test. You can worry about keeping things DRY, setting up data, setting up example groups and speeding up the test suite when refactoring the tests.  

- When you want to test for making sure that say 50 objects are returned in a collection by a method, you might want to make the number 50 a variable, and have a smaller variable be passed in your actuall tests, like 5, and test that ther aren't 6 records returned by the method. Suppose you are testing for pagination and want to make sure that 50 records are returned and not 51. You don't want to create 50 records because such things can slow down your tests. Myron Marston recommends that he would "tend to make the page size configurable in some way (maybe even just by stubbing the constant), and then set it to a small value in your test and create one more record than that"

- When writing tests you want to think through what is worth testing? In for-profit business there is a easier co-relation between functioning code and how much money they make, and so it make sense to write better and more comprehensive tests that could break easily. The opposite would apply to other areas of code testing. 

- Writing 100% test coverage isn't a good practice. 

- When you start working on a new project, start writing acceptance tests. Don't focus too tightly on unit tests. The code that you will write is too volatile. When it starts talking a form, then you can start writing and locking down unit tests. 
