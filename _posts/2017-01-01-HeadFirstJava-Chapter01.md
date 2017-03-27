---
layout: post
title: Head First Java - Chapter One
bigimg: /img/path.jpg
published: true
---

I will be doing a recap on the popular Head First Java book, giving an overview of everything I learned on a chapter to chapter basis, this can be used as an extra resource for anyone studying the book or be me to look over some notes.  **Chapter One**

-Firstly we create a source file, this is typically a .java file
-This source file goes through the compiler, any compiler issues will have to be resolved, e.g code that cannot be compiled e.g:

     e.g int number = "five";
     
- The outputted code from the compiler is bytecode and this is a .class file
- We can run our program by starting the java virtual machine with this class file, the JVM translates the bytecode and runs the program.

      int size = 27;  (Declare an integer called size, and *assign* it the value 27

      String name = "Fido"; (Declare a String called name, *assign* it the value Fido

      Dog myDog = new Dog(name, size);  (Create an object reference called myDog, Create and assign this      	reference to the new dog object

      x = size -5; (*assign* x the value of size minus 5)

      if (x < 15) myDog.bark(8); (if x is less than 15, call the bark method of myDog (Dog Object), passing in 	 the value of 8 as an argument

      while (x > 3) { myDog.play(); }   (while x is more than 3, call the play() method of myDog (Dog Object).

      int[] numList = {2,4,6,8}; (Create an array of integers called numList, assign the values 2,4,6,8.     		Remember arrays are 0 indexed. so point 1, is actually 0. 0 = 2, 1 = 4, 2 = 6, 3 = 8.

      System.out.println("Hello"); (Print out to the console "Hello")

      System.out.println("Dog");  (Print **on a new line** "Dog")

      String num = "8";
      int z = Integer.parseInt(num); (create an int called z, assign it the value 8.  "8" is a string (num) 		so 	 we must cast it to an integer hence the Integer.parseInt(num), calling parseInt() passing in our String     allowing us to the get the value but as an int.

      try {
          readTheFile("myFile.txt");
      } catch (FileNotFoundException ex) {
          System.out.printl("File Not Found");
      }                                            (*try* to do something, in this instance call the 		 													 readTheFile() method passing in the myFile.text String as 												     an argument.  Catch a FileNotFoundException and print 													     out "File Not Found".  A File not found exception would be   	                                             thrown if the file myFile.txt could not be found
    
Java initially started on version 1.02, current version is Java 1.8 (Java 8) However this book will be teaching us as of Java 5

We put a Class in a source file (.java)
We put Methods inside a class e.g -> calculateSomething();
We put Statements inside a method e.g -> System.out.println("Hello"); -> int a = b * c;
    

    Public Keyword -> Public so everyone  can access it
    Class Keyword -> This is a class
    Class Name -> Public class Dog
    Static -> Class does not need to be instantiated (created) to call the methods
    Void -> Method does not return something
    main -> Name of the method, this could be anything
    String[] args -> Method arguments, expects an array of Strings and they will be called args
    System.out.print -> Print out to the console
    
Doing something with java -> Statements, Declarations, Assignments, Method calls etc can all be ways we can *do* something.

    int x = 3;
    String name = Simon;
    x = x + 5;
    System.out.print("x is " + x);
    double d = Math.random();
    //this is a comment
    
Do something *over and over* -> For and While loops (note: there is also an enhanced for loop later)

    while (x > ) {
    // Do stuff in here
    }
    
    for (int x = 0; x < 10; x = x + 1) {
     //Do stuff in here
     }
     
 Each statement *must* end in a semicolon -> int a = 5;
 A single-line comment begins with two forward slashes -> //
 Most whitespaces doesn't really matter -> x      =      3;
 Variables are declared with a *name* and *type* -> int(Type) weight(Name); = int weight;
 Classes and methods must be definied within a pair of curly braces -> public void go() { //code goes here }
 
Java has three main types of loop -> while loop, for loop and do-while.  Each loop has a conditional test and if the conditional test is **true** the code inside the loop will execute, if it is false it will skip the code and carry on outside the loops curly braces {}.  Simple tests we can use as a conditional test are **<** (lesser than) **>** (greater than) **==** (equality, yes two equals signs).

in Java one = is to *assign* something -> int age = 26;
In Java two == is to check *equality* of something -> if (age == 26) {}

    int age = 25;
    while (age > 10) {
      age --;
    }
    
The above example is a while loop that will do something when age is less than 10, in this case it is less than 10 (its 25);  Each time in the loop we will be deducting 1 from age (age++;), without this our code/loop would run forever, we need a way out.  So in this example age will be deducted once per iteration of the loop, eventually it will stop.

In Java an *if* test is basically the same as the boolean test in a while loop, except instead of saying *while* something is true do this, we say if something is true do this.

    int age = 22;
    if (age == 25) {
      //Do something 
     }
     
In the above example, nothing would happen because age **isn't** 25, its 22. in order for the code to run inside our if statement it must be true, e.g below:

	int age = 25;
    if (age == 25) {
      System.out.println("The age is: " + age);
    }
    
Printing out "The age is: 25".  We can build an else onto our if statements, see below:

	if (age == 25) {
       //Do Something
	} else {
    	//Do something else
     }
     
System.out.print -> Print on the same line
System.out.println -> Print on a new line

Declare a new array of Strings -> String[] wordList = {"Simon", "George", "John", "Lee"}
Find the length of an array (the size) -> int size = wordList.length; (Length is an instance variable, not a method so we don't need wordList.length();  int size is now equal to 4 (4 Strings in our String[] array.
Generate a random number -> int ranom = (int) (Math.random() * wordList.length); (Because the Math.random() method returns a **double** between 0 - 0.99 we need to cast it (transform/change it) to an int because its likely to return a value like 0.24 and an int cannot take this, its a double  value, int is 0 or 1 etc.
