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
