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

# config/application.rb
## generatorでviewファイルを生成しない

```rb
module HelloWorldRails
  class Application < Rails::Application
    # Initialize configuration defaults for originally generated Rails version.
    config.load_defaults 5.2

    config.generators do |g|
      # ↓viewfileを生成しない
      g.template_engine false
      g.javascripts false
      g.stylesheets false
      g.helper false
      g.test_framework false
    end
    ↓apiモードで必要なものを生成する
    config.api_only = true

    # Settings in config/environments/* take precedence over those specified here.
    # Application configuration can go into files in config/initializers
    # -- all .rb files in that directory are automatically loaded after loading
    # the framework and any gems in your application.
  end
end
```
