Introduced in java 1.5
Enum is a collection of constant and act as a datatype.
### Enum internally implemented by using class

```java
enum Week{
SUN, MON, TUE, WED, THU, FRI, SAT;
}

// is equivalent to class

class Week{
	public static final Week SUN= new Week();
	public static final Week MON= new Week();
	public static final Week TUE= new Week();
	public static final Week WED= new Week();
	public static final Week THU= new Week();
	public static final Week FRI= new Week();
	public static final Week SAT= new Week();
}

class Driver{
	psvm(){
		Week firstDay=Week.SUN;   // var firstDay now refers the same object referred                                      by SUN
	}
}
```
* Every Enum Constant is static. Hence we can access Enum values using Enum name

### Enum class extends java.lang.Enum & for this Enum cannot extend any other class, but it can implement any no. of interfaces
* java.lang.Enum is a direct child of Object class and it is `abstract`. Also it implements interface `Comparable` and `Serializable`
* Every enum is declared as `final` implicitly so we cannot extend it to child. 
* **So in short, Enum does not support Inheritance** 
* As Enum created using class, so it has toString(), equals() method. toString() is defined by java.lang.Enum in which you get name of the constant
* Like a class, we can define Enum outside a class, inside a class but not inside a method.
* For enum outside class, we have available modifiers: `public`, `default`, `strictfp`
* For enum inside class, we have  modifiers: `public`, `default`, `strictfp`, `private`, `protected`, 'static'
* Switch-case supports various Integer types like, byte, short, char, int and String and Enum
### Value & Ordinal:
* Every Enum implicitly contains values() method to return all values present inside Enum.
```Java
Week[] days= Week.values();  // days now contains 7 Week objects viz. SUN to SAT
```
* Within Enum the order of constants are important and we can represent this order by using Ordinal value.
* We can find the Ordinal value of enum constant by ordinal(): `public final int ordinal()`
* Ordinal value are 0 based index
```java
psvm(){
	Week[] days= Week.values();
	for(Week each: days){
		sout(each+"..."+each.ordinal())
	}
}
// output
SUN...0
MON...1
..
..
SAT...6
```
### Enum contains methods:
Unlike enums in other methods, ENums in Java can contain method, Constructors, Variables, other enums etc. But we cannot have class inside enums. We can have enums inside class.
* We can even write psvm() inside it and can execute from cmd.
* Enum constructor executes seperately for every Enum constant at the time of enum class loading
* Yes, enums are static constants but are not compile time constants. Just like any other classes enum is loaded when **first time needed.**
```java
enum Weekend{
	SAT, SUN
	Weekend(){
		sout("constructor called!")
	}
}
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Main 1st call!");
        Weekend w= Weekend.SUN;
        System.out.println("Hello, World!");
    }
    // Output
    Main 1st call!
Cons called!
Cons called!
Hello, World!
}
```
* We cant create enum objects explicitly, like using new keyword. and so we can't call enum constructor directly.

## Writing methods inside enum
I know enum are behind the scene is a class which can contains method(). Enum can also have methods.
```java
enum Weekend{
	FRI, SAT("Last day"), SUN("First day") ;
	String description;
	Weekend(String desc){
		this.description=desc;
	}
	Weekend(){
		this.description="Not a weekend";
	}

	public String getDesc(){
		return this.description;
	}
}
class Main {
    public static void main(String[] args) {
        System.out.println("Main 1st call!");
		Weekend[] w= Weekend.values();
		for(Weekend e: w){
			System.out.println(e+e.getDesc());
		}
    }
}
/* Output
Main 1st call!
FRINot a weekend
SATLast day
SUNFirst day
*/
```
Above Enum constant `FRI` is `public static final Weekend FRI= new Weekend();`
Enum constant `SAT("Last day")` is `public static final Weekend SAT= new Weekend("Last day");`

Note: We can declare only concrete methods inside, no abstract allowed.

## Treat Enum as a class, and Enum constant as object of that class.

This way you can understand:
```java
// Working syntax
Week.MON.equals(Week.FRI)
Week.MON==Week.FRI
Week.MON.hashCode()==Week.FRI.hashCode()
Week.MON.ordinal()==Week.FRI.ordinal()

// Compile time error code
Week.MON>Week.FRI;     // Ofcourse, both are reference of object can't be compared
```

* Just like a static field of a class, requires `static import` when want to use field without class name, here also using enum constant without enum name requires `static import`

## Anonymous Inner class in enum
It is possible to override an enum method for a particular constant. This is same as Anonymoys inner class.

```java
enum Color{
    Blue, Red{
        public String info(){
            return "Dangerous colour";
            }
        }, Green;
        
        public String info(){
            return "Good colour";
        }
    }
    
    class Main{
        public static void main(String[] args){
            Color[] c= Color.values();
            for(Color e: c){
                System.out.println(e.info());
            }
        }
}
// Output
Good colour
Dangerous colour
Good colour
```

## enum vs Enum vs Enumeration:
### enum: 
	is a keyword in java which can be used to Define a Group named Constants.
#### Enum:
	is a Parent class  java.lang.Enum
	every enum is a extended child of Enum class
#### Enumeration
	It is an interface present in java.util package.
	Its a cursor to get object from a collection one-by-one as a cursor.