# 宣言と初期化子

型の宣言など、よく忘れるものの備忘録

## 宣言

### 構造体

複数型を組み合わせた、複合型。
Classとの使い分けが難しい。基本的にはClassでいいと思われる。
16バイト以下の、小さな複合型なら値型の構造体に軍配が上がる。

```C#
// 一番シンプルな構造体
struct Human {
    public int Id { get; set; }
    public string Name { get; set;}
}

// interfaceを実装できる
struct Person : IPerson {
    public int Id { get; set; }
    public string Name { get; set; }

    public Person(int _id, string _name){
        id = _id;
        Name = _name;
    }
}
```

## 初期化子

### List<T>

値型のシンプルな初期化

```C#
var list = new List<int> { 1, 2, 3, 4, 5 };
```

クラスのプロパティも同時に初期化
```C#
class Prop
{
    public string Name { get; set; }
    public int Age { get; set; }
}

static class Hoge
{
    static void Main()
    {
        var list = new List<Prop>
                    {
                        new Prop() { Name="Jon" Age=20 },
                        new Prop() { Name="Taro" Age=10 }
                    };
    }
}
```

### Dictionary

