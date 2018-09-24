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



