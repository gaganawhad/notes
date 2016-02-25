#### Blocks, Procs and Lambdas

##### TL;DR

  - Lambdas and Procs are `Proc`s
  - Lambdas are strict argument checkers, while procs are not.
  - Using the unary ampersand operator - `&` on lambdas or procs, actually converts them to Blocks
  - You are better off not worrying about the whole `return` statement issue. Use documentation, like this,
    when face a problem that requires the knowledge. 

##### Simple Procs

- A simple proc can be defined using `Proc.new` or `proc`. It can be referenced!

  ```ruby
  proc{|x| puts x }
  => #<Proc:0x007fccd30c7d10@(irb):8>
  a = Proc.new{|x| puts x }
  => #<Proc:0x007fccd307e0e8@(irb):9>
  a
  => #<Proc:0x007fc6b3838700@(irb):9>
  ```

- A simple proc is a `Proc`

  ```ruby
  proc{|x| puts x}.is_a?(Proc)
  => true
  ```

- A simple proc's lambda status is `false`

  ```ruby
   proc{|x| puts x}.lambda?
  => false
  ```

- Simple procs are not strict argument checkers

  ```ruby
  a = proc{|x| puts x}
  => #<Proc:0x007fc6b305ab28@(irb):11>
  a.call(4)
  4
  => nil
  a.call(4, 5)
  4
  => nil
   ```

- The unary `&` operator, when called on a Simple Proc converts it into a block maintaining the lambda status. This
  can be used only in the context of a method call.

  ```ruby
  def block_or_proc_or_lambda(&my_block)
    puts my_block.lambda?
    puts my_block.class
    my_block.call
  end

  a = proc { |ignored, arguments| puts 'hello' }
  => #<Proc:0x007f98bb1195a8@(irb):73>

  block_or_proc_or_lambda(&a)
  false
  Proc
  hello
  => nil

  def yield_block
    yield
  end

  yield_block(&a)
  hello
  => nil
  ```


- If a `return` exists within a simple proc, it exposes the return on the outside scope. If called as is, it returns
  an `LocalJumpError` exception, just as calling a `return` outside a method would do.

  ```ruby
  return 3
  LocalJumpError: unexpected return

  a = proc{|x| puts x; return x}
  => #<Proc:0x007fc6b3a66590@(irb):19>
  a.call(3)
  3
  LocalJumpError: unexpected return
  ```

- When used with return statement within a method, the method respects the return of the simple proc

  ```ruby
  def batman_ironman_proc
    victor = Proc.new { return "Batman will win!" }
    victor.call
    "Iron Man will win!"
  end

  puts batman_ironman_proc
  Batman will win!
  => nil

  ```

  I find this incredibly strange:
  BUT when it is passed as an argument... it raises the `LocalJumpError:`

  ```ruby
  victor = proc { return "Batman will win!" }
  def batman_ironman_proc(victor)
    victor.call
    "Iron Man will win!"
  end

  batman_ironman_proc(victor)
  => LocalJumpError: unexpected return

  def batman_ironman_proc_block
    yield
    "Iron Man will win!"
  end

  batman_ironman_proc_block(&victor)
  "Iron Man will win!"
  LocalJumpError: unexpected return
```

##### Lambda Procs

- It can be defined using `lambda` or `->()`. It can be referenced!

  ```ruby
  ->(x){ puts x}
  => #<Proc:0x007fa44983b220@(irb):17 (lambda)>
  a = lambda{|x| puts x }
  => #<Proc:0x007fccd314cdd0@(irb):6 (lambda)>
  a
  => #<Proc:0x007fccd314cdd0@(irb):6 (lambda)>
  ```


- A lamdba is a `Proc`

  ```ruby
  ->(x){ puts x}.is_a?(Proc)
  => true
  ```

- A lamdba's lambda status is `true`

  ```ruby
  ->(x){ puts x}.lambda?
  => true
  ```

- Lambda's are strict argument checkers. Like methods they can through an `ArgumentError` exception

  ```ruby
 a = lambda{|x| puts x}
  => #<Proc:0x007fc6b384ac98@(irb):8 (lambda)>
  a.call(4)
  4
  => nil
  a.call(4, 5)
  ArgumentError:
  ```

- The unary `&` operator, when called on a Simple Proc converts it into a block maintaining the lambda status. This
  can be used only in the context of a method call.

  ```ruby
  a = lambda {|unignored, arguments| puts 'hello' }
  => #<Proc:0x007f98bb0ebae0@(irb):83 (lambda)>
  block_or_proc_or_lambda(&a)
  true
  Proc
  ArgumentError: wrong number of arguments (given 0, expected 2)

  a = lambda { puts 'hello' }
  block_or_proc_or_lambda(&a)
  true
  Proc
  hello
  => nil
  ```

- Lambda procs can return a value when with a `return` statement when called

  ```ruby
  a = lambda{|x| puts x; return x}
  => #<Proc:0x007fc6b3a74578@(irb):21 (lambda)>
  a.call(3)
  3
  => 3
  ```

- When used with a return statement within a method, it ignores the `return` of the lambda proc.
  (As a note, this is what I find most surprising)

  ```ruby
  def batman_ironman_lambda
    victor = lambda { return "Batman will win!" }
    victor.call
    "Iron Man will win!"
  end

  puts batman_ironman_lambda
  Iron Man will win!
  => nil
  ```

  AND it can also be passed in as an argument without raising any errors.

  ```ruby
  victor = lambda { return "Batman will win!" }

  def batman_ironman_lambda
    yield
    "Iron Man will win!"
  end

  batman_ironman_lambda(&victor)
  => "Iron Man will win!"

  def batman_ironman_lambda(&victor)
    victor.call
    "Iron Man will win!"
  end

  batman_ironman_lambda(&victor)
  => "Iron Man will win!"
  ```



##### Blocks

- Blocks can't exist independently. They cannot be defined or referenced:

  ```ruby
  { puts 'hello world' }
  => SyntaxError
  a = { puts 'hello world' }
  => SyntaxError
  ```

- The unary `&` operator, when called on a Block converts it into a simple proc. (Which by the way, can only be called
  within the context of a method)

  ```ruby

  block_or_proc_or_lambda do |ignored, arguments|
    puts 'hello'
  end
  false
  Proc
  hello
  => nil
  ```

  FYI:
  ```ruby
  &{puts 'hello'}
  SyntaxError
  ```

- If a `return` exists within a block, even though it gets converted to a simple proc when passed to a method,
  it raises a `LocalJumpError`
  ```ruby
  block_or_proc_or_lambda do
    puts 'hello'
    return 4
    puts 'world'
  end

  false
  Proc
  hello
  LocalJumpError: unexpected return
  ```
