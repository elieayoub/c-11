# What's new in C# 11

## Static Abstract Members
C# 11 and .NET 7 include static virtual members in interfaces. This feature enables you to define interfaces that include overloaded operators or other static members. Once you've defined interfaces with static members, you can use those interfaces as constraints to create generic types that use operators or other static methods. Even if you don't create interfaces with overloaded operators, you'll likely benefit from this feature and the generic math classes enabled by the language update.

```csharp
var result = AddAll(new[] { 1, 5, 8, .1, 9});
WriteLine(result);

T AddAll<T>(T[] values) where T : INumber<T> {
  T result = T.AdditiveIdentity;
  foreach (var value in values) {
    result += value;
  }
  return result;
}
```

## Pattern Matching and List Patterns
Starting from C# 11, array or lists can be matched with sequence of elements.

So, let’s consider the example given below.

There is one array containing few numbers (Fibonacci series)
Then there is a conditional statement which is a probably different from what we have seen in the past. The if statement is using a ‘is‘ keyword and it is trying to match the Fibonacci series array with another list which is a comma separated list of numbers, specified between two square brackets.
The comparison would return true only if every element is present in both lists at exactly the same index. Below code example and its output should help us understand this easily.

```csharp
int[] example = { 1, 2, 3, 5, 8 };
bool result = false;

// result is false, as fibonacci ends with element 8
result = example is [..,  <8];

// result is true, 3 is third element from the ending
result = example is [.., >= 3, _, _];

// result is false, as first element is not greater than 1
result = example is [>1, .., 8];
```

## Field Access in Auto Properties
An instance property containing an init accessor is considered settable in the following circumstances, except when in a local function or lambda:

During an object initializer
During a with expression initializer
Inside an instance constructor of the containing or derived type, on this or base
Inside the init accessor of any property, on this or base
Inside attribute usages with named parameters
The times above in which the init accessors are settable are collectively referred to in this document as the construction phase of the object.

```csharp
class Base
{
    internal readonly int Field;
    internal int Property
    {
        get => Field;
        init => Field = value; // Okay
    }

    internal int OtherProperty { get; init; }
}

class Derived : Base
{
    internal readonly int DerivedField;
    internal int DerivedProperty
    {
        get => DerivedField;
        init
        {
            DerivedField = 42;  // Okay
            Property = 0;       // Okay
            Field = 13;         // Error Field is readonly
        }
    }

    public Derived()
    {
        Property = 42;  // Okay 
        Field = 13;     // Error Field is readonly
    }
}
```
