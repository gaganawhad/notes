#### Chapter 1 - Object oriented design

##### Introduction

- If an application lives long enough, that is, if it succeeds, its biggest problem will become that of dealing with change. Arranging code to efficiently accommodate change is a matter of design. The most visible elements of design are principles and patterns.

- The trick to get most bang for your design buck is to acquire an understanding of the theories of design and to apply these theories appropriately, at the right time, in the right amounts.

- Unfortunately, even applying principles correctly and using patterns appropriately does not guarantee the creation of an easy-to-change application.

##### Design - Praise, principles, patterns judgements etc.

- OOD requires that you shift from thinking of the world as a collection of predefined procedures to modeling the world as a **_series of messages_ that pass between objects**. Object oriented applications are made up of the objects and the messages that pass between them. _Messages_ will turn out to be the more important of the two.  (Messages, is mostly the methods we write. They encapsulate behavior. While it is important to put behavior in the right object, the behavior itself is more important)

- **The programming techniques that make code a joy to write overlap with those that most efficiently produce software**.

- **Getting the right message to the correct target object requires that the sender of the message know things about the receiver. This knowledge creates dependencies between the two and these dependencies stand in the way of change. OOD is about _managing dependencies_. It is a set of coding techniques that arrange dependencies such that objects can tolerate change**.

- For any period of time that extends past initial delivery of the beta, the cost of change will eventually eclipse the original cost of the application.

- The purpose of design is to allow you to design _later_, and its primary goal is to reduce the cost of change.

- The ultimate software metric would be _cost per feature over the time interval that matters_, but this is not easy to calculate. Cost, feature and time are individually difficult to define, track and measure.

- Making a design compromise by borrowing time from the future is known as taking on _technical debt_.

- Because your goal is to write software with the lowest cost per feature, your decision about how much design to do depends on two things: your skills and your timeframe. When the act of design prevents software from being delivered on time, you have lost.


###### Procedural languages
- In procedural languages, different kinds of data are called _data-types_. Each _data-type_ describes itself. Because _you_ create variables, you know what data-types they hold. Your expectations about which operations you can use are based on your knowledge of a variable's data-type.

- In procedural languages, there is a chasm between data and behavior. Data is one thing, behavior is completely different. Data gets packaged into variables and then passed around to behavior, which could, frankly, do anything to it. There is no way of knowing what happens to data once it is passed. The influence on data can be unpredictable and largely untraceable.


###### Object Oriented languages

- Object oriented programming is object-oriented _relative_ to non object oriented languages, or _procedural_ languages.

- In OO languages, data-types from procedural languages map to classes. Example Ruby has a `String` object instead of a string data-type. In fact there is a pre-existing class for every data type that you would expect a programming language to supply.

- In Ruby an object may have may _types_. One of its types, will always come from its _class_. Knowledge of an object's _type(s)_ therefore lets you have _expectations_ about the messages to which it responds.

- **Each OO application gradually becomes a unique programming language that is specifically tailored to your domain.**
