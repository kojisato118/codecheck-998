## 開発した作品について
### 作品場所
- [デプロイURL](http://sprint-koji.herokuapp.com/)
- [ソースコードURL](https://github.com/kojisato118/codecheck-970)
  - 別チャレンジで利用していたリポジトリをそのまま利用しています
  - このリポジトリに統合を計画中です

### 概要
 ポートフォリオということなので、作品の一覧が表示されるUIを作成しました。その際、レスポンシブになるようmasonry.jsを利用しました。
また、このアプリケーションで作成されるProjectsレコードよりも、外部のデータ表示に主軸をおき、自身のQiitaへの投稿と所属する研究室のPublicationを表示するようにし、さらに、自己表現として大好きなLiSAのinformationを表示できるようにしました。これらを実現するために**API連携とWebスクレイピングの技術**を利用しました。    
 バックエンド側では、独自でTestを作成したり、validationの実装、管理機能やapiのドキュメント作成など**"動くだけ"のものとならないよう**配慮しました。


## 選択したオリジナル実装機能
- クライアントサイドの実装
  - [masonry.js](http://masonry.desandro.com/)を用いて一覧表示→[TOP](http://sprint-koji.herokuapp.com/)
  - (簡易的な)投稿ページ→[投稿ページ](http://sprint-koji.herokuapp.com/projects/new)

- ページネーションの実装
  - ページ下部の"もっと見る"ボタンで次ページのコンテンツを取得し追加表示
  - apiを利用するクライアントによっては取得件数を絞りたい可能性があるので、一ページあたりの件数の指定も可能
  - 実装としては、[kaminari](https://github.com/amatsuda/kaminari)を利用

- バリデーションの実装
  - urlに対して```/\A#{URI::regexp(%w(http https))}\z/```というformatのvalidation
  - imageに対して```/\A#{URI::regexp(%w(http https))}.\*(png|jpg|jpeg|gif).\*\z|\/images\/medium\/no_image.png/```というvalidation
  - 課題とはちょっとずれると思いますが、modelに```presence: true```のvalidationや、外部apiから取得したコンテンツのidに```uniqueness: true```などのvalidation

- 画像のアップロード
  - [paperclip](https://github.com/thoughtbot/paperclip)を用いて画像アップロード機能を実装
  - 画像保存先はプロジェクト内部
  - 将来的にはs3などのストレージサービスの利用を検討

- タグ機能
  - [act_as_taggable](https://github.com/mbleigh/acts-as-taggable-on)を利用して実装

- 外部 API 連携
  - Qiitaから自分の投稿を取得
  - ([LiSAのinfomation](http://www.lxixsxa.com/info/)情報を取得)
    - LiSAが好きなので入れてみました！
    - 個人の利用としてとどめます

- その他オリジナルアイディア
  - 管理機能
    - [管理画面](http://sprint-koji.herokuapp.com/admin)
    - [rails admin](https://github.com/sferik/rails_admin)を利用
    - ログインの必要
  - APIドキュメント　
    - [ドキュメント](http://sprint-koji.herokuapp.com/swagger)
    - [grape-swagger-rails](https://github.com/ruby-grape/grape-swagger-rails)を利用
  - 研究室HPのスクレイピング
    - 研究室のHPからpublication情報を抜き出し表示
  - 管理者権限
   - 投稿ページや管理画面など一般に公開すべきでないページにauthenticationを必要にしました
 - 定期バッチ処理
   - ページを表示する際に毎回外部のapiを叩くのは非効率なので、1時間ごとにcronでデータを取得するようにしました
    - local環境では[wheneber](https://github.com/javan/whenever)を利用しました
     - herokuではheroku schedulerを利用しました
 - ER図の作成
   - プロジェクト直下にerd.pdfを作成

## その他、アピールポイント
### 様々なコンテンツ
課題として出されたProjectsテーブルにこだわらず、qiitaや研究室のpublication、LiSAのinformationなど様々なコンテンツを表示できるようにしました。

### 技術的な挑戦
APIの利用(自身の、qiita、LiSA)やWebスクレイピングなどのデータ取得のための技術、masonry.jsやjquery、cssなどデータを表現する技術など様々な技術を利用するよう挑戦しました。

### セキュリティへの配慮
投稿画面や管理画面はグローバルに公開されるべきでないためログインを必須にしました。また、urlに対して```javascript:alert('XSS');//http://example.com/```のような値が入らないようなvalidationをかけました。   
ただし、apiのpostに対しても認証を用意したかったですが、未実装です。

### 独自のテスト
[RSpec](http://rspec.info/)を用いたテストを書いています。
```spec/``` にあります。結合テストは用意していませんが、modelとapiに関してのテストを用意しています。

### Wikiの利用
導入手順と機能一覧などを[Wiki](https://github.com/kojisato118/codecheck-998/wiki)にまとめる予定です。
機能一覧にはその機能実装に利用したgemや参考ページ、プロジェクトのどこに記載されているかなどをまとめています。
