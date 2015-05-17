#### Chapter 1 - Designing Classes with SRP

  Notes are not particularly in order in the way they appear in the chapter. Neither do they match word for word.

  Notes on Design:

  - Your goal is to model your application, using classes, such that it does what it is supposed to do _right now_ and is also easy to change _later_.

  - \* Design is more an art of preserving changeability than it is the act of achieving perfection \*

  - When future cost of doing nothing is the same as the current cost, postpone the decision. The most effective course of action to change may be to wait for more information.

  - Improve it now v/s improve it later tension has always exists. Applications are never perfect and each choice has a price. A good designer understands this tension and minimizes costs by making informed tradeoffs between the needs of the present and the possibilities of the future.

  - When writing initialize methods - if you can control it, pass in a meaningful object. If not, write clean (private) methods to hide the mess.

  - Some Refactoring is needed even when you don't know the ultimate design not because the design is clear, but because it isn't.

  - Because you are writing changeable code, you are best served by postponing decisions until you are absolutely forced to make them.

  - How to determine if a Class violates SRP ?
    \* One way is to pretend it is sentient and to prepare questions corresponding to the methods/behavior of the class. If the question comes across as awkward, and it feels like the class shouldn't be answering that question, then it probably doesn't follow SRP. \*

  - SRP doesn't require that a class do only one very narrow thing, but that it is cohesive. i.e. everything the class does be highly related to its purpose.

  - Using behavior / method instead of data / instance variable is always better
    This is because if the value of the instance variable becomes more complex it is easier to change it within a method than as data. So always use accessor methods instead of instance variables.

  - *Direct references to complicated data structures are confusing, because they obscure what the data really is, and they are a maintenance nightmare, because every reference will need to change if the structure ( for example, array) changes.* Tip Use ruby Struct class to wrap a structure.  

  - Struct - A convenient way to bundle a number of attributes together, using accessor methods, without having to write an explicit class.
    Use Struct / OpenStruct to quickly convert a data structure to an object
    ```ruby
    class Bicycle
      attr_reader :wheels

      def initialize(data)
        @wheels = wheelify(data)
      end

      Wheel = Struct.new(:rim, :tire)
      def wheelify(data)
        data.collect do |cell|
          Wheel.new(cell[0], cell[1])
        end
      end
    end
    # Bicycle.new([[2,3],[3,5]])
    ```
