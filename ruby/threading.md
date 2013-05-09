### Threading

- Everytime you execute `ruby`, `rails` or `irb` you are creating a process. 
- Within each process you have something which is executing the code in your process. This is called a `thread`
- The operating system starts every process with a "main" thread.
- Ruby allows you to create as many new threads as you want by calling Thread.new with a block of code to be executed. Once the block of code has finished executing, the thread is considered dead. If the main thread exits, the process dies. 
- Generally your computer can execute one thread per core. i.e. if a computer has two cores, it can execute two threads at the exact same time (this is true JRuby, but not in Matz Ruby Interpreter. That may be why Ruby is not considered to be truly concurrent). 
- I think that code is considered to be thread safe if it does not cause race conditions. 

- Ruby 1.9 onwards, threading is performed by the operating system. Although threads can now take advantage of multiple processors (and multiple cores in a single processor), since many ruby extension libraries are written for the older threading model of ruby, tehy aren't thread-safe. Ruby will never run two threads in the same application truly concurrently - however, you will see threads busy doing I/O while other thread executes ruby code.


Questions: 

- If I run `irb` and run some code which returns the value, at that point is the "main" thread dead? 
- What is native operating system threads? 


Sources: 

- [http://blog.carbonfive.com/2011/10/11/a-modern-guide-to-threads/]
- The picaxe book

