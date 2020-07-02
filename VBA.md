# 最終行を取得
`Cells(Rows.Count, 列番号).End(xlUp).Row`

# 日付の比較
- 比較する値の両方とも、<u>日付型</u>にする
- 文字列型を数値型に変更する場合は、`CDate関数`を使用する

## CDate関数
[CDate 関数の例](https://docs.microsoft.com/ja-jp/office/vba/language/concepts/getting-started/type-conversion-functions#cdate-function-example)

```vb
Dim MyDate, MyShortDate, MyTime, MyShortTime
MyDate = "February 12, 1969" ' Define date.
MyShortDate = CDate(MyDate) ' Convert to Date data type.

MyTime = "4:35:47 PM" ' Define time.
MyShortTime = CDate(MyTime) ' Convert to Date data type.

```

# IIF関数（三項演算子っぽいもの)
## 構文
`IIF(条件, trueのとき, falseのとき)`

## 例
```vb
Dim x As Long: x = 2
Debug.Print IIF(x Mod 2 = 0, "偶数", "奇数")
```

# 変数を使って、範囲を指定する
Rangeオブジェクト内でCellsを使用するときの書き方

```vb
Range(Cells(n,1), Cells(m,3))
```
※ n,m はinteger型の変数

# セルの値をクリアする
`Range("A1").Clear`

# 全シートに対して処理をしたいとき
- `For Each ~ Next`を使用する。
- Workbooksコレクション、Worksheetsコレクション等でも使える

例
```vb
Dim datasheet As Worksheet

For Each datasheet In Worksheets
  処理
Next datasheet
```

# ディレクトリ内の全ファイルを処理
## サンプル
sampleディレクトリ内の`.xlsx`ファイル名をイミディエイトウィンドウに表示する

### コード
```vb
Sub Sample1()
    Dim buf As String, cnt As Long
    Const Path As String = "C:\Sample\"
    '↓ポイント①
    buf = Dir(Path & "*.xlsx")
    'ポイント②
    Do While buf <> ""
        Debug.Print buf
        '↓ポイント②
        buf = Dir()
    Loop
End Sub
```

### 解説
- ポイント①
  - Dir関数の第１引数には、ディレクトリのパスを指定
  - Dir関数の第２引数には、検索するファイルを指定する。
    この例では、ワイルドカード（`*`）を使用して、`.xlsx`の全ファイルを取得

- ポイント②
  - マッチしたファイルが複数ある場合は、繰り返し処理で複数ファイルで同様の処理ができる。
  - 次のマッチしたファイルを呼び出すときは、Dir関数を引数なしで呼び出す。(`buf = Dir()`の部分)
  - マッチするファイルがない場合、Dir関数は長さ０の文字列(`""`)を返す。（`Do while buf <> ""`の部分）

## 参考
- [Dir 関数 \(Visual Basic for Applications\) \| Microsoft Docs](https://docs.microsoft.com/ja-jp/office/vba/language/reference/user-interface-help/dir-function)
- [Office TANAKA \- ファイルの操作\[ファイルの一覧を取得する\]](http://officetanaka.net/excel/vba/file/file07.htm)


# 変数の定義と代入を一行で
## 例
```vb
dim name as string : name = "ddaawwaa"
```
この例に限らず、`:`を使えば、複数行を１行にまとめることができる

# セルの文字を「折り返して全体を表示する」
## 例
A1セルの文字を「折り返して全体を表示する」

```vb
Range("A1").WrapText = true
```
## 参考
[WrapText プロパティ \(Excel\) \| Microsoft Docs](https://docs.microsoft.com/ja-jp/office/vba/api/excel.range.wraptext)


# 縦位置を中央揃えする
## 例
A1セルの文字の「縦位置を中央揃え」にする

```vb
Range("A1").VerticalAlignment = xlCenter
```

## 参考
[指定範囲の一方向の配置プロパティ \(Excel\) \| Microsoft Docs](https://docs.microsoft.com/ja-jp/office/vba/api/excel.range.verticalalignment)