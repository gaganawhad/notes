#### Exceptions

- _I tried to search for the difference between an Exception and an Error. It seems that in languages other than ruby, an Exception is an unusal sitation (as the meaning of the word implies). It's meant to be caught. An error on the other hand, is just something going completely wrong. In Ruby, the concepts of Exception and Error seem to coincide._

- Ruby has its own [Exception class hierachy](http://blog.nicksieger.com/articles/2006/09/06/rubys-exception-hierarchy/).

- When you need to raise an exception, you can use one of the built-in Exception classes, or you can create one of your own. Make your own exceptions are subclasses of *StandardError* or one of its children. If you don't, your exception won't be caught. 

- When an exception is raised, and independent of any subsequent excpetion handling, Ruby places a reference to the associated Exception object into the global variable `$!`. _However, in common usage, the object is often assigned to a local variable._

- `rescue` clause 
  - For the rescue clause to get executed, the raised exception should match the parameter passed to `rescue`. The match will get executed if the exception named in the rescue clause is the same as the type of the currently thrown exception or is a superclass of that exception. 
  - If you write the rescue clause with no parameter list, the parameter defaults to `StandardError`

- `ensure` clause
  - Sometimes you need to guarantee that some processing is done at the end of a block of code, regardless of whether an exception was raised. Use the `ensure` clause in that case. `ensure` goes after the last `rescue` clause. 

- `else` clause
  - If present, it goes after the `rescue` clauses and before any `ensure`.  The body of the `else` clause is executed only if no exceptions are raised by the main body of code.

- `raise`
  - `raise` simply raises current exception (stored in `$!`) or a `RuntimeError` if there is no current exception.
  - `raise "error message here"` raises a new `RuntimeError` exception, setting its message to the given string (without the trace) Example: 

```
      raise "error message here"
      RuntimeError: error message here
      from (irb):6
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands/console.rb:90:in `start'
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands/console.rb:9:in `start'
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands.rb:62:in `<top (required)>'
      from bin/rails:4:in `require'
      from bin/rails:4:in `<main>'
```
  - `raise InterfaceException, "Keyboard failure", caller` raises exception and shows the trace
```
      raise RuntimeError, "error message here", caller
      RuntimeError: error message here
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/workspace.rb:86:in `eval'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/workspace.rb:86:in `evaluate'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/context.rb:380:in `evaluate'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:492:in `block (2 levels) in eval_input'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:624:in `signal_status'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:489:in `block in eval_input'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/ruby-lex.rb:247:in `block (2 levels) in each_top_level_statement'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/ruby-lex.rb:233:in `loop'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/ruby-lex.rb:233:in `block in each_top_level_statement'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/ruby-lex.rb:232:in `catch'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb/ruby-lex.rb:232:in `each_top_level_statement'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:488:in `eval_input'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:397:in `block in start'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:396:in `catch'
      from /Users/gagan/.rvm/rubies/ruby-2.1.0/lib/ruby/2.1.0/irb.rb:396:in `start'
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands/console.rb:90:in `start'
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands/console.rb:9:in `start'
      from /Users/gagan/.rvm/gems/ruby-2.1.0/gems/railties-4.0.2/lib/rails/commands.rb:62:in `<top (required)>'
      from bin/rails:4:in `require'
      from bin/rails:4:in `<main>'Maybe IRB bug!
```

- _The book has notes about how to add information to Exceptions ... i.e. to make custom exceptions that will store useful information... for example, information about  whether a retry will help or not. Don't think specific notes will be necessary_.

#### `catch` and `throw`

- A note from Avdi Grimm that comprehensively explains what `catch` and `throw` are used for. 

> A common need in programming is a way to terminate execution early when we find there is no further work to be done. Programmers in languages other than ruby either abuse the exception mechanism or use multiple loop breaks and method return to achieve the same effect. Ruby provides the `catch` and `throw` to quickly and cleanly make an early escape. This leaves `begin` / `rescue` / `raise` free to be used for errors and nothing else. -- Avdi Grimm, http://rubylearning.com/blog/2011/07/12/throw-catch-raise-rescue-im-so-confused  <sub> note: I recommend the blog post to see how to use `catch` and `throw` in action </sub>
