# 最終行を取得

```vb
Cells(Rows.Count, 列番号).End(xlUp).Row
```

# 最終列を取得

```vb
Cells(行番号, Columns.Count).End(xlLeft).Column
```

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

# 文字列の右から○文字を消す
## 例
文字列"sample.xlsx"から左５文字（.xlsx）を消す

```vb
Left("sample.xlsx", Len("sample.xlsx") - 5)
```
## 解説
### Left
`Left(文字列, 数字)`
- 「文字列」の左から、「数字」分の文字列を抽出する

### Len
`Len(文字列)`
- 「文字列」の文字数を表示する

→ 右から○字消す = 左から(全文字数 - 消す数)分残す

# ユーザーフォーム

## ボタンにユーザーフォームの出現マクロを登録
`show`メソッドを使用する

例）`botton1`をクリックすると、`UserForm1`を出現させる
```vb
sub botton1_click()
  UserForm1.Show
end sub
```

## 文字数制限を設定
`MaxLength`プロパティーを変更する
最大４字だったら、「４」

## 入力モードを事前に設定
`IME Mode`プロパティーを変更する

### 一覧(一部)
|選択肢|概要|
|:-:|:-:|
|fmIMEModeDisable|IMEをOFF(手動変更不可)|
|fmIMEModeOff|IMEをOFFにし、英語モードに|
|fmIMEModeHiragana|全角ひらがな|
|fmIMEModeAlpha|半角英数モードでIMEをオンにする|

## tabキーを押したときの順番
`TabIndex`プロパティの数値を変更

## 表示されているタイトルの変更
`Caption`プロパティの値を変更

## ユーザーフォームの値を代入

例）`UserForm1`の`txt_box1`の値を変数`input_num`に格納
```vb
dim input_num as integer
input_num = UserForm1.txt_box1.Value
```
# ループを逆から回す(for~nextステートメントを使用)
例）イミディエイトウィンドウに100から１を順番に表示

```vb
dim i as integer
for i = 100 To 1 Step -1
  Debug Print i
next i
```
- `Step 数値`は次のループ時のカウンタ変数の増減を表す
  - `Step -3`だったら、１周目：i=100→２周目：i=97→３周目：i=94

# 条件分岐：○○でなければ（否定）
例）セルが空欄ではなければ、メッセージボックスで「何か入力してあります」と出力

 ```vb
if Not Range("A1").Value = "" then
  MsgBox "何か入力してあります。"
End if
 ```

`If Not ~ Then`と記載する。

# 行の番号を確認（イミディエイトウィンドウ）

イミディエイトウィンドウで
`? Range("A1").column`と入力
=>`1`が返ってくる

# 今日の年or月or日を取得

```vb
'年
Year(Date)

'月
Month(Date)

'日
Day(Date)
```
- `Date`は本日の年月日
- 各関数で抽出

# 行を削除する
例）１行目を削除する
```vb
  Row(1).Delete
```
※ 行ごと消すと、「削除後、上に詰める」しか考えられない
→ オプションは付けなくで問題ない

# 文字列かどうか判定
## サンプルコード

```vb
Dim input_data as integer: input_data = 3

if vartype(input_data) = vbInteger then
~
```
## 参考
[VarType 関数 \(Visual Basic for Applications\) \| Microsoft Docs](https://docs.microsoft.com/ja-jp/office/vba/language/reference/user-interface-help/vartype-function)