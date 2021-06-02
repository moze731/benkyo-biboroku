# テキスト操作

## .NET Core以降でのShift-JISを使う

.NET Core以降は、Shift-JISをサポートしていないので、以下のおまじないが必要。

```C#
Encoding.RegisterProvider(CodePagesEncodingProvider.Instance);
```