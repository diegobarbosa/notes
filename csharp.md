## Bitwise operators
- | : OR bitwise
- & : AND bitwise
- ^ : bitwise exclusive OR
- ~ : The bitwise complement operator

## Logical 
- ! - Unary logical negation operator. Don´t work as bitwise
- num % 2 == 0 ? "even" : "odd" - ternary operator
- expr1 && expr2 : short-circuit evaluation, if first expr1 is false the second expr2 is not evaluated; Improves performance;
- expr1 || expr2 : short-circuit evaluation, if first expr1 is true the second expr2 is not evaluated

## Relational
- < Less than expr1 < expr2
- > Greater than expr1 > expr2
- <= Less than or equal expr1 <= expr2
- >= Greater than or equal expr1 >= expr2
- == Equality expr1 == expr2
- != Not equal expr1 != expr2

## switch
```
// switch statement syntax
switch (condition)
{
  case 1:
    statement1;
  break;
  case 2:
    statement2;
  break;
  case 3:
    statement3;
  break;
  default: // OPCIONAL
    defaultStatement;
  break;
}
```

## for
used when the list size is know in advance

```
for(initializer; condition; iterator)
{
  statement(s);
}
```

#foreach
Use when the list has a unknow size

# while
- Condition variable must be declare outside while. 
- Only executes if condition is true, may neve execute.

```
// while statement syntax
while(condition)
{
  statement;
}
```
# do-while
- Condition variable must be declare outside while. 
- Executes only time at least.

```
// do-while loop syntax
do
{
    statement;
} while (condition);  // (";" must be informed)

```

## Enumerations
```
// enum called Months, using default initializer
  enum Months {Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sept, Oct, Nov, Dec};

// enum call Months, using an overidden initializer
  enum Months {Jan = 1, Feb, Mar, Apr, May, Jun, Jul, Aug, Sept, Oct, Nov, Dec};
  
  // using a non-default data type for an enum
enum Months : byte {Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sept, Oct, Nov, Dec};
  
  
```

## C# Modifiers
- readonly: Read-only members can be assigned only during declaration or in a class constructor.
No other means of changing or assigning a value to that member are permitted.
- internal: Allows access only within files in the same .NET assembly
- extern: Used to indicate that the method has been declared and implemented externally.
You might use this with imported DLLs or external assemblies.
- sealed:  Applied to classes. Sealed classes cannot be inherited.
- unsafe: Using the unsafe keyword declares a context that is not safe in terms of memory management.
- volatile: When this modifier is applied to a field, the field can be modified by components other than your code. Examples might be the operating system.

## Constructors

A constructor is a method but includes no return type, not even void. To include
a return type in a constructor is improper syntax and will generate a compiler warning.
In the Student class code, there are two constructors provided. One is a nondefault constructor that
accepts three string values and uses them to initialize the member variables. The second is a default constructor that includes no statements and takes no arguments. This is the type of constructor that
the compiler generates if no other constructors are created by the developer. This constructor initializes
the member variables with their default values.

**Default constructors are used only when no other constructor is called or
none exist.**
