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