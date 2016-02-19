## 開発した作品について
- [デプロイURL](http://sprint-koji.herokuapp.com/)
- [ソースコードURL](https://github.com/kojisato118/codecheck-970)
  - 別チャレンジで利用していたリポジトリをそのまま利用
  - 締め切りまでにはこのリポジトリに統合したい

## 選択したオリジナル実装機能
- クライアントサイドの実装
  - [masonry.js](http://masonry.desandro.com/)を用いて一覧表示

- ページネーションの実装
  - ページ下部の"もっと見る"ボタンで次ページのコンテンツを取得し追加表示する
  - 実装としては、[kaminari](https://github.com/amatsuda/kaminari)を利用した

- バリデーションの実装
  - 課題とはちょっとずれると思いますが、modelにpresence: trueのvalidationや、外部apiから取得したコンテンツのidにuniqueness: trueなどを加えた

- 画像のアップロード
  - [paperclip](https://github.com/thoughtbot/paperclip)を用いて画像アップロード機能を実装
  - 画像保存先はプロジェクト内部とした
  - 将来的にはs3などのストレージサービスに流したい

- タグ機能
やる予定

- 外部 API 連携
  - Qiitaから自分の投稿を取得
  - ([LiSAのinfomation](http://www.lxixsxa.com/info/)情報を取得)
    - 個人の利用としてとどめます

- その他オリジナルアイディア
  - 管理機能
    - [管理画面](http://sprint-koji.herokuapp.com/admin)
    - [rails admin](https://github.com/sferik/rails_admin)を利用
  - APIドキュメント　
    - [ドキュメント](http://sprint-koji.herokuapp.com/swagger)
    - [grape-swagger-rails](https://github.com/ruby-grape/grape-swagger-rails)を利用

## その他、アピールポイント
- [RSpec](http://rspec.info/)を用いたテストを書いています。
- その他諸々を[Wiki](https://github.com/kojisato118/codecheck-998/wiki)にまとめる予定です。
