#### Refactoring from Good to Greate - Ben Orenstein

* When you have a temp variable getting assigned in most cases it is a good idea to make a private method by the name of the temp variable. The reaons being: 
  - You don't read the implementation that goes into assigning the temp variable. When reading the code, it is abstracted out for you now and you trust the implementation. 
  - You can reuse the temp variable
  - Shorter methods are more likely to do one thing


* When you have two attributes that are connected with each other, they are called  dataclump and they should be moved to a different class and be made together

* Range#include actually goes an instantiates all objects and checks to see if the value passed to it is one of all the values. Range#cover? actually only instantiatest the extreme values and does math to check if the values are covered in the range. It is faster!

* The fewer the number of parameters a method takes the superior it is. That is because parameters introduce something known as paramater coupling which increases cupling of the code.
