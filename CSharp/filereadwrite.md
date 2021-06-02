# ファイル操作の読み書き

## ファイル操作のAPI

C#でファイルを操作する場合の選択肢は大きく以下

- System.IO.Fileクラスを使用した簡単操作  
静的メソッドで、簡易操作する
- System.IO.Streamクラスを使用した詳細操作      
Stream操作により、部分削除、部分挿入、ファイル位置の移動等を使用した、より複雑な操作が可能

## System.IO.File

### テキストファイルの行単位読み込み

行単位読み込みは、基本的にIEnumerableで応答するSystem.IO.File.ReadLinesを使用する。

```C#
using Sytem.IO;

var lines = File.ReadLines(@"file/sample.txt");
// SHIFT-JISで読み込む場合は、第二引数にEncodingを設定
// var lines = File.ReadLines(@"file/sample.txt", Encoding.GetEncoding("shift_jis"));
foreach(var line in lines){
    System.Console.WriteLine(line);
}
```

メリットとしては、LINQで扱えるため、ファイル内容をメモリには吐き出さない。必要な時にメモリに抱えるため、メモリ節約と同期処理でも遅延を最小にできるメリットがある。

System.IO.File.ReadAllLinesで、string[] として一気にメモリに読み込むことも可能だが、メモリ圧迫と読み込み時に同期処理の場合、フリーズするため、非同期処理g亜必要になる。

### テキストファイルの全読み込み

ファイル内のテキストを単一のstring変数に格納する。

```C#
using Sytem.IO;

var text = File.ReadAllText(@"file/sample.txt");
// var text = File.ReadAllText(@"file/sample.txt", Encoding.GetEncoding("shift_jis"));
System.Console.WriteLine(text);
```

## System.IO.FileStream

### 複雑なファイル操作

行挿入などの、ファイル位置を操作留守場合は、Streamを使用する。

```C#
using(var file = new FileStream(@"file/sample.txt", FileMode.Open, FileAccess.ReadWritFileShare.None))
{
    using(var reader = new StreamReader(file, Encoding.GetEncoding("shift_jis")))
    using(var writer = new StreamWriter(file, Encoding.GetEncoding("shift_jis")))
    {
        string t = reader.ReadToEnd();
        file.Position = 0;
        string insert = "insert row !!!!!";
        writer.WriteLine(insert);
        writer.Write(t);
    }
}
```

上の例は、ファイルを他プロセスからの読み込み不可で開き、ファイルの内容を全読み込み後、1行目に行追加。その後、最初に読み込んだファイル内容を再度書き込むことで、ファイルの先頭に行追加している。