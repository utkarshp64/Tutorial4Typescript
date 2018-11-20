# Tutorial4Typescript

* [Variable Declaration](#variable-declaration)
* [Basic Datatypes](#basic-datatypes)
  * [Type assertions](#type-assertions)
  * [Variable Scope in typeScript](#variable-scope-in-typescript)
* [Operator In Typescript](#operator-in-typescript)
* [Conditional Statement and Loops](#conditional-statement-and-loops)
* [Functions in Typescript](#functions-in-typescript)
  * [Function Parameters](#function-parameters)
* [Classes](#classes)
  * [Inheritance](#inheritance)
  * [Abstract Class](#abstract-class)
  * [Access Modifiers](#access-modifiers)
  * [Accessors](#accessors)
* [Interfaces](#interfaces)
* [Generics](#generics)
* [Modules](#modules)
* [Namespaces](#namespaces)
* [Javascript Objects Basics](#javascript-objects-basics)

---
 ## Variable Declaration

* In typescript variable are decleared using `let` and `const` keyword.
* `const` is an augmentation of `let` in that it prevents re-assignment to a variable.
* **`const` declarations must be initialized**
* When a variable is declared using `let`, it uses what some call block-scoping.
* `var` declarations are accessible anywhere within their containing function, module, namespace, or global scope

```typescript
let x = 10;
let x = 20;// error: can't re-declare 'x' in the same scope
const pi = 3.14;
```

## Basic Datatypes
> syntax
```typescript
let <variableName>: <dataType> = value;
//<dataType> :  boolean | number | string | null | undefined | any | void
```

##### Examples:
1. Boolean
```typescript
let isDone: boolean = false;
```
2. Number
```typescript
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```
3. String
```typescript
let color: string = "blue";
let fullName: string = 'Bob Bobbington';
let sentence: string = `Hello, my name is ${ fullName }.
                        I'll be ${ age + 1 } years old next month.`
```
4. Null & Undefined
```typescript 
let u: undefined = undefined;//(Something hasn't been initialized : undefined.)
let n: null = null;//(Something is currently unavailable: null.)
```
> By default `null` and `undefined` are subtypes of all other types. That means you can assign null and undefined to something like `number`
5. Any
```typescript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false;
```
> The any type is a powerful way to work with existing JavaScript, allowing you to gradually opt-in and opt-out of type-checking during compilation.
6. Void
    Declaring variables of type void is not useful because you can only assign `undefined` or `null` to them:
```typescript
let unusable: void = undefined;
```
```typescript
function warnUser(): void {
    alert("This is my warning message");
}
```
7. Never
> The `never` type represents the type of values that never occur. For instance, `never` is the return type for a function expression or an arrow function expression that always throws an exception or one that never returns; Variables also acquire the type never when narrowed by any type guards that can never be true.
8. Union
    Union types are used to declare a variable that is able to store a value of two or more
    types.
```typescript
let path : string[]|string|boolean;
path = '/temp/log.xml';
path = ['/temp/log.xml', '/temp/errors.xml'];
path = 1; // Error
path = true
```

---

* Array
	* TypeScript, allows you to work with arrays of values, like JavaScript. Array types can be written in one of two ways. In the first, you use the type of the elements followed by `[]` to denote an array of that element type
##### Example:
```typescript
//type 1
let list: number[] = [1, 2, 3];

//type 2
let list: Array<number> = [1, 2, 3];
```
```typescript
let num: number[][] = [[1,2,3],[1,2,3],[0,0,0]];
console.log(num)
//[Array[3], Array[3], Array[3]]
 //0: Array[3]
    //0: 1
    //1: 2
    //2: 3
 //1: Array[3]
    //0: 1
    //1: 2
    //2: 3
 //2: Array[3]
    //0: 0
    //1: 0
    //2: 0
```
* Tuples
    * Tuple types allow you to express an array where the type of a fixed number of elements is known, but need not be the same.
    * The Tuple type represents a JavaScript array where you can define the datatype of each element in array.

##### Example:
```typescript
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```
```typescript
let tupleArray: [string, number, number];

tupleArray = ['add', 2, 3]; // GOOD!

tupleArray = ['multiply', 3, 4]; // GOOD!

tupleArray = [2, 3, 'multiply']; // ERROR!

tupleArray = ['add', 2]; // ERROR!

tupleArray = ['add', 2, 3, 4, 5, 6, 'add', 'divide', 'subtract', 6, 'Hello'] // GOOD?

// Mixed tuple
let tupleMix: [string, number, number,boolean];

tupleMix = ['add', 2,3,true,false,2,'string',false];//Good
```
* Enums
    * An enum is a way to organize a collection of related values.
    * TypeScript enums are number based
    * The `enum` keyword is used to define Enum type in TypeScript.
    * By default, the value of enum’s members start from 0.

##### Example:
```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
console.log(c) // 1
```
```typescript
enum Color {Red=2, Green=4, Blue}
let c: Color = Color.Green;
console.log(c) // 4
```
```typescript
enum Tristate { False, True, Unknown }
console.log(Tristate[0]); // "False"
console.log(Tristate["False"]); // 0
console.log(Tristate)//{0: "False", 1: "True", 2: "Unknown"}
console.log(Tristate['Unknown'])//2
```

##### Example: Advanced `enum`
```typescript
// Example of enum with string-valued members
enum StringEnum {
    JSON = "application/json",
    XML = "application/xml"
}
console.log(StringEnum);
console.log(StringEnum['JSON']);
 let num = StringEnum.JSON
 console.log(num)

//Example of enum with number-valued members
 enum DefaultPorts {
    HTTP = 80,
    HTTPS = 443
}
console.log(DefaultPorts);//{80: "HTTP", 443: "HTTPS", HTTP: 80, HTTPS: 443}
console.log(DefaultPorts[80]) //HTTP
console.log(DefaultPorts['HTTPS'])//443
```
### Type assertions
Type assertions is type casting in Typescript.Type assertions have two forms:
1. “angle-bracket” syntax:
```typescript
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

2. as-syntax:
```typescript
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length
```

### Variable Scope in typeScript
* Global Scope − Global variables are declared outside the programming constructs. These variables can be accessed from anywhere within your code.

* Class Scope − These variables are also called fields. Fields or class variables are declared within the class but outside the methods. These variables can be accessed using the object of the class. Fields can also be static. Static fields can be accessed using the class name.

* Local Scope − Local variables, as the name suggests, are declared within the constructs like methods, loops etc. Local variables are accessible only within the construct where they are declared.

##### Example:
```typescript
let global_num = 12          //global variable 
class Numbers { 
   num_val = 13;             //class variable 
   static stat_val = 10;         //static field 
   
   storeNum():void { 
      let local_num = 14;    //local variable 
   } 
} 
console.log("Global num: "+global_num)  
console.log(Numbers.stat_val)   //static variable  
let obj = new Numbers(); 
console.log("Class num: "+obj.num_val) 
```
## Operator In Typescript
* Arithmetic operators
  `[+, -, /, *, %, ++, --]`
* Relational operators
  `[<, >, <=, >=, ==, !=]`
* Logical operators
  `[&& (AND), || (OR), ! (NOT)]`
* Bitwise operators
  `[& (Bitwise AND), | (BitWise OR), ^ (Bitwise XOR), ~ (Bitwise Not), << (Left Shift), >> (Right Shift), >>> (Right shift with Zero)]`
* Assignment operators
  `[+=, -=, *=, /=, %=]`
* Ternary/conditional operator
  `[condition ? statement1 : statement2]`
* Type Operator
  `[typeof, instanceof]`

## Conditional Statement and Loops
* **If-else and nested if statement** 
> syntax
```typescript
if (condition) {
  code to run if condition is true
} else if {
  run some other code instead
} else {
  run some other code instead
}
```
##### Example:
```typescript
let num:number = 2 
if(num > 0) { 
   console.log(num+" is positive") 
} else if(num < 0) { 
   console.log(num+" is negative") 
} else { 
   console.log(num+" is neither positive nor negative") 
}
```
* **Switch statement**
> syntax
```typescript
switch (expression) {
  case choice1: run this code
                break;
  case choice2: run this code instead
                break;
                
  // include as many cases as you like
  
  default: actually, just run this code
}
```
##### Example:
```typescript
let grade:string = "A"; 
switch(grade) { 
   case "A": { 
      console.log("Excellent"); 
      break; 
   } 
   case "B": { 
      console.log("Good"); 
      break; 
   } 
   default: { 
      console.log("Invalid choice"); 
      break;              
   } 
}
```
* **While statement**
> syntax
```typescript
initializer
while (exit-condition) {
  // code to run

  final-expression
}
```
##### Example:
```typescript
let n: number = 5
while (n != 0) {
    console.log("Entered while");
    n--;
}
```
* **Do-while statement**
> syntax
```typescript
initializer
do {
  // code to run

  final-expression
} while (exit-condition)

```
##### Example:
```typescript
let n: number = 5
while (n != 0) {
    console.log("Entered while");
    n--;
}
n = 5
do {
    console.log("Entered do…while");
} while (n > 5);
```
* **For statement**
> syntax
```typescript
for (initializer; exit-condition; final-expression) {
  // code to run
}
```

##### Example:
```typescript
let num:number = 5; 
let factorial = 1; 

for(let i: number = num;i>=1;i--) {
   factorial *= i;
}
console.log(factorial)
```
* **For-in statement**
> syntax
```typescript
for (let val in list) { 
   //statements 
}
```

##### Example:
```typescript
let someArray = [9, 2, 5];
for (let item in someArray) {
  console.log(item); // 0,1,2
  //console.log(someArray[item]); // 9,2,5
}
```

* **For-of statement**
>synatx
```typescript
for (let val of list) { 
   //statements 
}
```

##### Example:
```typescript
//using for-of
let someArray = [9, 2, 5];
for (let item of someArray) {
  console.log(item); // 9,2,5
}
```
##### Example:
```typescript
let i:any; 
let alphabetList:any = "a b c d e f g h"  
//using for-of
for(i of alphabetList) {
   console.log(i); // a _ b _ c _ d _ e _ f _ g _ h
}
//using for-in
for(i in alphabetList) {
   console.log(i); // 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
}

//using for-in & passing i as index 
for(i in alphabetList) {
   console.log(alphabetList[i]); // a _ b _ c _ d _ e _ f _ g _ h
}

//using for-of & passing i as index 
for(i of alphabetList) {
   console.log(alphabetList[i]); // undefined*15
}
```
* **`break` & `continue` Statement**
> The `break` statement is used to take the control out of a block. Using `break` in a loop causes the program to exit the loop.

> The `continue` statement skips the subsequent statements in the current iteration and takes the control back to the beginning of the loop. Unlike the `break` statement, the `continue` doesn’t exit the loop. It terminates the current iteration and starts the subsequent iteration.

> syntax
```typescript
break;
continue;
```

## Functions in Typescript
**1. Named function(Function Declaration)**
> syntax
```typescript
function  function_name() { 
   // function body 
}
```

##### Example:
```typescript
function add(x: number,y: number) {
    return x + y;
}
```
**2. Anonymous function(Function Expression)**
> syntax
```typescript
let val = function( [arguments] ) { ... }
```

##### Example:
```typescript
let myAdd = function(x:number, y:number): number { return x + y; };
```
##### Example: `greetNamed` is a function declaration while `greetUnnamed` is a function expression
```typescript
console.log(greetNamed("John"));
console.log(greetUnnamed("John"));
function greetNamed(name : string) : string {
 if(name) {
 return "Hi! " + name;
 }
}
let greetUnnamed = function(name : string) : string {
 if(name){
 return "Hi! " + name;
 }
}
```

**3. Arrow function / Fat arrow(=>) function**
> syntax
```typescript
let val = ( [arguments] ) => { ... }
```

##### Example:
```typescript
let add = ( a, b) => a + b;
console.log(add(2,3));//5
```

##### Example: function Multiple return values and multiline Arrow function 
```typescript
let deck = {
  suits: ["hearts", "spades", "clubs", "diamonds"],
  cards: Array(52),
  createCardPicker: function () {
  // NOTE: the line below is now an arrow function, 
  // allowing us to capture 'this' right here
    return () => {
      let pickedCard = Math.floor(Math.random() * 52);
      let pickedSuit = Math.floor(pickedCard / 13);

      return { suit: this.suits[pickedSuit], card: pickedCard % 13 };
    }
  }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();

console.log("card: " + pickedCard.card + " of " + pickedCard.suit);
```

### Function Parameters
* **Optional Parameters**

##### Example:
```typescript
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return console.log(firstName + " " + lastName);
    else
        return console.log(firstName);
}
let result1 = buildName("David");               // works correctly now
let result2 = buildName("David", "Webb", "Sr.");// error,too many parameters
let result3 = buildName("David", "Webb");       // ah, just right
```
* **Default Parameters**
##### Example:
```typescript
function calculate_discount(price:number,rate:number = 0.50) { 
   let discount = price * rate; 
   console.log("Discount Amount: ",discount); 
} 
calculate_discount(1000)      //500
calculate_discount(1000,0.30) //300

```
* **Rest Parameters**
##### Example:
```typescript
function buildName(firstName: string, ...restOfName: string[]) {
    return console.log(firstName + " " + restOfName.join(" "));
}
let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```
```typescript
function buildName(firstName: string, ...restOfName: any[]) {
  return console.log(firstName + " " + restOfName.join(" ")); //Joseph Samuel,Lucas MacKinzie,David
  //return console.log(firstName + " " + restOfName[0]); //Joseph Samuel,Lucas
  //return console.log(firstName + " " + restOfName[0][1]);   //Joseph Lucas
  //return console.log(firstName + " " + restOfName[1][1]); //Joseph David

  //return console.log(firstName + " " + restOfName[0][2][1]); //Joseph David
}
let employeeName = buildName("Joseph", ["Samuel", "Lucas"], ["MacKinzie", "David"]);
//let employeeName = buildName("Joseph", ["Samuel", "Lucas",["MacKinzie", "David"]]);
```
##### Example:
```typescript
function add(...foo : number[]) : number {
 let result = 0;
 for(let i = 0; i < foo.length; i++){
 result += foo[i];
 }
 return result;
}
add();      // returns 0
add(2);     // returns 2
add(2,2);   // returns 4
add(2,2,2); // returns 6
```
## Classes
A class is composed of a fields, Constructors, and methods / functions.
> syntax
```typescript
class class_name { 
   //field
   //constructor
   //function
}
```
##### Example:
```typescript
class Greeter {
    //fields
    greeting: string;
    
    //constructor
    constructor(message: string) {
        this.greeting = message;
    }
    
    //function
    greet() {
        return "Hello, " + this.greeting;
    }
}
// Creating Instance objects
let greeter = new Greeter("world");

//accessing function using (" . ") operator
console.log(greeter.greet()) // Hello, world
```
> A constructor is a special method used by the new keyword to create instances(also known as objects) of our class.
```typescript=
 
 // Normal Constructor Defining
class Person {
  name: string;
  surname: string;
  public email: string;
  constructor(name: string, surname: string, email: string) {
    this.email = email;
    this.name = name;
    this.surname = surname;
  }
  greet() {
    alert("Hi!");
  }
}
let person = new Person('David','Webb');
console.log(person.name);
person.greet();
```
```typescript
// shortcut syntax
class Person {
  constructor(public name: string, public surname: string, public email?: string) { }
  greet() {
    alert("Hi!");
  }
}

let person = new Person('David','Webb');
console.log(person.name);
person.greet();
```

### Inheritance
* Inheritance is an important pillar of OOP(Object Oriented Programming).
* Inheritance allows us to create a new class (child class) that inherits all the properties and methods from an existing class (parent class). Child classes can include additional properties and methods not available in the parent class.
* It is the mechanism in Typescript by which one class is allow to inherit the features(fields and methods) of another class using `extends` keyword

##### Example:
```typescript
class Animal {
    move(distanceInMeters: number = 0) {
        console.log(`Animal moved ${distanceInMeters}m.`);
    }
}

class Dog extends Animal {
    bark() {
        console.log('Woof! Woof!');
    }
}

//multi-level inheritance here Cat indirectly inherit from Animal
//TypeScript doesn’t support multiple inheritance.
class Cat extends Dog {
    meow() {
        console.log('meow! meow!');
    }
} 
const dog = new Dog();
dog.bark();
dog.move(10);
dog.bark();
const cat = new Cat();
cat.move(20);
cat.meow();
```
### Abstract Class
An Abstract class is a special type of class which cannot be instantiated and acts as a base class for other classes. Abstract class members marked as abstract must be implemented by derived classes.
```typescript
abstract class Shapes {
  abstract Area(): number;
}
class Square extends Shapes {
  constructor(public side: number = 0) {
    super();
  }
  // implemented Area method
  Area(): number {
    return this.side * this.side;
  }
}
class Rectangle extends Shapes {
  constructor(public length: number = 0, public width: number = 0) {
    super();
  }
  // implemented Area method
  Area(): number {
    return this.length * this.width;
  }
}
let s = new Square(4);
console.log(s.Area()); //16

let r = new Rectangle(4, 3);
console.log(r.Area()); //12
```
##### Example: Abstraction, Inheritance, Method overriding
```typescript
abstract class Animal {
  abstract move();
  eat() {
    console.log('IN ANIMAL: Eat method from Animal Class');
  }
}


class Bird extends Animal{
  // Non-abstract class 'Bird' does not implement inherited abstract 
  // member 'move' from class 'Animal'
}


class Dog extends Animal {
  move() {
    console.log('IN DOG: Abstract method move() from Animal class edited in Dog class');
  }
}

class Cat extends Dog {
  speak() {
    console.log('IN CAT: meow! meow!');
  }

  eat() {
    super.eat();
    console.log('IN CAT: Eat() method from Animal Class overriding in Cat Class ');
  }
}

let dog = new Dog();
dog.eat();
dog.move();

let cat = new Cat();
cat.eat();
cat.speak();
cat.move();

//IN ANIMAL: Eat method from Animal Class
//IN DOG: Abstract method move() from Animal class edited in Dog class
//IN ANIMAL: Eat method from Animal Class
//IN CAT: Eat() method from Animal Class overriding in Cat Class
//IN CAT: meow! meow!
//IN DOG: Abstract method move() from Animal class edited in Dog class
```
### Access modifiers
* `public`
  A public data member has universal accessibility. Data members in a class are public by default
* `private`
  Private data members are accessible only within the class that defines these members
* `protected`
  A protected data member is accessible by the members within the same class as well as child class

| accessible on   | `public` | `protected` | `private` |
| --------------- | -------- | ----------- | --------- |
| class           | yes      | yes         | yes       |
| class children  | yes      | yes         | no        |
| class instances | yes      | no          | no        |

* **`readonly`**
    * TypeScript supports readonly modifiers on property level by using the `readonly` keyword. The Readonly properties must be initialized at their declaration or in the constructor.
    * The **readonly modifier** is part of TypeScript's type system. **It's only used by the compiler to check for illegal property assignments.** Once the TypeScript code has been compiled to JavaScript, all notions of readonly are gone.
##### Example:
```typescript
class Person {
  //fields or property with access modifiers
  public firstName: string;
  lastName: string;// by default taken as public
  protected DOB: string;
  private salary: number;
  
  // readonly initialized at declaration or in constructor
  readonly country: string = "India";
  readonly name: string;
  constructor(name: string) {
    this.name = name;//readonly initialized in constructor
  }
  
  // methods with access modifiers
  public move() { };// move(){};
  protected run() { };
  private stop() { };
}
```
### Accessors
TypeScript supports **getters/setters** as a way of intercepting accesses to a member of an object.
##### Example:
```typescript
class Employee {
  private _fullName: string; // naming convention for private variable
// getter method
  get fullName(): string {
    return this._fullName;
  }
// setter method 
  set fullName(newName: string) {
    this._fullName = newName;
  }
}
let employee = new Employee();
employee.fullName = "Bob Smith";
console.log(employee.fullName);
```
## Interfaces
* Interfaces define properties, methods, and events, which are the members of the interface. Interfaces contain only the declaration of the members.
* Interfaces are particularly useful for validating the required structure of properties, objects passed as parameters, and objects returned from functions.
> syntax
```typescript
interface finterface_name{
    //fields or properties
    //methods (only declaration part)
}
```
##### Example:
```typescript
interface Person { 
   firstName:string, 
   lastName:string,
   middleName?:string,
   sayHi: ()=>string 
}
let customer:Person = { 
   firstName:"Tom",
   lastName:"Hanks", 
   sayHi: ():string =>{return "Hi there"} 
} 
console.log("Customer Object ") 
console.log(customer.firstName) 
console.log(customer.lastName) 
console.log(customer.sayHi())  

let employee:Person = { 
   firstName:"John",
   lastName:"Reese", 
   sayHi: ():string =>{return "Hello!!!"} 
} 
console.log("Employee  Object ") 
console.log(employee.firstName) console.log(employee.lastName)
```

##### Example: An interface can extend multiple interfaces, creating a combination of all of the interfaces.
```typescript
interface Shape {
  color: string;
}

interface PenStroke {
  penWidth: number;
}

interface Square extends Shape, PenStroke {
  sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```

##### Example: A class can use Interfaces using keyword `implements`
```typescript
interface IStore {
  Read(): void;
  Write(): void;
  paint(): void;//comment paint() to remove error
}
interface ICompress {
  Compress(): void;
  Decompress(): void;
}
// Error Message:
// Class 'DocStore' incorrectly implements interface 'IStore'.
// Property 'paint' is missing in type 'DocStore'.

class DocStore implements IStore, ICompress {
  Read(): void {
    console.log("Read Method for IStore");
  }
  Write(): void {
    console.log("Write Method for IStore");
  }
  Compress(): void {
    console.log("Compress Method for ICompress");
  }
  Decompress(): void {
    console.log("Decompress Method for ICompress");
  }
}

let I1: IStore = new DocStore();
//can access only IStore members
I1.Read();
I1.Write();

let I2: ICompress = new DocStore();
//can access only ICompress members
I2.Compress();
I2.Decompress();

let I3 = new DocStore();
//can acccess both members
I3.Read();
I3.Write();
I3.Compress();
I3.Decompress();
```
> **Interfaces are not to be converted to JavaScript.**

## Generics
* `generics` is a reusable code(class,function,interface)
* creating reusable a component that can work over a variety of types rather than a single one.
* In generics, a type parameter is supplied between the open (<) and close (>) brackets
##### Example:
* Part 1
```typescript
//In Queue class we want to add only say number type but above code
//will accept string also. so we will modify code for number in part 2
class Queue {
  private _data = [];
  push = (item) => this._data.push(item); //Arrow function
  // push = function (items) {
  //   return this._data.push(items)
  // }

  pop = () => this._data.shift();         //Arrow function

  // getter method as _data array is private
  get data(): any {
    return this._data
  }
}
const queue = new Queue();
queue.push(0);
queue.push("Hi"); // Oops a mistake
console.log(queue.data);
```
* Part 2
```typescript
class Queue {
  private _data = [];
  push = (item: number) => this._data.push(item); //Arrow function
  // push = function (items) {
  //   return this._data.push(items)
  // }

  pop = (): number => this._data.shift();         //Arrow function

  // getter method as _data array is private
  get data(): any {
    return this._data
  }
}
const queue = new Queue();
queue.push(0);
queue.push("Hi"); //  ERROR : cannot push a string. 
console.log(queue.data);
```
* Part 3
```typescript
//Lets modify our code for any data type i.e. using generics
/** A class definition with a generic parameter */
class Queue<T> {
  private _data = [];
  push = (item: T) => this._data.push(item);
  pop = (): T => this._data.shift();
  get data(): any {
    return this._data;
  }
}
/** Again sample usage */
const queueNumber = new Queue<number>();
queueNumber.push(0);
queueNumber.push("Hi"); //  ERROR : cannot push a string.
console.log(queueNumber.data);
const queueString = new Queue<string>();
queueString.push(0);    //  ERROR : cannot push a number.
queueString.push("Hi");
console.log(queueString.data);
```

## Modules
* A module is a container to a group of related variables, functions, classes, and interfaces etc.
* Module file will contain `export` keyword and the file where you want use functionality provided by module, will contains `import` keyword
##### Example:
```typescript
//calculator.ts
//exporting calculator class 
export class Calculator {
  constructor(public firstNum: number, public secondNum: number) { }

  summation(): number {
    return this.firstNum + this.secondNum
  }
  substraction(): number {
    return this.firstNum - this.secondNum;
  }
}

//main.ts
// importing module calculator in main.ts
import { Calculator } from './index' 

let cal = new Calculator(10, 2);
console.log(cal.summation());
console.log(cal.substraction());
```
## Namespaces
Namespaces are used for grouping of variables, functions, objects, classes, and interfaces, so that you can avoid the naming collisions. Namespaces are declared using the `namespace` keyword.
##### Example:
```typescript
// namespace named collegeDatabase
namespace collegeDatabase {
  export class Student {
    constructor(private rollNo: number, private name: string) { }
    showDetails() {
      return console.log(this.rollNo + ", " + this.name);
    }
  }
  class StudentFee {
  }
  class StudentResult {
  }
  class StudentCources {
  }
}

// namespace named universityDatabase
namespace universityDatabase {

  import Student = collegeDatabase.Student;

  export class StudentResult {
  }
  class CollegeList {
  }
  class StudentCources {
  }
  let divA_St1 = new Student(1, 'Bob');
  divA_St1.showDetails();
}
```

## Javascript Objects Basics
* An object is a collection of related data and/or functionality
* It consists of several variables and functions - which are called "properties" and "methods' when they are inside objects.

##### Example
```typescript
var Person = {
  name: ['Bob', 'Smith'],
  birth: {
    day: 11,
    month: 'Jun',
    year: 1995
  },
  age: 32,
  gender: 'male',
  interests: ['music', 'skiing'],
  bio: function () {
    console.log(this.name[0] + ' ' + this.name[1] + ' is '
      + this.age + ' years old. He likes '
      + this.interests[0] + ' and ' + this.interests[1] + '.');
  },
  greeting: function () {
    console.log('Hi! I\'m ' + this.name[0] + '.');
  }
};

//Getting Object Values
//Dot notation
console.log(Person.name);         //["Bob", "Smith"]
console.log(Person.birth);        //{day: 11, month: "Jun", year: 1995}
console.log(Person.birth.month);  //Jun
console.log(Person.interests[1]); //skiing
Person.bio();         //Bob Smith is 32 years old. He likes music and skiing.
Person.greeting();    //Hi! I'm Bob.
//Bracket notation
console.log(Person['name']);            //["Bob", "Smith"]
console.log(Person['birth']);           //{day: 11, month: "Jun", year: 1995}
console.log(Person['birth']['month']);  //Jun
console.log(Person['interests'][1]);    //skiing

//Setting Object Values
Person.age = 45;                        //using Dot notation
console.log(Person.age);                //45
Person['birth']['month'] = 'Nov';       //using Bracket notation
console.log(Person['birth']['month']);  //Nov

//Adding New Values to Object
Person['eyes'] = 'hazel';
Person.farewell = function() { alert("Bye everybody!"); }

//Difference between Dot & Bracket
var myDataName = 'height';
var myDataValue = '1.75m';
Person[myDataName] = myDataValue;
console.log(Person.height);    //1.75m

```
* **The `this` keyword refers to the current object, the code is being written inside** 

##### Example: Object creation using constructor function
```typescript
//object creation using constructor function
function Person(first, last, age, gender, interests) {
  this.name = {
    'first': first,
    'last': last
  };
  this.age = age;
  this.gender = gender;
  this.interests = interests;
  this.bio = function () {
    alert(this.name.first + ' ' + this.name.last + ' is ' + this.age + ' years old. He likes ' + this.interests[0] + ' and ' + this.interests[1] + '.');
  };
  this.greeting = function () {
    alert('Hi! I\'m ' + this.name.first + '.');
  };
};
var person1 = new Person('Bob', 'Smith', 32, 'male', ['music', 'skiing']);
console.log(person1);

// Person {name: {…}, age: 32, gender: "male", interests: Array[2]…}
// age: 32
// bio: ƒ ()
// __proto__: Function
// gender: "male"
// greeting: ƒ ()
// __proto__: Function
// interests: Array[2]
// 0: "music"
// 1: "skiing"
// name: Object
// first: "Bob"
// last: "Smith"
// __proto__: Object
// __proto__: Person
```
