1. Integers, Strings, Symbols, Booleans, and Nil. Nil is technically not a data type, depending on who you 
   are talking to, because traditionally data types are raw values that can be of more than one form. i.e. an 
   integer can be 1, or 2, or 3. A boolean can be true, or false. Nil can only be nil, but it is used just like 
   other data types are, so in Ruby I think it's ok to put nil in the data type category.
   
2. Arrays and Hashes. Again, some will say they are also data types, but it's all up to how you want to organize 
   your concept of Ruby mechanics. I like to keep types and structures separate in my head because a type will 
   only be itself, while a structure will hold multiple types.
   Others: Binary Search Tree, Trie, Linked List, Bitmap, Lookup table, HEAP, Graph.

3. Structures, Literal Values, Classes, Structs can all be assigned to variables, so they are all usable values
   once assigned. Basically anything you can assign to a variable is a value. If `x =` works on it, you're good.
   
4. Variables, Methods and Data Structures are the usual suspects here: 
   a. Variables, because you can just use an assignment operator `=` to "hold" that value. <br> 
   b. Methods, because Ruby's implicit return will try to give you the last thing evaluated in the method.
      Sometimes you won't use this mechanic, but you certainly can to have a method call return a value for you. <br>
   c. Structures, because you can just pry them open to get at the value you want.
   d. Classes, by way of their methods, can also just be fancy value holders, though normally they also mutate 
      those values, or produce new values via input and methods.
   e. Structs are dumbed down class-like structures that you can use dot notation on to get at the values
      stored in key/value pairs. Not used often, but good to know about. 
    
5. Absolutely. An array that contains a million elements is still just a value itself, that can be assigned to 
   the variable `really_long_collection`.
   
6. Nothing. And nope. Not that I've found. A class without methods is a fancy safe with no known combination to 
   open it. You can have all the instance variables you want in it, but you won't be able to get to them.
   
7. Methods can return values at any time. So yes, a class with methods only could be used, I just don't know 
   why you'd want to, unless your use case somehow only needed multiple things returned without ever worrying 
   about maintaining state or changing anything. 
   
8. a. A local variable lives as long as it's out wrapper, which is almost always a method. In the console for 
   example, a local variable will hang out for as long as you are in your irb or pry session, because Ruby 
   has a handy class called Main that is the default scope when there are no files, classes, or methods 
   present. Normally, it lives as long as the method using it, then it's gone. <br>
   b. Instance variables are saved in local memory as soon as the method they live in is called (like initialize).
   They will live as long as the class instance is alive, and can be used be one method after another, as many 
   times as you like. That's why they are great at maintaining and changing state inside of a class.
   
9. You can pass it to the other method as an argument. It's technically not extending the variable's life, 
   because the other method fires while the method that passed the argument is still executing, but it's good 
   to know that a local variable can be used by another method just by passing it as an argument.

10. No. No it is not. And the Ruby police frown on this. Instance variables however, can be declared out 
    in the open without being assigned a value. In that case, Ruby default's that instance variable's value 
    to nil. 
  
11. A local variable or a method call. It can't be a method definition because there is no `def` in front of 
    it. It can't be any other kind of variable because they all look different than that (@var, @@var, VAR). 
    To find out if it's a local variable, look for it higher in the method with an assignment operator `=` to
    the right of it. Local variables MUST be assigned before they can be used. That or it will be in the argument 
    list for the method, meaning it was passed in (and assigned when it was passed). If neither of those are
    present, then it absolutely must be a method call, and you can look for the method inside the class (or 
    in a module if you happen to see one included at the top of the class).
    
12. You just call it. By name. Example: <br>
```
     def cool_method
       "this is cool"
     end
     
     def use_cool_method
       cool_method
     end
```
13. Dot notation. If you are outside the class, you must first open your "container"
    (the class where the method you want to use lives). So if you've already done
    `dog = Dog.new` and you know you have a method called name in your Dog class,
    you just say `dog.name`. 

14. A method that doesn't start with `self.`, or that isn't inside of a do 
    block where the class inherits from self, is called an instance method 
    because in order to use it you must instantiate the class it is defined 
    in. Class methods are used without instantiating them first. (most
    commonly, and probably best for clarity, these begin with `self.dot`
    example: `def self.do_something_cool`). To see how else they can be 
    defined [check this out](http://yehudakatz.com/2009/11/15/metaprogramming-in-ruby-its-all-about-the-self/) <br>
    So, to call a class method, you can just do `MyClass.my_method` instead 
    of having to do `MyClass.new.my_method`.
    
    To recap: Instance methods are called on an instance of a class, while 
    class methods are just called directly on the class without instantiation.
    
15. Looking at answer 14 above, we would now say "it depends on whether the 
    class has any class methods defined." A class can have both instance methods 
    and class methods defined inside of it at the same time, but if there are no 
    class methods defined, then the answer to the first part of the  question is yes. 
    The second part of the question can be solved a couple different ways, but for 
    clarity it's a good idea to use `def self.my_method` instead of inheriting, because 
    if you end up with 50 class methods and 50 instance methods it will be hard just looking 
    at the method itself to determine if it's an instance or class method. Putting self. in 
    front of the method name will always tell another dev what kind of method you are 
    defining.
    
16. One, and only one, ever. That value can in turn store multiple values, which can store values, which...etc. But 
    when looking at something that a variable points to: `x = "mystring"`, or `x = Cat.new`, that thing is always only one 
    value. Take, for instance, an array: `arr = [1, 2, 3, 4, 5]`. At first glance it's easy to think that the variable `arr` 
    points to multiple values. But what is really points to is a single data structure. An array. That array contains multiple 
    values, but the array itself is only one value. Same for hashes, structs, and classes.
