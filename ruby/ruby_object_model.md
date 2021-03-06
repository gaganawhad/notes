#### The Ruby Object Model

These notes are dreived from [this talk](https://www.youtube.com/watch?v=X2sgQ38UDVY) given by Dave Thomas at a conference called Scotland on Rails

##### Introduction

- Book recommendation - Small Talk best practice patterns written by Kent Beck. It is applicable to ruby.
- Object orientation was not programming with classes. That was not how it was conceived.
- Inheritence is the work of the devil :)
- Ruby is a _pure_ Object oriented language, not class oriented language. (I am not sure I completely follow what he means here, but my guess is that ruby is unlike C++ in that if needed, each object can be made unique in its behavior such that it is inherited from a class that is unique to that object. This class is the eigen class concept).


##### Body

###### Self
- current object
- where instance variables are found
- default receiver for method calls.( i.e. when done without the the x.method_name format)

When does self change ?
- Only *2* things change slef
  - When you call a method
  - Class / Module definition

- Changing self when you Call a method:

```ruby
animal = "cat"
# animal gets a reference to the object "cat"
```

- `animal` is a reference to the object "cat"
- That `Object` has state and behavior
- state is stored in _that_ Object


- Fundamentally, all a Class is, in ruby, is an Object that contains a table of methods. For example, String class is a table of methods for string objects.
- it holds a pointer to another *ruby `Object`* that holds, as a part of _its state_ a table that has behavior definition of the methods (keeps behavior defintion DRY)
- _that_ table is the String class.
- the pointer that points to that table is the class pointer.
- `animal.class` will result in the String
- String itself is an object.


- Every method call in Ruby works the same way: It follows the following rule
    - go to its `class` `object` and find the method and invoke it.
    - If method is not found go to that objects parent and find the method and invoke it.
    - Continue finding the method in the hierarchy until you hit BasicObject/Object. ( Depending on the ruby version Object inherits from BasicObject).
- BasicObject has method definition for 'method_missing'
