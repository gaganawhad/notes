#### Chapter 1 - Introduction

- Rather than thinking TDD as a testing practice, we se it as a technique used to deliver high-quality code to testers, who are responsible for formal testing practices 

- When you are wearing the 'TDD hat', focus on red/green/refactor, design and documentation. Don't think about testing. Once you have developed a body of code, put on your 'tester hat', and think about all the thigns that could go wrong. This is where you add all the crazy edge cases, using exploratory testing to weed out the nasty bugs hiding in the cracks and documenting them as you discover them with more code examples. 

- The problem with testing an object's internal structure is that we're testing what an object _is_ instead of what it _does_. What an object _does_ is significantly more important. Brittleness can make test suites much more expensive to maintain is the primary reason for test suites to be become ignored and, ultimately discarded

#### Chapter 2 - Hello

_Nothing in particular that I felt should be noted_


#### Chapter 3 - Describing Features

- (User stores are an excellent way of describing the scope of a project or a release). When you write user stories, write them in the form of a role and a action.

- A user story should be
  - adding business value
  - testable
  - small enough to implement in one iteration 

- You don't have to stick to the Connextra format of describing a feature in the 'In order to...', 'As a .. ', 'I Should'. You can choose free form narratives, example when describing an algorithm

- In Cucumber, you can use `Scenario Outline` and a tabular format to dry up your scenario. Format on page 33


#### Chapter 4 - Automating features with Cucumber

- We should have an `env.rb` file in `features/support` directory. The `.rb` extension tells Cucumber that we're using Ruby.

- *TEST DOUBLE*: A fake object that pretends to be real object is called a test doupble. A 'test double' is a generic name for stubs, mocks, fakes, spies etc. 


#### Chapter 5 - Describing code with RSpec

- A strict adherence to a structure in which every object has a single example group and evry method has a single code example should be avoided! That sort of structure leads to long examples that take an object through many phases, setting expectations at several stopping points in each example. Examples like these are difficult to write to begin with, and much more difficult to uanderstand and debug later. 

- `spec_helper.rb` is required in every spec file and is stored in `spec/` directory. RSpec adds this directory to the global `$LOAD_PATH`. 

- 'describe()` method hooks into RSpec's API and returns a subclass of `RSpec::Core::ExampleGroup`. This is a group of examples of the expected behavior of an object. 

- The `it()` method creates an example. Technically it is an instance of `ExampleGroup` returned by `describe()`. 

- Each spec file requires `spec/spec_helper.rb`, which, incase of an standard ruby project requires `lib/my_project.rb` which inturn then requires all other files required for the project

- 'One expectation per example' is a good guideline to follow. The rationale there is that if there are two expectations in an example that should both fail given the implementation at that moment, we'll only see the first failure. No sooner do we meet that expectation than we discover that we haven't met the second expectation. If they live in separate examples, then they'll both fail, and that will provide us with more accurate information than if only one of them is failing. 

- `as_null_object`: The book talks about this but doesn't really explain it. Only mentions that it is a design pattern described in 'Pattern Languages of Program Design 3' and is supported by RSpec's `double` framework. - bad book

- `let(:method) {}` 
        - takes a symbol representing a method name and a block, which represents the implementation of that method
        - it comes with inbuilt memoization


#### Chapter 6 - Adding new features

_Nothing in particular that I felt should be noted_

#### Chapter 7 - Specifying an Algorithm

- One of the principles of TDD is writing only enough code to get a failing test to pass - independent of other tests that are still to be worked on. One of the difficult things for people new to TDD is to accept code we know with some certainity is going to change. That it's not the implementation we are going to want when we are finished. 

- One of the benifits of progressing in small steps is that when we introduce a new failure, we know exactly what we did, so we have context in which we can analyze the failure. 

#### Chapter 8 - Refactoring with Confidence

- Generally we want to avoid writing procedural code (like `each` loops) because it has a tendency to grow in complexity and become progressively difficult to understand and maintain.

- Using temp variables within methods should be avoided as it adds to complexity especially as it can get assiged values in several ways, and then its hard to fix bugs.

- "Extract Class" refactoring which the book discusses on pages 86 to 93 was challenging and something I don't easly have a smell for. Refer to the book if you want to think/meditate/read about it again.

- Refactoring can be addictive. Every time we do one refactoring, our attention is drawn to an area of the code we may not have focused on before. We could continue refactoring for ever, but eventually we have to stop and move on.   

- *Exploratory Testing* is a practice in which we discover the behavior of an application by interacting with it directly. We havent tested the app until we haven't interacted with it because BDD / TDD is a design practice, not a testing practice. It by itself fails to unearth all of the corner cases that we'll naturally discover by simply using the software. 

- Refactoring is impossible without a test suite.

#### Chapter 9 - Feeding back what we have learnt

_This chapter is written mostly to walk you through a BDD process and applying principles, techniques etc. that have been covered in the previous chapters of this book. Nothing new to note here_

#### Chapter 10 - The Case for BDD & 

_This chapter spends time in looking into the history of traditional software projects, some analysis of why they fail, and gives some history and philosophy of agile software engineering._

#### Chapter 11 - Writing Software That Matters

- *Behavior Driven Development* is about implementing an application by describing its behavior from the perspective of its stakeholders. It started as a simple reframing of Test Driven Devlopment. It implies that there is more than one stakeholder. We don't just look at the world from the point of view of an end user or the person paying the bills but anyone with an interest in the project.

- The philosophy of BDD - 'writing software that matters' means that we write software that has value to a stakeholder that is neither too little to solve the problem nor over-engineered, and that we can demonstrate that it works. It can be summed up in: 
        1. Enough is enough: Don't do anything less that whats needed to get started but don't do any more either. 
        2. Deliver stakeholder value: If you are doing something that isn't either delivering value to the stakeholder or increasing your ability to deliver value, stop doing it and do something else. 
        3. It's all behavior: Behavior is described at any level of granularity - application, module, class, unit etc. 


- A *Stakeholder* is anyone who cares about the project in question. The people whose problems we are trying to solve are called _core stakeholders_ and the people who are goin to help solve it are called _incidental stakeholders_.

- From a BDD perspective, there is no such thing as 'non functional requirement', just a feature with an incidnetal stakeholder.

- A 'feature' in BDD is more useful from the point of view of a stakeholder and a 'story' is more useful from th point of view of the team delivering the feature. In Cucumber stories are scenarios.


#### Chapter 12 - Code Examples

- Describe and context are aliases. `describe` is used for objects and `context` to describe contexts. 

- When no block is passed to `it`, RSpec considers it to be pending. When a block is passed when nothing is written in it, RSpec considers it to be a passing test. You can also use `pending` to explicitly write a message for why it's pending. Especially useful when you have written a failing test but don't want it to break the test suite.

- It is a bad practice to use `before(:all)` to initailize instance variables that get passed throught he tests - ie the `it` blocks. This is because the state leaks into other `it` blocks and causes problems / bugs that are _very_ hard to fix.

- `after(:each)` is guaranteed to run after each example, even if there are failures or errors - so it is reliable
