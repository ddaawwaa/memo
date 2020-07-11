# (コマンド)bundle exec rails -T
- railsから始まるコマンドを一通り確認できる

# データベースのリセット方法
## `rails db:reset`
データベースを一度削除し、<u>schema.rb</u>とおりにデータベースを作り直す

## `rails db:migrate:reset`
データベースを一度削除し、<u>migrationファイル</u>に従ってデータベースを作り直す
こっちがおすすめ

# active record
## pluck
任意のカラムの値をArrayで取得

```ruby
user = User.all
user.plick(:id)
# [1, 2, 3, 4]
```

# renderでcontrollerからjsonを返す
viewファイルではなく、jsonをコントローラーから返したい場合

```ruby
class UsersController < ApplicationController
  def index
    @users = User.all
    render json: @users
  end
end
```
`render`メソッドに`:json`を記載する

参考 [render \| Railsドキュメント](https://railsdoc.com/page/render)