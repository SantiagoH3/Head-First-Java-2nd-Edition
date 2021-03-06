# Head First Java
Notes and exercises related to the book Head First Java, 2nd Edition.

## Exercise Solutions
Discussions and links to code for various exercises from the book.  
### Chapter 1 - A Quick Dip
#### Page 9 - Writing a class with main  
Typing, compiling and running of a program called [MyFirstApp](/workspace/Ch01 My First App/src/MyFirstApp.java). The output of this program will be:  
```
I Rule!
The World!
```
#### Page 12 - Example of a while loop  
Typing, compiling and running of a program called [Loopy](/workspace/Ch01 Loopy/src/Loopy.java). The output of this program will be:  
```
Before the Loop
In the Loop
Value of x is 1
In the Loop
Value of x is 2
In the Loop
Value of x is 3
This is after the loop
```

### Chapter 2 - Classes and Objects  

#### Page 42 - Be the Compiler
The code about tape decks will not compile because an object, called t, is used without being created. A fixed version of the code can be found [here](/workspace/Ch02 Tape Deck/src/TapeDeckTestDrive.java). The output of this program will be:  
```
tape playing
tape recording
```

The code about DVD players will not compile because an method is called that isn't defined in the class DVDPlayer. A fixed version of the code can be found [here](/workspace/Ch02 DVD Player/src/DVDPlayerTestDrive.java). The output of this program will be:  
```
DVD playing
DVD recording
```

### Chapter 3 - Primitives and References

#### Page 63 - Be the Compiler  
The code with the Books class will not run as intended. It will cause a null-pointer exception at run time. The problem is that an array that can hold references to Books objects is created, but no actual Books objects are then created to be put in the array.  

A fixed version of the code can bee found [here](/workspace/Ch03 Books/src/BooksTestDrive.java). The output when running the code will be:  
```
The Grapes of Java by bob
The Java Gatsby by sue
The Java Cookbook by ian
``` 

The code with the Hobbits class will not run as intended. It will cause a array out of bounds exception at run time. The allowed array indexes to use will in this case be 0 to 2 but the original code will try to place a hobbit at index 3 that does not exist. Array indexes start at 0 and is it a common mistake to forget this.  

A fixed version of the code can bee found [here](/workspace/Ch03 Hobbits/src/Hobbits.java). The output when running the code will be:  
```
bilbo is a good Hobbit name
frodo is a good Hobbit name
sam is a good Hobbit name
```

### Chapter 4 - Methods use Instance Variables

#### Page 87 - Sharpen your pencil  
Assume the method definition given below.  
```
int calcArea(int height, int width) {
	return height * width;
}
```
Example of legal statements that use the method are then the following.  
```
int a = calcArea(7, 12);  // OK, the literals 7 and 12 will be interpreted as int values
```
```
short c = 7;
calcArea(c, 12);  // OK because a short will always fit in an int  
```
```
calcArea(2, 3);  // It is OK to not use the return value for anything
```
Statements that would be illegal are for example the following.  
```
int d = calcArea(57);  // One of the arguments are missing 
```
```
long t = 42;
int a = calcArea(t, 12);  // Must cast the long to an int since t may be to big to fit in the int
```
```
int g = calcArea();	 // Both arguments are missing
```
```
calcArea();  // Both arguments are missing
```
```
byte h = calcArea(4, 20);  // The result may not fit in an byte variable since it is of type int
```
```
int j = calcArea(2, 3, 5);  // There is one argument too many
```

#### Page 88 - Be the Compiler
The [code](/workspace/Ch04 X Copy/src/XCopy.java) with the class called XCopy will compile.  

The value that is changed inside the method go is just a copy of the value called orig. This means that orig will remain unchanged and will hold 42, y will be set to twice the value of orig.

The output when running the code will be:  
```
42 84  
```

The original code with the class called Clock will not compile. The problem is that the getter function does not return anything according to the declaration. This function should be declared to return a String.  

A fixed version of the code can be found [here](/workspace/Ch04 Clock/src/ClockTestDrive.java).  

The output when running the code will be:  
```
time: 1245  
```
### Chapter 5 - Writing a Program  

#### Page 118 - Be the JVM  
The code in this exercise will update the variables x and y in the following seguence.

y is set to 7 and x is undefined before entering the for loop.  

y is increased to 8 and x is 1 in the first round of the for loop.  

y is increased to 9 and x is 2 in the second round of the for loop.

y is increased to 10 and x is 3 it the third round of the for loop.

y is increasde to 11 and x is 4 in the fourth round of the for loop.

y is first increased to 12 and x is 5 in the fifth round of the for loop. x now being larger than 4 causes y to be increased to 13 and then so is this number printed.  

y is first increased to 14 and x is 6 in the sixth round of the for loop. x being larger than 4 causes y to be increased to 15 and then so is this number printed. y now being larger than 14 causes "x = " and the value of x to be printed. The following break statement  will then end the execution of the for loop out of the for loop.  

To conclude so will the program when run print out:  
```
13 15 x = 6
```

### Chapter 9 - Object Construction  

#### Page 252 - Sharpen your pencil  
Example code that illustrates constructor chaining. We have a class Hippo that inherits from another class called Animal. When a new Hippo is created so will the Animal constructor be run before the Hippo constructor. This can be verified by running the this [test program](/workspace/Ch09 Test Hippo/src/TestHippo.java) that uses the classes [Hippo](/workspace/Ch09 Test Hippo/src/Hippo.java) and [Animal](/workspace/Ch09 Test Hippo/src/Animal.java).  

#### Page 266 - Be the Garbage collector
Assume the following code:
```Java  
public class GC {
	public static GC doStuff() {
		GC newGC = new GC();
		doStuff2(newGC);
		return newGC;
	}
	
	public static void main(String[] args) {
		GC gc1;
		GC gc2 = new GC();
		GC gc3 = new GC();
		GC gc4 = gc3;
		gc1 = doStuff();
		
		// (A)
		
		// call more methods

	}

	public static void doStuff2(GC copyGC) {
		GC localGC = copyGC;
	}
}

```  

Now assume that we have the following list of statements that are suggested to be inserted at (A) in the code above. The question is which can be inserted without compilation errors and then also which statements would cause exactly one extra object to be up for garbage collection?  

```
copyGC = null;
```
Will not compile because `copyGC` is out of scope when attempted to be used.  
```
gc2 = null;
```
Will compile and will cause `gc2` to be up for garbage collection.  
```
newGC = gc3;
```
Will not compile because `newGC` is out of scope when attempted to be used.  
```
gc1 = null
```
Will compile and will cause the `GC` instance that `gc1` used to refer to be up for garbage collection.  
```
newGC = null;  
```
Will not compile because `newGC` is out of scope when attempted to be used.  
```
gc4 = null;
```
Will compile but will not cause anything new to be up for garbage collection since `gc3` still refers to the same instance.  
```
gc3 = gc2;
```
Will compile but will not cause anything new to be up for garbage collection since `gc4` still refers instance that `gc3` used to refer to.
```
gc1 = gc4;
```  
Will compile and will cause the `GC` instance that `gc1` used to refer to be up for garbage collection. 
``` 
gc3 = null;
```
Will compile but will not cause anything new to be up for garbage collection since `gc4` still refers instance that `gc3` used to refer to.  
