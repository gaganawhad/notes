
When a unary `&` operator  is called on a object that is not a Block or a Proc it
  - first calls `#to_proc` on the object
  - then converts it into a Block
    (It is called in the context of a method call.)

  Examples:

  Using a simple proc:
    ```ruby
    proc { |a| a.to_s}
    => #<Proc:0x007fcf9a0ab358@(irb):38>

    a.call
    => ArgumentError: no receiver given

    a.call(1)
    => "1"

    a.call(1, 2)
    => "1"
    ```

  Actually converting a symbol to proc

    ```ruby
    b = :to_s.to_proc
    => #<Proc:0x007fa2cb825dc8(&:to_s)>

    b.call
    => ArgumentError: no receiver given

    b.call(1)
    => "1"

    b.call(1, 2)
    => "1"
    ```

  Using unary `&` operator

    ```ruby
    def my_method_1
      yield
    end

    def my_method_2
      yield(1)
    end

    def my_method_3
      yield(1, 2)
    end

    my_method_1(&:to_s)
    => ArgumentError: no receiver given
    my_method_2(&:to_s)
    => "1"
    my_method_3(&:to_s)
    => "1"

    ```
