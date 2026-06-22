### Tips & Tricks for XML documentation
📌 Reuses tags comment tags from another member via `inheritdoc`.
```xml
<remarks><inheritdoc cref="Update"/></remarks>
```
---
📌 Reuses documentation tags from another member via `inheritdoc`.
```xml
<remarks>
    <inheritdoc cref="Update(bool)" path="/param[@name='includeId']"/>
</remarks>
```
## 📒 External Links
[Recommended XML tags for C# documentation comments](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/xmldoc/recommended-tags) 