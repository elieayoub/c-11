# What's new in C# 11

## Static Abstract Members
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
