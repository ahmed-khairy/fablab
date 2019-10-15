# Become-an-android-developer-from-scratch
## [Welcome video](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1046310#overview)

## [Why android studio](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/2128242#overview)
- `IDE` : integrated development environment
  - it helps your while your coding
  - give you feed backs
  - it is fast because of the auto complete mechanism
  - better to troubleshoot because of debugging feature
  - i can change class name in all of my program easily, don't need to search for each file

## [The best tool to develop your app](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/2128244#overview)
- there are three ways to test your app
  - first your can use emulator : has problems
  - second use a physical device : better but have to test on specific number of device, depending on what you own
  - use genymotion : best way

## [Files, packages, classes and methods](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1009674#overview)
- Java code components
  - File
  - class
  - attribute
  - methods
  - ![java](java-components.png)
  - ![java2](java-components2.png)

## [Syntax symbols](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1009678#overview)
- ![symbols](symbols.png)
- case of the writing : how you write variables or methods or any name
  - `camelCase` : small first word `camel` and capital the second one `Case`
  - `PacalCase` : capital each word

## [Method signature](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1009686#overview)
- there are five components for the java method signature
  1. accessibility keyword, this defines what has access to this method
  2. the return value type, even if there is no return value
  3. method name, so we can call it
  4. syntax symbols like parenthesis or braces
  5. parameters, these are the inputs to the method
  - ![method](method.png)
  - ![method](method2.png)

## [Data types and variables](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1009702#overview)
- attribute is in the beginning of the class
- how to differentiate between class and method
  - the class's name followed by braces {}, it's better to use PascalCase to define it
  - the method's name followed by parenthesis (), it's better to use camelCase to define it
- example of class, a private method and variables
```
// class definition
public class MyInfo
{
  // attributes
  int myAge = 33;
  String myName = "Ahmed";
  boolean isMale = true;
  char middleInitial = 'M';
  float myHeightInMeters = 1.6f;
  // method definition
  private void updateMyInfo ()
  {
    myAge = 35;
    myName = "Ahmed Khairy";
  }
}
```

## [Memory lockers](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1157038#overview)
- memory
- reading, writing
- pointers, that used when one location is not sufficient, so it give it the beginning of the memory that can be used

## [Introduction to computer memory](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1012938#overview)
- if we use pointer it won't be known where is the end of that variable until we put `\n` that's mean the end of that variable, the benefit of pointer that i can use data without copying it
- ![pointer](pointer.png)
- there are two different data types
- ![data](data-types.png)
- it is better to reduce the usable memory as possible
- ![variable](variables.png)

## [Reference and null](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1012942#overview)
- references are pointers
- to define a reference you use : `int[] new = new int [4];`
  - this code means that this is an int array called new and it reserves 4 places in memory each place is int data type
- to assign value to each place : `new [0]= 2;`, and so one to `new [3]`
- if i want to make reference but not giving it a memory we use : `int [] new;`, this declaration make the reference equal `null`
- so for example if i create another reference : `int[] new2;` it's value will be `null`
- i can make the new reference points to the value of the first reference by writing : `new2 = new;`, but if i assign a `null` to `new` reference, the `new2` still point to the same data

## [Android studio](https://www.udemy.com/course/become-an-android-developer-from-scratch/learn/lecture/1012948#overview)
- installing android studio
- sdk manager installing
- 
